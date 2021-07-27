---

title: Oracle Cloud Setting 3

categories:
  - Cloud Server
last_modified_at: 2021-07-27

tags: [oracle cloud, server, setting, nginx]

---

# 오라클 클라우드 서버 설정 3

SSH forwarding으로 GW에서 MySQL로 연결시키려했는데 그게 안되서 그냥 nginx로 리버스 프록시 설정하려고 한다.

설정하다 알게된건데 http와 무관한 TCP/UDP 통신의 경우 stream 블럭에 작성해야한다는 것을 알게 되었다.

[nginx reverse proxy for TCP/UDP](https://docs.nginx.com/nginx/admin-guide/load-balancer/tcp-udp-load-balancer/)

설정했는데 안된다

그냥 파이썬에서 ssh 터널 생성후 DB에 저장하는 형태로 시도해야겠다. [방법](https://practicaldatascience.co.uk/data-science/how-to-connect-to-mysql-via-an-ssh-tunnel-in-python)

