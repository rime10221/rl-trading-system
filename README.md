# 강화학습 기반 암호화폐 트레이딩 시스템

바이낸스 선물/현물 시장에서 강화학습(RL) 모델을 활용한 자동 트레이딩 시스템입니다.

## 주요 기능

- **강화학습 환경**: OpenAI Gym 호환 트레이딩 환경
- **PPO 모델 학습**: stable-baselines3를 활용한 PPO 알고리즘 학습
- **백테스트**: 학습된 모델의 성능 검증
- **실시간 거래**: 바이낸스 API를 통한 실시간 추론 및 주문 실행
- **텔레그램 알림**: 거래 결과 및 시스템 상태 알림

## 시스템 요구 사항

- Python 3.13.3
- stable-baselines3 (PPO 알고리즘)
- torch (PyTorch)
- pandas, numpy, matplotlib 등 데이터 분석 패키지
- python-telegram-bot (텔레그램 알림용)
- binance-python (바이낸스 API 연동용)

## 폴더 구조

```
project_root/
├── data/             # 과거 가격 데이터 저장
├── models/           # 학습된 정책 모델 (.pt)
├── strategies/       # 룰/AI 기반 전략 모듈
├── executor/         # 실시간 매매 실행기
│   ├── binance_executor.py    # 바이낸스 API 연동
│   ├── telegram_notifier.py   # 텔레그램 알림
│   └── live_trader.py         # 실시간 거래 실행기
├── logs/             # 주문 기록 및 에러 로그
├── envs/             # 강화학습 환경 정의
│   └── custom_env.py          # 트레이딩 환경
├── train_rl.py       # PPO 모델 학습 스크립트
├── backtest.py       # 백테스트 스크립트
├── config.yaml       # API Key, 텔레그램 설정, 학습 파라미터 등
└── run.py            # 메인 실행 스크립트
```

## 설치 방법

1. 저장소 클론

```bash
git clone https://github.com/rime10221/rl-trading-system.git
cd rl-trading-system
```

2. 가상환경 생성 및 활성화

```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

3. 의존성 설치

```bash
pip install -r requirements.txt
```

4. 설정 파일 수정

`config.yaml` 파일을 열고 다음 항목 설정:
- 바이낸스 API 키/시크릿
- 텔레그램 봇 토큰/채팅 ID
- 트레이딩 설정 (심볼, 레버리지 등)
- 강화학습 파라미터

## 사용 방법

### 1. 모델 학습

```bash
python run.py --mode train --data data/btcusdt_1m_2022.csv --model ppo_trader
```

### 2. 백테스트 실행

```bash
python run.py --mode backtest --model ppo_trader --data data/btcusdt_1m_2023.csv
```

### 3. 실시간 거래 시작

```bash
python run.py --mode live --model ppo_trader
```

### 4. 데이터 수집 (개발 예정)

```bash
python run.py --mode data --symbol BTCUSDT --timeframe 1m
```

## 환경 정의

강화학습 환경은 다음과 같이 정의됩니다:

- **상태 (Observation)**:
  - 과거 N틱의 OHLCV, 이동평균, 볼린저 밴드, RSI, 포지션 상태 등

- **행동 (Action)**:
  - [0]: 보유
  - [1]: 전액 매수 (롱)
  - [2]: 전액 매도 (숏)

- **보상 (Reward)**:
  - (현재 수익률) - (MDD 패널티) - (거래 수수료)
  - 손절/익절 발생 시 보상 조정

## 텔레그램 알림

다음과 같은 경우에 텔레그램 알림이 발송됩니다:

- 실시간 매수/매도 시 알림
- 포지션 종료(익절/손절) 시 수익률 포함 알림
- 예외/오류 발생 시 에러 메시지 전달

알림 예시:
- ✅ [매수] BTCUSDT 1.25개 @ $32,110
- ❌ [손절] BTCUSDT -2.3% @ $31,430
- ⚠️ [에러] 주문 실패: insufficient margin

## 주의 사항

- 실제 자금을 사용하기 전에 충분한 백테스트와 테스트넷 환경에서의 검증을 거치세요.
- 암호화폐 거래는 높은 변동성을 수반하며 원금 손실 위험이 있습니다.
- API 키와 시크릿은 안전하게 보관하고, 필요한 권한만 부여하세요.

## 라이선스

MIT

## 기여하기

이슈 및 풀 리퀘스트는 언제나 환영합니다. 대규모 변경 사항의 경우, 먼저 이슈를 열어 논의해 주세요.