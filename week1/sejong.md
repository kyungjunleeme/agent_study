# VAE (Variational Autoencoder) 완전 정리

## 📌 VAE란 무엇인가?

**VAE는 생성 모델의 일종**으로, 인코딩된 데이터를 쉬운 확률 분포(가우시안)에서 샘플링 가능하도록 노이즈를 섞어 학습함으로써 새로운 데이터를 생성하는 모델입니다.

### 일반 오토인코더 vs VAE

| 구분 | 일반 오토인코더 | VAE |
|------|----------------|-----|
| 목적 | 학습 데이터 복원 | 새로운 데이터 생성 |
| 인코딩 | 결정적(deterministic) | 확률적(stochastic) |
| 노이즈 | 없음 | 인코딩 과정에 노이즈 추가 |
| 샘플링 | 불가능 | 가능 |

---

## 1. 인코더(Encoder)의 기본 원리

### 인코딩이란?

데이터를 **더 적은 개수의 숫자로 압축하여 표현**하는 과정

### 예시 1: 버튼 정보 인코딩

```
원본: 0~9번 버튼 중 하나가 눌림 (10가지 경우)
인코딩: 4개의 비트(0000~1001)로 표현
압축률: 10개 정보 → 4개 비트
```

### 예시 2: 이미지 인코딩

```
원본: 32×32 RGB 이미지
     = 32 × 32 × 3 = 3,072개 숫자

인코딩: 512개 숫자로 압축
압축률: 3,072 → 512 (약 1/6)
```

### 인코더의 핵심 특성

#### 1) 가정의 필요성

- 더 적은 정보로 인코딩하려면 **데이터의 규칙성(패턴)에 대한 가정**이 필요
- 예: 고양이 이미지의 경우
  - 겉부분 픽셀의 RGB 차이가 0.1 이하
  - 특정 형태의 귀, 눈, 수염 패턴 존재
  - 이런 가정들이 있어야 압축 가능

#### 2) 여러 인코딩 방식 존재

- 인코딩 공식은 하나가 아님
- 같은 데이터를 다양한 방식으로 압축 가능

### 디코딩(Decoding)

- 인코딩된 정보를 **원본 데이터로 복원**하는 과정
- 인코딩이 의미를 갖기 위해서는 디코딩이 가능해야 함

---

## 2. 오토인코더(Autoencoder)의 이해

### '오토(Auto)'의 의미

**데이터의 규칙을 자동으로 찾아 인코딩/디코딩 공식을 학습**

### 수동 인코딩 설계의 문제점

#### 2차원 데이터 예시

```python
# 수동 설계 과정
1. 데이터를 2D 좌표에 시각화
2. 선형 패턴 발견
3. 사인 함수로 영역 분리
4. X 좌표만 저장하도록 변환
5. 복원 시 2차 함수 사용
```

#### 한계점

1. **복잡하고 귀찮음**
   - 2차원도 어려운데 3,072차원은 사실상 불가능
   - 목표가 바뀔 때마다 규칙을 새로 설계해야 함

2. **가정 오류로 인한 정확도 저하**
   - 2차 함수 가정이 틀리면 복원 오차 발생

### 오토인코더의 구조

```
입력(Input)
    ↓
인코더(Encoder) → 압축된 표현(Latent Space) → 디코더(Decoder)
                       [차원 축소]
    ↓
출력(Output)
```

### 학습 목표

**입력 = 출력**이 되도록 학습

```python
Loss = ||Input - Output||²
```

### 학습 과정

1. **중간층의 차원을 입력보다 작게 설정**
   - 예: 3,072 → 512 → 3,072

2. **모델이 자동으로 학습**
   - 데이터의 가정/규칙을 찾아냄
   - 경우의 수를 줄일 수 있는 방법 발견
   - 최적의 인코딩/디코딩 공식 학습

---

## 3. 오토인코더의 한계: 생성 모델로의 부적합성

### 생성 모델의 조건

**확률 분포에서 샘플링하여 새로운 데이터 생성**

### 오토인코더의 문제

1. **인코딩된 분포를 모름**
   - 인코딩된 숫자들이 어떤 규칙을 갖는지 알 수 없음
   - 샘플링하기 쉬운 확률 분포가 아님

2. **강제 집중 시도**
   ```python
   # 인코딩 값을 0 근처로 모으려는 시도
   Loss = ||Input - Output||² + λ * mean(z²)
   ```
   - z: 인코딩된 값
   - 하지만 여전히 샘플링이 잘 안 됨

3. **근본적인 문제**
   - 학습 과정에 **확률적 샘플링이 없음**
   - 데이터셋의 인코딩 값만 복원하도록 학습됨
   - 샘플링된 새로운 값에 대해서는 제대로 생성하지 못함

---

## 4. VAE: Variation 기법의 도입

### 핵심 아이디어: 노이즈 주입(Noise Injection)

**인코딩 과정에 노이즈를 섞어서 디코더에 입력**

### VAE의 학습 과정

```python
# 기존 오토인코더
z = Encoder(x)
x_reconstructed = Decoder(z)

# VAE
μ, σ = Encoder(x)  # 평균과 표준편차 출력
ε ~ N(0, 1)        # 표준정규분포에서 샘플링
z = μ + σ * ε      # 노이즈를 섞은 인코딩
x_reconstructed = Decoder(z)
```

### Variation의 효과

#### 학습 단계

- **정확한 인코딩 값뿐만 아니라 그 근처 값들도 복원 가능하도록 학습**
- 인코딩 값 주변의 범위를 허용

```
학습 전: 정확히 z₁일 때만 고양이 생성
학습 후: z₁ ± ε 범위 내에서 모두 고양이 생성
```

#### 샘플링 단계

```python
# 새로운 데이터 생성
z_new ~ N(0, 1)  # 표준정규분포에서 샘플링
x_new = Decoder(z_new)  # 디코더로 생성
```

### VAE의 손실 함수

```python
Loss = Reconstruction_Loss + KL_Divergence

# 상세
Loss = ||x - x_reconstructed||² + KL(q(z|x) || p(z))
```

- **Reconstruction Loss**: 복원 오차
- **KL Divergence**: 인코딩 분포를 표준정규분포에 가깝게 만듦

---

## 5. VAE 작동 원리 요약

### 전체 프로세스

```
[학습 단계]
1. 입력 이미지 x
2. 인코더 → 평균 μ, 표준편차 σ
3. 샘플링: z = μ + σ * ε (ε ~ N(0,1))
4. 디코더 → 복원된 이미지 x'
5. Loss 계산 및 역전파

[생성 단계]
1. z ~ N(0,1)에서 랜덤 샘플링
2. 디코더에 입력
3. 새로운 이미지 생성
```

### 핵심 알고리즘

```python
class VAE:
    def encode(self, x):
        # 평균과 로그 분산 출력
        mu, log_var = self.encoder(x)
        return mu, log_var
    
    def reparameterize(self, mu, log_var):
        # Reparameterization Trick
        std = exp(0.5 * log_var)
        eps = randn_like(std)  # N(0,1)
        return mu + eps * std
    
    def decode(self, z):
        return self.decoder(z)
    
    def forward(self, x):
        mu, log_var = self.encode(x)
        z = self.reparameterize(mu, log_var)
        return self.decode(z), mu, log_var
    
    def loss_function(self, x, x_recon, mu, log_var):
        # Reconstruction loss
        recon_loss = MSE(x, x_recon)
        
        # KL divergence
        kl_loss = -0.5 * sum(1 + log_var - mu² - exp(log_var))
        
        return recon_loss + kl_loss
```

---

## 6. 핵심 개념 정리

### VAE의 3가지 핵심 요소

1. **인코더가 분포의 파라미터(μ, σ) 출력**
   - 단일 값이 아닌 확률 분포

2. **Reparameterization Trick**
   - 역전파 가능하게 만드는 핵심 기법
   - z = μ + σ * ε (ε는 상수 취급)

3. **KL Divergence 제약**
   - 인코딩 분포를 표준정규분포에 가깝게 유지
   - 샘플링 가능한 분포로 만듦

### 왜 생성 모델인가?

- **표준정규분포에서 샘플링 가능**
- 샘플링된 값이 학습된 범위 내에 있음
- 디코더가 이를 의미있는 데이터로 변환

---

## 7. 주의사항

### 수학적 정확성

이 설명은 **직관적 이해를 위한 단순화된 버전**입니다.

정확한 이해를 위해서는:
- VAE 원논문 참고 (Kingma & Welling, 2013)
- KL Divergence의 수학적 유도
- ELBO(Evidence Lower Bound) 개념
- 전문가의 자세한 설명

### VAE의 한계

1. 생성 이미지가 흐릿한 경향
2. GAN 대비 선명도 낮음
3. 복잡한 분포 모델링의 어려움

### 발전 방향

- β-VAE: KL 가중치 조절
- Conditional VAE: 조건부 생성
- VQ-VAE: 이산적 잠재 공간
- Diffusion Models: VAE의 아이디어 발전

---

## 참고 문헌

- Kingma, D. P., & Welling, M. (2013). Auto-Encoding Variational Bayes
- Doersch, C. (2016). Tutorial on Variational Autoencoders

---

**생성일**: 2025-11-06  
**주제**: Deep Learning - Generative Models - VAE
