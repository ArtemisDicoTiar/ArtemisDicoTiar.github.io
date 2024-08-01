---
title: 'AI models collapse when trained on recursively generated data'
categories:
  - Daily Paper reading
last_modified_at: 2024-08-01
tags: [paper, reading, Nature]
---

* Reference: [Paper Link](https://www.nature.com/articles/s41586-024-07566-y)
* 정리 순서: Abstract → Implementation/Idea → Ablation Study/Analysis → Reflections

# 0. First feelings
* 최근에 나온 페이퍼중에 가장 핫했던 페이퍼 중에 하나.
  * (저자들이 누군가하고 봤더니 역시나 영국..)
  * 유튜브에서는 인공지능 모델의 근친혼과 같다. 라는 식으로까지 말하기도했음.
  * 하지만 그렇게까지 얘기할 페이퍼는 아닌거 같음.
  * 이유는 LLM generated data is then again fed into the same LLM 인줄 알았는 데 그게 아니였음.
  * 저자들은 이걸 실험하는 데에 비용도, 환경 문제도 심하니 OPT-125M로 실험함. 즉, LLM에서의 영향에 대한 결과는 절대 아님.
  * 그렇기 때문에 이 결과를 가지고 "와 우리 이제 LLM으로 데이터 생성하면 절대 안되겠는데?"는 아님.
  * 그렇지만 여전히 그 영향이 같은 transformer 기반인 모델들이니 고려는 하는 게 좋다.
  * (추가로 페이퍼에서는 작은 모델에서도 그 영향이 있다는 걸 보였으니 더더욱...)
* 이유는 간단하다. 사람들이 마냥 생각하던/혹은/대략적인 실험으로 확인된 생성된 데이터로 학습하면 모델이 망가지지 않을까?
* 이걸 확인했기 때문.
* 네이처 페이퍼다 보니 실험이 extensive한 편이고, 결과 정리, 문체 모두 굉장히 깔끔하다.
  * 용어의 정의, 정의의 세부 정의, 문단 정리, 내용 구성 모두 어디하나 흠잡을 때 없는 페이퍼.
* 한번 읽어볼법한 페이퍼.
* 세부 내용은 죄다 supplementary materials 로 빼는 건 네이처 특징이니 주의.

# 1. Abstract 
* 페이퍼에서 하는 이야기가 곧 제목이다.
  * AI 모델이 생성한 데이터로 학습하면 모델이 망가진다.
* 네이처 페이퍼이니만큼 ours로 propose된 메소드는 없고 현상에 대한 발견이 주된 내용.
* 망가지는 이유를 3가지 정도로 정의했는데
  * Statistical approximation error
    * 데이터 샘플링으로 인해 생기는 문제
  * Functional expressivity error
    * 모델이 어떻게 표현하는 가에 대한 문제
    * 예를 들어, quantization처럼 표현할 수 있는 범위가 부족해서, 실제로는 없는 확률을 표현할 수도 있음.
  * Functional approximation error
    * 모델이 infer할 때 생기는 문제
    * 근데 사실상 SGD의 문제가 아닌가.

# 2. Idea & Implementation
* 실험 데이터: 위키 텍스트
* 사용한 모델
  * discrete distribution
  * multidimensional gaussian
  * LM (OPT-125M)


# 3. Ablation study/Analysis
* 위에서 언급한 3개 모델에서 모두 생기는 문제다.
* 중요한 결과는
  * 실제로 없는 분포로 이동한다.
  * 0인 공간에 1이 생기고, 1인 공간에 0이 생기는
  * 쉽게 말해 original dataset에 있는 tail는 소실되고, 없던 tail이 생긴다.

# 4. Reflections
* 네이처다운 페이퍼였다. 굉장히 읽기 편했고, 내용 구성도 잘 되어 있고. 실험에 대한 설명도 구체적이어서 좋았다.
* 그 악명과 달리 LLM에 대한 직접적인 이야기는 아니라서 실망.
* 그래도 어떻게 글을 쓰면 좋은지 얻어갈 수 있었던 페이퍼.
