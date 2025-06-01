# 환경 디렉토리

이 디렉토리는 강화학습 환경 구현 파일을 포함합니다.

## 파일

- `custom_env.py`: OpenAI Gym 호환 트레이딩 환경 구현

## 주요 클래스

### TradingEnv

`TradingEnv`는 암호화폐 트레이딩을 위한 강화학습 환경을 제공합니다:

- OpenAI Gym 인터페이스 준수
- OHLCV 데이터와 기술적 지표 기반 상태 공간
- 매수/매도/홀딩 액션 지원 (이산형 또는 연속형)
- 수익률 기반 보상 함수 (MDD 패널티 및 수수료 포함)
- 손절/익절 기능 구현

## 주요 메서드

- `reset()`: 환경을 초기 상태로 리셋
- `step(action)`: 환경에서 한 스텝 진행
- `render()`: 환경 시각화
- `get_performance_metrics()`: 성능 지표 반환

## 사용 예시

```python
from envs.custom_env import TradingEnv
import pandas as pd

# 데이터 로드
df = pd.read_csv('data/btcusdt_1m_2022.csv')

# 환경 생성
env = TradingEnv(
    df=df,
    lookback_window=60,
    initial_balance=1000.0,
    commission_fee=0.0004,
    leverage=5.0
)

# 환경 리셋
obs = env.reset()

# 액션 실행
action = 1  # 매수
next_obs, reward, done, info = env.step(action)
```

## 커스터마이징

새로운 환경을 추가하거나 기존 환경을 수정할 때는 OpenAI Gym의 인터페이스를 준수해야 합니다.