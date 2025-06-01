# 전략 디렉토리

이 디렉토리는 다양한 트레이딩 전략 및 보조 모듈을 포함합니다.

## 파일

- `hybrid_strategy.py`: 강화학습과 규칙 기반 전략을 결합한 하이브리드 전략
- `kelly_calculator.py`: 켈리 기준을 활용한 최적 포지션 크기 계산기
- `market_regime.py`: 시장 레짐 분류 및 감지 모듈
- `risk_manager.py`: 위험 관리 모듈

## 주요 클래스

### HybridStrategy

강화학습 모델과 규칙 기반 전략을 결합한 하이브리드 전략:

- 시장 상황에 따라 강화학습 또는 규칙 기반 전략 선택
- 모델 신뢰도에 따른 가중치 조정
- 전략 간 충돌 해결 로직

### KellyCalculator

켈리 기준을 활용한 최적 포지션 크기 계산:

- 승률과 손익비를 고려한 최적 포지션 계산
- 분수 켈리 적용 (보수적 접근)
- 역사적 성과 기반 켈리 계수 추정

### MarketRegime

시장 레짐 분류 및 감지:

- 추세형 (상승/하락)
- 횡보형
- 고변동성/저변동성
- 레짐별 최적 전략 추천

### RiskManager

위험 관리 모듈:

- 최대 허용 가능 손실 계산
- 포트폴리오 수준 위험 관리
- 레버리지 조정
- 손절/익절 최적화

## 사용 예시

```python
from strategies.market_regime import MarketRegime
from strategies.risk_manager import RiskManager
from strategies.kelly_calculator import KellyCalculator

# 시장 레짐 감지
market_regime = MarketRegime()
current_regime = market_regime.detect(data)

# 위험 관리
risk_manager = RiskManager(initial_balance=1000)
max_position_size = risk_manager.calculate_position_size(current_regime)

# 켈리 계산
kelly = KellyCalculator(win_rate=0.55, profit_loss_ratio=1.5)
optimal_size = kelly.calculate(max_position_size, fraction=0.5)
```

## 커스터마이징

새로운 전략을 추가할 때는 다음 인터페이스를 준수하세요:

- `predict(observation)`: 상태 관측값을 받아 액션 반환
- `update(observation, action, reward, next_observation, done)`: 학습/업데이트