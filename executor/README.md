# 실행기 디렉토리

이 디렉토리는 실시간 거래 실행과 관련된 파일들을 포함합니다.

## 파일

- `binance_executor.py`: 바이낸스 API 연동 및 주문 실행 모듈
- `telegram_notifier.py`: 텔레그램 알림 모듈
- `live_trader.py`: 실시간 거래 실행 모듈
- `execution_optimizer.py`: 주문 실행 최적화 모듈
- `slippage_model.py`: 슬리피지 예측 모델

## 주요 클래스

### BinanceExecutor

바이낸스 API를 통한 주문 실행 및 계좌 정보 조회 기능 제공:

- REST API 통신
- 시장가/지정가 주문 실행
- 손절/익절 설정
- 계좌 정보 조회
- 오류 처리 및 재시도 로직

### TelegramNotifier

텔레그램을 통한 알림 전송 기능 제공:

- 거래 알림 (진입, 청산)
- 오류 알림
- 성능 상태 보고

### LiveTrader

학습된 모델을 사용한 실시간 거래 실행:

- 데이터 수집 스레드
- 추론 및 주문 실행 스레드
- 상태 보고 스레드

## 사용 예시

```python
from executor.binance_executor import BinanceExecutor
from executor.telegram_notifier import TelegramNotifier
from executor.live_trader import LiveTrader

# 바이낸스 실행기
executor = BinanceExecutor('config.yaml')

# 텔레그램 알림
notifier = TelegramNotifier('config.yaml')

# 실시간 거래
trader = LiveTrader('models/ppo_trader.pt', 'config.yaml')
trader.run()
```

## 주의 사항

- 실제 자금을 사용하기 전에 테스트넷 환경에서 충분히 테스트하세요.
- API 키와 시크릿은 안전하게 보관하고, 필요한 권한만 부여하세요.
- 시스템 안정성을 위해 오류 처리 및 로깅을 철저히 하세요.