# 로그 디렉토리

이 디렉토리는 시스템 로그 파일을 저장합니다.

## 로그 종류

- `environment.log`: 강화학습 환경 로그
- `training.log`: 모델 학습 로그
- `backtest.log`: 백테스트 결과 로그
- `live_trader.log`: 실시간 거래 로그
- `binance_executor.log`: 바이낸스 API 연동 로그
- `telegram_notifier.log`: 텔레그램 알림 로그

## 로그 포맷

기본 로그 포맷:
```
2025-06-01 12:30:45 - ModuleName - LogLevel - Message
```

## 로그 레벨

- DEBUG: 디버깅 목적의 상세 정보
- INFO: 일반적인 시스템 작동 정보
- WARNING: 경고 (오류는 아니지만 주의가 필요한 상황)
- ERROR: 오류 (시스템은 계속 작동 가능)
- CRITICAL: 심각한 오류 (시스템 중단 가능성 있음)

## 주의 사항

- 로그 파일은 Git 저장소에 포함되지 않으며, 로컬에서 생성됩니다.
- 로그 파일이 너무 커지지 않도록 주기적으로 정리하는 것이 좋습니다.
- 개인 정보나 API 키가 로그에 포함되지 않도록 주의하세요.