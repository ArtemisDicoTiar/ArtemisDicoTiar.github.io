---
title: 'Buffer of thoughts: Though-Augmented Reasdoning with Large Language Models'
categories:
  - Daily Paper reading
last_modified_at: 2024-07-30
tags: [paper, reading, arxiv, preprint]
---

* Reference: [Paper Link](https://arxiv.org/pdf/2406.04271)
* 정리 순서: Abstract → Implementation/Idea → Experiment → Result → Conclusion/Introduction

# 1. Abstract (간단 정리)
* proposed: Buffer of thoughts, thought들을 저장해두고 이걸 검색해서 프롬프트에 활용해두는 방법.
* 사람이 생각하는 방식 처럼 여러 문제에 대한 가능한 해결 경로들을 생각 저장소라는 데에 넣어두고, 문제가 발생하면 각 문제 해결 템플릿을 검색해와서 그 프롬프트로 해결.

* 문제점: Chain of thought이니 Tree of thought 이니 여러 프롬프팅 방법론들이 많았는데 이들은 두가지 문제를 가지고 있었다.
	* CoT 같은 single query reasoning: 하나의 길로만 가기 때문에 이 길이 최적화가 안되어 있으면 성능이 그리 좋지 않음.
	* ToT 같은 multi query reasoning: 여러 길을 찾아봐서 복잡한 문제를 잘게 쪼개서 푸는 게 가능. 하지만 여러 노드가 생겨서 비효율적임.


# 2. Idea & Implementation
아이디어도 그렇고 구현 자체도 굉장히 심플하다.
그냥 prompt template을 여러개 만들어서 buffer 공간에 저장.
embedding similarity를 기반으로 관련 있는 템플릿 가져와서 프롬프트 적용.

근데 계속 넣으면 buffer가 넘칠테니 buffer manager를 달아놓음.
적당히 관련 있는 템플릿 위주로만 남김.

오히려 problem distiller로 설명되어 있는 부분이 중요해보임.
문제의 핵심을 잘 남기게 한다. (keyword)
그 후에 condenstation and translation 을 통해 natural language 레벨로 가지고 온다.

# 3. Questions
prompt template을 만들어가는 과정은 어떻게 되는 거지..?
during inference? 그러면 처음 푸는 문제랑 이후에 푸는 문제랑 성능차가 많이 날거 같은데?
그리고 이렇게 in-task 문제로 thought을 쌓아나가다보면 자연히 성능이 오르지 않나..?
아 아니다. 문제를 푸는 과정에서 이게 성공했는지
 실패했는지에 대한 피드백은 안들어오니...

