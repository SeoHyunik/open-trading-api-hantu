# KOSPI / KOSDAQ 실시간 지수 API 사용법

## 개요

이 문서는 `open-trading-api-hantu` 프로젝트에서 KOSPI(코스피) 및 KOSDAQ(코스닥) 실시간 지수 데이터를 추출하는 방법을 설명합니다.

관련 함수는 별도의 `domestic_index` 폴더 없이 **`domestic_stock`** 카테고리 아래에 위치합니다.

- REST API 함수: `examples_user/domestic_stock/domestic_stock_functions.py`
- WebSocket 함수: `examples_user/domestic_stock/domestic_stock_functions_ws.py`
- WebSocket 사용 예시: `examples_user/domestic_stock/domestic_stock_examples_ws.py`

---

## 지수 코드 (fid_input_iscd)

| 코드 | 설명 |
|------|------|
| `0001` | KOSPI (코스피 종합) |
| `1001` | KOSDAQ (코스닥 종합) |
| `2001` | KOSPI 200 |
| `3003` | KSQ150 (코스닥 150) |

업종 세부 코드는 KIS 포탈 FAQ (종목정보 다운로드 > 업종코드) 를 참조하십시오.

시장 구분 코드(`fid_cond_mrkt_div_code`)는 업종 조회 시 **`"U"`** 를 사용합니다.

---

## REST API 함수 목록

### 1. `inquire_index_price` — 현재지수 조회

**API ID**: `FHPUP02100000`  
**엔드포인트**: `/uapi/domestic-stock/v1/quotations/inquire-index-price`

현재 시점의 지수 값(현재가, 전일대비, 등락률 등)을 조회합니다.

```python
from examples_user.domestic_stock.domestic_stock_functions import inquire_index_price

# KOSPI 현재지수 조회
df = inquire_index_price(
    fid_cond_mrkt_div_code="U",
    fid_input_iscd="0001"  # KOSPI
)
print(df)

# KOSDAQ 현재지수 조회
df = inquire_index_price(
    fid_cond_mrkt_div_code="U",
    fid_input_iscd="1001"  # KOSDAQ
)
print(df)
```

**파라미터**

| 파라미터 | 타입 | 필수 | 설명 |
|----------|------|------|------|
| `fid_cond_mrkt_div_code` | str | O | 업종 시장 구분 코드 (`"U"` 고정) |
| `fid_input_iscd` | str | O | 지수 코드 (예: `"0001"`, `"1001"`) |

**반환**: `pd.DataFrame` — 지수 현재가, 전일대비, 거래량, 등락률 등

---

### 2. `inquire_index_tickprice` — 시간별지수(초 단위)

**API ID**: `FHPUP02110100`  
**엔드포인트**: `/uapi/domestic-stock/v1/quotations/inquire-index-tickprice`

초 단위 틱 데이터로 지수 흐름을 조회합니다.

```python
from examples_user.domestic_stock.domestic_stock_functions import inquire_index_tickprice

df = inquire_index_tickprice(
    fid_input_iscd="0001",           # KOSPI
    fid_cond_mrkt_div_code="U"
)
print(df)
```

**파라미터**

| 파라미터 | 타입 | 필수 | 설명 |
|----------|------|------|------|
| `fid_input_iscd` | str | O | 지수 코드 (`0001`, `1001`, `2001`, `3003`) |
| `fid_cond_mrkt_div_code` | str | O | 시장 구분 코드 (`"U"` 고정) |

**반환**: `pd.DataFrame` — 틱별 지수 데이터

---

### 3. `inquire_index_timeprice` — 시간별지수(분 단위)

**API ID**: `FHPUP02110200`  
**엔드포인트**: `/uapi/domestic-stock/v1/quotations/inquire-index-timeprice`

분 단위 인터벌로 지수 흐름을 조회합니다.

```python
from examples_user.domestic_stock.domestic_stock_functions import inquire_index_timeprice

# KOSPI 1분봉 지수
df = inquire_index_timeprice(
    fid_input_hour_1="60",           # 60초 = 1분
    fid_input_iscd="0001",           # KOSPI
    fid_cond_mrkt_div_code="U"
)
print(df)

# KOSDAQ 5분봉 지수
df = inquire_index_timeprice(
    fid_input_hour_1="300",          # 300초 = 5분
    fid_input_iscd="1001",           # KOSDAQ
    fid_cond_mrkt_div_code="U"
)
print(df)
```

**파라미터**

| 파라미터 | 타입 | 필수 | 설명 |
|----------|------|------|------|
| `fid_input_hour_1` | str | O | 인터벌(초 단위): `"60"` (1분), `"300"` (5분), `"600"` (10분) |
| `fid_input_iscd` | str | O | 지수 코드 |
| `fid_cond_mrkt_div_code` | str | O | 시장 구분 코드 (`"U"` 고정) |

**반환**: `pd.DataFrame` — 인터벌별 지수 데이터

---

### 4. `inquire_index_daily_price` — 일자별지수

**API ID**: `FHPUP02120000`  
**엔드포인트**: `/uapi/domestic-stock/v1/quotations/inquire-index-daily-price`

일/주/월 단위 과거 지수 데이터를 조회합니다.

```python
from examples_user.domestic_stock.domestic_stock_functions import inquire_index_daily_price

df1, df2 = inquire_index_daily_price(
    fid_period_div_code="D",         # D: 일별, W: 주별, M: 월별
    fid_cond_mrkt_div_code="U",
    fid_input_iscd="0001",           # KOSPI
    fid_input_date_1="20240223"      # 기준일 (YYYYMMDD)
)
print(df1)  # 지수 헤더 정보
print(df2)  # 일별 지수 목록
```

**파라미터**

| 파라미터 | 타입 | 필수 | 설명 |
|----------|------|------|------|
| `fid_period_div_code` | str | O | 기간 구분: `"D"` (일), `"W"` (주), `"M"` (월) |
| `fid_cond_mrkt_div_code` | str | O | 시장 구분 코드 (`"U"` 고정) |
| `fid_input_iscd` | str | O | 지수 코드 |
| `fid_input_date_1` | str | O | 기준일 (YYYYMMDD 형식) |

**반환**: `Tuple[pd.DataFrame, pd.DataFrame]` — (지수 헤더, 기간별 지수 목록)

---

### 5. `inquire_index_category_price` — 업종 구분별 전체시세

**API ID**: `FHPUP02140000`  
**엔드포인트**: `/uapi/domestic-stock/v1/quotations/inquire-index-category-price`

KOSPI 또는 KOSDAQ 내 세부 업종 구분별 전체 시세를 조회합니다.

```python
from examples_user.domestic_stock.domestic_stock_functions import inquire_index_category_price

df1, df2 = inquire_index_category_price(
    fid_cond_mrkt_div_code="U",
    fid_input_iscd="0001",           # KOSPI
    fid_cond_scr_div_code="20214",   # Unique key (고정값)
    fid_mrkt_cls_code="K",           # K: 거래소, Q: 코스닥, K2: 코스피200
    fid_blng_cls_code="0"            # 0: 전업종
)
print(df1)
print(df2)
```

---

## WebSocket 실시간 구독 함수

WebSocket 기반 함수는 `examples_user/domestic_stock/domestic_stock_functions_ws.py` 에 있으며, `kws.subscribe()` 로 호출합니다.

### 공통 사용 구조

```python
import kis_auth as ka
from examples_user.kis_auth import KisAuth
from examples_user.domestic_stock.domestic_stock_functions_ws import (
    index_ccnl,
    index_exp_ccnl,
    index_program_trade,
)

# WebSocket 클라이언트 초기화 (기존 인증 객체 사용)
kws = ka.get_ws_client()

# 구독 등록 후 메시지 수신 루프 실행
kws.subscribe(request=index_ccnl, data=["0001", "1001"])
kws.run_forever()
```

---

### 6. `index_ccnl` — 국내지수 실시간체결 [실시간-026]

**TR ID**: `H0UPCNT0`

실시간 지수 체결 데이터를 WebSocket으로 구독합니다.

```python
# KOSPI(0001), KOSDAQ(1001) 동시 구독
kws.subscribe(request=index_ccnl, data=["0001", "1001"])
```

**파라미터**

| 파라미터 | 타입 | 설명 |
|----------|------|------|
| `tr_type` | str | `"1"`: 구독 등록, `"0"`: 구독 해제 |
| `tr_key` | str | 지수 코드 (예: `"0001"`) |

**반환 컬럼 (주요)**

| 컬럼 | 설명 |
|------|------|
| `bsop_hour` | 영업 시간 |
| `prpr_nmix` | 현재 지수 |
| `prdy_vrss_sign` | 전일 대비 부호 |
| `bstp_nmix_prdy_vrss` | 전일 대비 지수 |
| `prdy_ctrt` | 전일 대비율 |
| `acml_vol` | 누적 거래량 |
| `acml_tr_pbmn` | 누적 거래대금 |
| `nmix_hgpr` | 지수 최고가 |
| `nmix_lwpr` | 지수 최저가 |

---

### 7. `index_exp_ccnl` — 국내지수 실시간예상체결 [실시간-027]

**TR ID**: `H0UPANC0`

장 시작 전 예상 체결 지수를 WebSocket으로 구독합니다.

```python
# KOSPI 예상체결지수 구독
kws.subscribe(request=index_exp_ccnl, data=["0001"])
```

**파라미터 및 반환 구조는 `index_ccnl`과 동일**

---

### 8. `index_program_trade` — 국내지수 실시간프로그램매매 [실시간-028]

KOSPI/KOSDAQ 프로그램 매매 데이터를 WebSocket으로 구독합니다.

```python
kws.subscribe(request=index_program_trade, data=["0001", "1001"])
```

---

## 함수 위치 요약

| 함수명 | 유형 | 파일 |
|--------|------|------|
| `inquire_index_price` | REST | `examples_user/domestic_stock/domestic_stock_functions.py` |
| `inquire_index_tickprice` | REST | `examples_user/domestic_stock/domestic_stock_functions.py` |
| `inquire_index_timeprice` | REST | `examples_user/domestic_stock/domestic_stock_functions.py` |
| `inquire_index_daily_price` | REST | `examples_user/domestic_stock/domestic_stock_functions.py` |
| `inquire_index_category_price` | REST | `examples_user/domestic_stock/domestic_stock_functions.py` |
| `inquire_daily_indexchartprice` | REST | `examples_user/domestic_stock/domestic_stock_functions.py` |
| `inquire_time_indexchartprice` | REST | `examples_user/domestic_stock/domestic_stock_functions.py` |
| `index_ccnl` | WebSocket | `examples_user/domestic_stock/domestic_stock_functions_ws.py` |
| `index_exp_ccnl` | WebSocket | `examples_user/domestic_stock/domestic_stock_functions_ws.py` |
| `index_program_trade` | WebSocket | `examples_user/domestic_stock/domestic_stock_functions_ws.py` |

`examples_llm/domestic_stock/` 아래에도 함수별 독립 모듈(`index_ccnl/`, `inquire_index_price/` 등)이 구성되어 있으며, LLM 에이전트 호출용으로 사용됩니다.

---

## 참고

- 별도의 `domestic_index` 폴더는 존재하지 않습니다. 모든 지수 관련 함수는 `domestic_stock` 카테고리 내에 있습니다.
- 실시간 WebSocket 구독을 위해서는 사전에 웹소켓 접속키(approval_key) 발급이 필요합니다. `examples_user/auth/` 또는 `examples_llm/auth/auth_ws_token/` 참조.
- 이 문서는 소스 탐색 기준 2026-04-09 작성되었습니다.
