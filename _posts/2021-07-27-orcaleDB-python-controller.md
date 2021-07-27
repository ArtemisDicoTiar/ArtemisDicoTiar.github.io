---

title: DB controller for oracle cloud

categories:
  - Cloud Server
  - storyteller
last_modified_at: 2021-07-27

tags: [oracle cloud, server, setting, python, mysql]

---

# 오라클 MySQL with python

이전에 쓴 글에서 시도한 것처럼 게이트웨이 인스턴스에 리버스 프록시를 두고 바로 데이터베이스 서버로 연결되게 하려고 했으나 실패...

그래서 파이썬에서 DB저장 시도할때 ssh 터널링 되게끔 해야한다.

## SSH tunneling in python

찾아보니깐 관련 라이브러리가 있어서 어렵진 않아보인다.

[이 글](https://practicaldatascience.co.uk/data-science/how-to-connect-to-mysql-via-an-ssh-tunnel-in-python)을 참고해서 작성해보자.

### .env 환경변수 설정

내가 자주 쓰는 프로젝트 구조가 아래와 같다.

~~~
.env에 환경변수 작성 → secrets.py에서 필요한 변수 로드 → 다른 파이썬 파일에서 사용
~~~

그렇기 때문에 환경변수에 서버 주소 포트 부터 작성해줘야한다.

### base tunnel connector class 작성

혹여나 나중에 해당 게이트웨이 인스턴스로 다른 데이터 베이스나 애플리케이션 접속 혹은 연결해야하는 경우를 대비하여 해당 작업을 독립된 클래스로 작성, DB 컨트롤러에서 사용.

~~~python
class SSHTunnel:
    def __init__(self,
                 gateway_addr: str,
                 gateway_port: int,
                 gateway_user: str,
                 gateway_public_key: str,

                 database_addr: str,
                 database_port: int,
                 ):
        self.__local_port = 33600

        self.gateway_addr = gateway_addr
        self.gateway_port = gateway_port
        self.gateway_user = gateway_user
        self.gateway_public_key = gateway_public_key
        self.database_addr = database_addr
        self.database_port = database_port

        self.tunnel = self._establish_tunnel()

    def _establish_tunnel(self):
        return SSHTunnelForwarder(
            ssh_address_or_host=(self.gateway_addr, self.gateway_port),
            ssh_username=self.gateway_user,
            ssh_pkey=self.gateway_public_key,
            remote_bind_address=(self.database_addr, self.database_port),
            local_bind_address=('127.0.0.1', self.__local_port)
        )

    def get_DB_engine(self, database_user: str, database_pw: str):
        return create_engine('mysql+mysqldb://{user}:{pw}@{addr}'
                             .format(user=database_user, pw=database_pw,
                                     addr='127.0.0.1:{port}'.format(port=self.__local_port)),
                             encoding='utf-8')
~~~

터널 클래스에 DB엔진 생성까지 넣었다. 생각해보니깐 터널을 생성하면 로컬에서 사용하는 포트가 해당 터널 클래스에서 지정되는 데 다른 클래스에서 그걸 참조하게 하려면 public변수로 지정해야한다. 하지만 해당 포트는 외부에서 안보이게 private처리하는 게 좋을 거 같아서 DB엔진 생성 메소드까지 넣었다. 

(파이썬에서 private하게 변수 생성하는 방법은 언더스코어를 변수명/메소드명(함수명) 앞에 달면 된다. )

(언더스코어 하나면 클래스 외부에서 접근이 가능하다. 애초에 파이썬은 private public 개념이 없다. 그래서 그렇다. 하지만 외부에서 "_변수"에 접근하게 되면 IDE수준에서 워닝을 띄워준다. 되도록이면 숨겨진 변수에 접근하지 말라는 거다.)

(언더스코어가 두개면 접근자체가 안된다. 외부에서 접근하려면 인터프리터가 Mangling하는 것처럼 

~~~
_클래스__변수명
~~~

의 형태로 접근해야한다. 그냥 누군가 __변수 이렇게 해두면 외부에서 사용하지 말라는 거다.)



### DB controller 

이제 여기는 평소에 쓰던 그 컨트롤러에 터널을 start 시키고 작업 끝나면 close시키는 코드 + 터널 establish 하고 DB오류나면 finally close하는 코드 넣으면 끝.

~~~python
class DBController:
    def __init__(self,
                 user: str,
                 password: str,
                 schema: str
                 ):

        self.database_user = user
        self.database_pw = password
        self.database_schema = schema

        self._tunnel_builder = SSHTunnel(
            gateway_addr=GW_HOST,
            gateway_port=GW_PORT,
            gateway_user=GW_USER,
            gateway_public_key=GW_PKEY,

            database_addr=DB_HOST,
            database_port=DB_PORT,
        )

    def start_tunnel(self):
        try:
            self._tunnel_builder.tunnel.start()

        except:
            raise ConnectionError("SSH Tunnel Establish Failed")

    def close_tunnel(self):
        self._tunnel_builder.tunnel.close()

    def _get_engine(self):
        global engine
        if self._tunnel_builder.tunnel.is_active:
            return self._tunnel_builder.get_DB_engine(database_user=self.database_user, database_pw=self.database_pw)
        
        else:
            raise ConnectionRefusedError("To obtain DB engine, you must start the tunnel.")

    def get_df_from_sql(self,
                        target_query: str) -> pd.DataFrame:
        global engine, query_result
        
        self.start_tunnel()
        
        try:
            engine = self._get_engine()

        except:
            raise ConnectionError("DB connection Establish Failed.")

        else:
            query_result = pd.read_sql_query(sql=target_query, con=engine)

        finally:
            engine.dispose()
            self.close_tunnel()

        return query_result

    def save_df_to_sql(self,
                       origin_df: pd.DataFrame,
                       target_table_name: str,
                       if_exists: str,
                       index: bool):
        self.start_tunnel()
        global engine
        try:
            engine = self._get_engine()

        except:
            raise ConnectionError("DB connection Establish Failed.")

        else:
            origin_df.to_sql(
                con=engine,
                name=target_table_name,
                schema=self.database_schema,
                if_exists=if_exists,
                index=index
            )

        finally:
            engine.dispose()
            self.close_tunnel()
~~~



여기까지 쓰고 나서 생기는 문제

1. 판다스가 안도와준다. 하아..
   1. MariaDB를 사용할때와는 달리 MySQL은 Primary key를 무조건 지정해야한다.
   2. 근데 판다스에서 to_sql을 사용할 때 primary_key 를 지정하는 파라미터같은 게 없다.
   3. 그래서 그냥 그대로 에러. (Create fail)

해결책

1.  append는 문제가 안된다. 생성 문제 이므로 if_exists가 replace인 경우만 해결해야한다.
   1. 내가 직접 if_exists == 'replace' 확인
      1. 테이블이 DB에 있으면 해당 테이블 Drop
   2. TABLE 먼저 생성
   3. 그리고 to sql은 무조건 fail로 (테이블이 있으면 ValueError발생시킨단다.)
2. DB 테이블 존재여부 확인은 기존에 쓰던 코드 들고 와야겠다.
   1. 저장 로직자체를 거의 다 새로 썼다 허허허허 아니 판다스 라이브러리 업데이트에 이런거 왜 추가 안하는 거지.



## Conclusion

이제 만들어놓은 DB, Tunnel 클래스를 이용해서 크롤링된 내용을 저장 할 수 있다.

**다만! 주의 할점**은 MariaDB랑은 달라서 무조건 Schema를 미리 생성해줘야한다. 실험은 test 스키마에서 했고. 앞으로는 ****이라는 스키마에 저장 예정. secrets에 컨트롤러 생성해뒀으니 이 컨트롤러 바로 import해서 쓰면 될듯.
