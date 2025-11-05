제 1 장은 Generative AI에 대한 개념, 종류, 간단한 실제 사례, 다양한 애플리케이션들, 극복과제/한계, 윤리적/사회적 함의에 대한 간략한 설명이다.

Generative AI를 간단히 설명하면 training 데이터와 입력값를 사용하여 **새로운** 자료를 만들어 낸다는 점이다.
이 새로운 자료는 만들어 내는 것이 discriminative 모델과 다른 점이다.

종류로 크게 세가지가 제시되고 있다: VAE, GAN, Autoregressive models.
1. VAE (Variational AutoEncoder). training 통해 데이터와 latent space사이의 관계를 만들고 그것을 사용하는 방식이다.
2. GAN (Generative Adversarial Network). 상반된 목적을 가진 두 개의 모델이 동시에 training 된다. generator/discriminator. 
generator는 이미지를 생성하고 discriminator는 생성된 이미지가 가짜인지 진짜인지 판별한다. 
3. Autoregressive models는 생성된 데이터가 다음 단계에서 조건으로 사용되는 방식으로 순차적으로 데이터를 생성한다.

Transformer와 LLM (Large Language Model)에 대한 개념 정리는 정확히 제시하고 있는 것 같지는 않다.
문맥 구조상으로는 Autoregressive models에 확장판 같은 걸로 취급하는 듯하나 
Autoregressive 설정도 Non-Autoregressive 설정과도 사용될 수 있다고 하니 정확한 개념을 잡기는 힘들었다.

다음으로 여러가지 LLM이 나열된다. 
Autoregressive LLM, Encoder-only LLM, Encoder-decoder LLMs, Multi-modal LLMs, Instruction-tuned LLMs, Domain-specific LLMs.
에이전트 AI와 관련이 된 것은 마지막 두 개인 (Instruction-tuned LLMs, Domain-specific LLMs)로 보인다.

비행기 예약 시스템으로 간단한 예제를 보여준다. 이 책 전체를 통해 계속 사용되는 예제이다.

Generative AI가 사용되는 여러 분야에 대한 설명이 나온다.
이미지/영상/텍스트/코드 Generation과 상관관계 예측를 통한 의료분야, 독자판단 가능한 에이전트로 정리될 수 있겠다.

도전과제와 한계는 데이터 어떻게 관리할 것인가에 대한 점, 데이터의 Privacy를 관리하는 것, 거대한 컴퓨팅 자원을 어떻게 지원할 것인가에 대한 점이 나와 있다.

윤리적/사회적 함의는 딥페이크와 잘못된 정보의 유통, 지적 재산권/데이터의 소유권 문제, 실업의 문제등을 나열하고 있다.
개인적으로는 권력의 집중과 권력의 형체는 형해화되고 힘은 내재화되는 것도 커다란 문제라 생각된다. 
