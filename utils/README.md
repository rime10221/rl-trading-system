# 유틸리티 디렉토리

이 디렉토리는 시스템 전반에서 사용되는 유틸리티 모듈을 포함합니다.

## 파일

- `feature_engineering.py`: 기술적 지표 및 특성 추출 모듈

## 주요 함수 및 클래스

### FeatureEngineering

데이터에서 기술적 지표 및 특성을 추출하는 클래스:

```python
class FeatureEngineering:
    """기술적 지표 및 특성 추출 클래스"""
    
    def __init__(self, config):
        """
        Args:
            config: 특성 엔지니어링 설정
        """
        self.config = config
    
    def add_technical_indicators(self, df):
        """
        데이터프레임에 기술적 지표 추가
        
        Args:
            df: 원본 데이터프레임 (OHLCV 포함)
            
        Returns:
            지표가 추가된 데이터프레임
        """
        # 구현 생략
        
    def normalize_features(self, df, method='zscore'):
        """
        특성 정규화
        
        Args:
            df: 원본 데이터프레임
            method: 정규화 방법 ('zscore', 'minmax', 'robust')
            
        Returns:
            정규화된 데이터프레임
        """
        # 구현 생략
```

## 지원하는 기술적 지표

- 이동평균 (SMA, EMA, WMA)
- 상대강도지수 (RSI)
- 볼린저 밴드 (Bollinger Bands)
- MACD (Moving Average Convergence Divergence)
- ATR (Average True Range)
- 스토캐스틱 오실레이터 (Stochastic Oscillator)
- OBV (On-Balance Volume)
- 피보나치 리트레이스먼트 (Fibonacci Retracement)

## 지원하는 정규화 방법

- Z-점수 정규화 (Z-score Normalization)
- 최소-최대 정규화 (Min-Max Normalization)
- 로버스트 스케일링 (Robust Scaling)
- 변화율 기반 정규화 (Percentage Change)

## 사용 예시

```python
import pandas as pd
from utils.feature_engineering import FeatureEngineering

# 설정
config = {
    'technical_indicators': [
        'sma_7', 'sma_25', 'rsi_14', 'bb_20_2', 'macd_12_26_9'
    ]
}

# 특성 엔지니어링 인스턴스 생성
fe = FeatureEngineering(config)

# 데이터 로드
df = pd.read_csv('data/btcusdt_1m_2022.csv')

# 기술적 지표 추가
df_with_indicators = fe.add_technical_indicators(df)

# 특성 정규화
normalized_df = fe.normalize_features(df_with_indicators, method='zscore')
```

## 주의 사항

- 정규화 시 데이터 누수(data leakage)를 방지하기 위해 시간 순서를 고려하세요.
- 결측치가 생길 수 있으므로 처리 방법을 고려하세요 (제거 또는 채우기).
- 계산 집약적인 지표의 경우 성능 최적화를 고려하세요.