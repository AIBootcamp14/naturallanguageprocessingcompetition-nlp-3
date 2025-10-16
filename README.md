
# Dialogue Summarization Project (NLP 경진대회)

## 팀명 : 4Tune

<div align="center">

| <img src="https://avatars.githubusercontent.com/u/66048976?v=4" width="120" style="border-radius:50%;"> | <img src="https://avatars.githubusercontent.com/u/168383346?v=4" width="120" style="border-radius:50%;">  |<img src="https://avatars.githubusercontent.com/u/213417897?v=4" width="120" style="border-radius:50%;">  |
| :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: |
|           [박재홍](https://github.com/woghd8503)           |           [이준영](https://github.com/junyeonglee1111)           |           [김동준](https://github.com/rafiki3816)           |
|                          팀장                           |                            부팀장                            |                            팀원                             |

</div>

---

## 1️⃣ 개발 환경 및 기술 스택  

| 구분 | 내용 |
|------|------|
| **주 언어** | Python 3.10 |
| **핵심 라이브러리** | PyTorch / Transformers / Optuna / Pandas / NumPy / Matplotlib |
| **버전 및 이슈 관리** | GitHub (Branch : main / dev / feature) |
| **협업 툴** | GitHub Projects · Notion · Google Drive · Upstage Playground |
| **실험 도구** | Weights & Biases (W&B) – 모델 로그 및 학습 곡선 시각화 |
| **환경 관리** | requirements.txt 기반 공통 세팅 / Conda 환경 통일 |

---

## 2️⃣ 프로젝트 구조  

```
├── code
│   ├── jupyter_notebooks
│   │   └── model_train.ipynb         # 실험 및 튜닝 노트북
│   └── train.py                      # 모델 학습 스크립트
├── docs
│   ├── pdf
│   │   └── (Template) [패스트캠퍼스] Upstage AI Lab 1기_그룹 스터디 .pptx
│   └── paper                         # 참고 논문/자료
└── input
    └── data
        ├── eval
        └── train
```

---

## 3️⃣ 구현 기능  

### ⚙️ 기능 1 – 모델 학습 및 튜닝  
- **Encoder–Decoder 기반 (BART)** 및 **Decoder-Only 모델 (Solar Pro2)** 비교 적용  
- Optuna 활용 총 20회 하이퍼파라미터 탐색으로 최적 값 도출  
- encoder_max_len = 512 / decoder_max_len = 128 로 Out of Memory 방지  

### ⚙️ 기능 2 – 데이터 전처리 및 EDA  
- 대화 길이 통계 분석 (평균·최대 토큰 수 및 문장 분포 시각화)  
- 불용어 제거 세 수준 테스트 → “불용어가 가장 적을 때 성능 최고” 결론  
- 대화 패턴 및 요약문 길이 분포 기준 최소 요약 길이 설정  

### ⚙️ 기능 3 – RLHF (인간 피드백 기반 강화학습 시도)  
- 요약문 내 인물명 손실 및 날짜 환각 오류 발견 후 직접 피드백으로 수정  
- RLHF 사이클 시각화 (결과 검토 → 수정 → 모델 재학습 → 성능 비교)  
- 실제 피드백을 반영한 요약문 정확도 향상 사례 확인  

---

## 4️⃣ 작품 아키텍처 (선택)  

```
User Input (Dialogue CSV)
        │
        ▼
[ Preprocessing & EDA ]
        │
        ▼
Encoder–Decoder (BART) or Decoder-only (Solar Pro2)
        │
        ▼
Hyperparameter Tuning (Optuna)
        │
        ▼
RLHF Loop (Human Feedback Correction)
        │
        ▼
Summary Output → Evaluation / Leaderboard Submission
```

> 💡 Upstage Playground 활용으로 Prompt 실험 → 성공 설정 코드 이식 → 재현성 및 효율성 확보

---

## 5️⃣ 트러블 슈팅  

### 🧩 문제 1 – Baseline 요약 후반부 정보 누락  
**설명:** 기존 코드 사용 시 요약문 길이가 짧아 핵심 단어 손실 발생  
**해결:** min_length 하이퍼파라미터 설정 및 decoder_max_len 조정으로 정보 보존 개선  

---

### 🧩 문제 2 – Out of Memory (OOM)  
**설명:** encoder/decoder 길이 과다 설정 시 메모리 초과 발생  
**해결:** encoder_max_len = 512, decoder_max_len = 128 로 조합 테스트 → 안정화  

---

### 🧩 문제 3 – 반복 실험 시 속도 저하 및 루프 지연  
**설명:** 매 실험 환경 초기화로 피드백 루프 길어짐  
**해결:** Upstage Playground 도입 → Prompt 단위 검증 속도 10배 단축  

---

## 6️⃣ 프로젝트 회고  

### 🎯 목표 달성도  
- “**한 걸음씩, 그리고 함께**” 슬로건 아래 협업용 베이스라인 구축 성공  
- 모든 팀원이 전 과정 직접 참여 하여 끝까지 결과 도출  

### 🌱 잘한 점  
- 정기 미팅 (10시 5분 / 14시 5분 / 18시) 으로 진행 상황 공유  
- 영어로 감정 점수 공유 등 창의적 커뮤니케이션 시도  
- 가설 기반 실험 로그 체계 확립  

### 🧠 개선 점  
- 파이프라인 통합 시 제어 요인 이해 부족 → 이론 보완 및 통합 관리 체계 구축 필요  

### 💬 느낀 점 (요약)  
> 박재홍 : ‘왜?’라는 질문을 반복하며 문제 본질을 탐구. 작은 변화도 기록의 중요성 깨달음.  
> 이준영 : 향후 스터디 방향성 정립 계기 확보.  
> 김동준 : 변인 통제의 어려움 속에서도 자연어 파이프라인 이해 심화  

---

## 7️⃣ 참고자료  

- Upstage AI Playground Docs  
- FastCampus Kernel Academy 14기 자료  
- Hugging Face Transformers Documentation  
- Optuna Official Guide  
- RLHF Research (“Learning to Summarize from Human Feedback”, Ziegler et al., 2020)

---

## 📌 요약  

> 본 프로젝트는 단순한 요약 모델 개발을 넘어,  
> **“직접 눈으로 결과를 확인하고 수정 피드백을 학습에 반영한 RLHF 적용”** 을 핵심 가치로 삼았습니다.  
> 실험 기록, 협업 문화, 피드백 루프 측면에서 AI 개발 프로세스의 본질을 체험한 의미 있는 경험이었습니다.  
