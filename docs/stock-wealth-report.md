# 이 프로젝트로 체계적인 주식 투자를 시작하는 방법

> **이 문서는 투자 권유가 아닙니다.**
> 주식 투자에는 원금 손실 위험이 있습니다.
> 이 프로젝트의 도구들은 전략 설계·검증·자동화를 돕는 기술 도구이며, 수익을 보장하지 않습니다.
> 실전 투자 전에 반드시 모의투자로 충분히 검증하세요.

---

## 1. 이 프로젝트가 제공하는 것

`open-trading-api-hantu`는 한국투자증권 KIS Open API를 기반으로
**전략 설계 → 과거 검증 → 시그널 생성 → 실전/모의 주문**까지의
퀀트 투자 전체 워크플로우를 하나의 저장소에서 지원합니다.

```
전략 설계         과거 검증          실전 적용
Strategy Builder ──▶ Backtester ──▶ Strategy Builder
(비주얼 빌더)       (Lean 엔진)       (시그널 + 주문)
    ▲                  │
    └──────────────────┘
      (검증 완료 전략 재사용)
```

구성 요소:

| 구성요소 | 위치 | 역할 |
|---------|------|------|
| KIS Open API 예제 | `examples_llm/`, `examples_user/` | API 직접 호출 예제 |
| Strategy Builder | `strategy_builder/` | 비주얼 전략 설계 + 실시간 주문 |
| Backtester | `backtester/` | 과거 데이터 기반 전략 검증 |
| KIS Code Assistant MCP | `MCP/KIS Code Assistant MCP/` | AI 에이전트용 API 검색 도구 |
| KIS Trading MCP | `MCP/Kis Trading MCP/` | AI 에이전트용 거래 실행 도구 |
| stocks_info | `stocks_info/` | 종목 마스터 데이터 (KOSPI, KOSDAQ, ETF 등) |

---

## 2. 사전 준비

### 2.1 계좌 및 API 키 발급

1. 한국투자증권 계좌 개설 (증권 계좌)
2. [KIS Developers 포털](https://apiportal.koreainvestment.com/)에서 Open API 서비스 신청
3. **모의투자용 앱키 + 실전투자용 앱키** 각각 발급
4. `~/KIS/config/kis_devlp.yaml` 파일에 키 입력

```yaml
# 실전투자
my_app: "실전투자 앱키"
my_sec: "실전투자 앱시크릿"

# 모의투자
paper_app: "모의투자 앱키"
paper_sec: "모의투자 앱시크릿"

my_htsid: "HTS ID"
my_acct_stock: "증권계좌 앞 8자리"
my_paper_stock: "모의투자 계좌 앞 8자리"
my_prod: "01"
```

### 2.2 환경 요구사항

| 도구 | 버전 | 용도 |
|------|------|------|
| Python | 3.11+ | 백엔드 |
| Node.js | 18+ | 프론트엔드 |
| Docker Desktop | 최신 | Backtester Lean 엔진 |
| uv | 최신 | Python 패키지 관리 |

---

## 3. 워크플로우: 단계별 사용법

### 3단계 핵심 흐름

```
[1단계] 전략 설계     [2단계] 백테스트      [3단계] 실전 적용
Strategy Builder ──▶ Backtester ──▶ Strategy Builder
http://localhost:3000  http://localhost:3001   http://localhost:3000
```

---

### 3.1 Strategy Builder — 전략 설계

**시작**

```bash
cd strategy_builder
./start.sh
# 브라우저: http://localhost:3000
```

**사용 방법**

1. `/builder` 페이지에서 10개 프리셋 전략 중 하나를 불러오거나 새 전략을 만듭니다.
2. 80개 기술지표 중 원하는 지표를 조합합니다.
3. 진입 조건, 청산 조건, 손절/익절 비율을 설정합니다.
4. 설계한 전략을 `.kis.yaml` 파일로 Export합니다.

**제공되는 10개 프리셋 전략**

| 전략 | 카테고리 | 설명 |
|------|---------|------|
| 골든크로스 | 추세추종 | 단기 MA가 장기 MA를 상향 돌파 시 매수 |
| 모멘텀 | 추세추종 | N일 수익률 기준 매매 |
| 추세 필터 | 추세추종 | MA 위/아래 추세 방향 기준 매매 |
| 52주 신고가 | 돌파매매 | 52주 최고가 갱신 시 매수 |
| 연속 상승/하락 | 추세추종 | N일 연속 패턴 감지 |
| 이격도 | 역추세 | MA 대비 이격도 기반 매매 |
| 돌파 실패 | 손절 | 전고점 돌파 실패 시 매도 |
| 강한 종가 | 모멘텀 | 고가 대비 종가 강도 기준 매수 |
| 변동성 확장 | 돌파매매 | 변동성 최저 후 돌파 시 매수 |
| 평균회귀 | 역추세 | MA 대비 이탈 시 반대 매매 |

---

### 3.2 Backtester — 전략 검증

**시작**

```bash
cd backtester
./start.sh
# 브라우저: http://localhost:3001
```

> Docker Desktop이 실행 중이어야 합니다.

**사용 방법**

1. Strategy Builder에서 Export한 `.kis.yaml` 파일을 드래그 앤 드롭으로 업로드합니다.
2. 테스트할 종목과 기간을 선택합니다.
3. 백테스트를 실행하고 결과를 확인합니다.

**확인해야 할 핵심 지표**

| 지표 | 설명 | 주의점 |
|------|------|--------|
| 총 수익률 | 기간 전체 수익률 | 미실현 이익 포함 여부 확인 |
| CAGR | 연환산 수익률 | 워밍업 기간이 길면 과대계상 가능 |
| 최대 낙폭 (MDD) | 고점 대비 최대 하락폭 | 실전 감내 가능한지 확인 |
| 샤프 비율 | 위험 대비 수익 효율 | 워밍업이 길면 실제보다 높게 나올 수 있음 |
| 승률 | 청산 포지션 기준 | 미청산 포지션은 포함되지 않음 |

**파라미터 최적화**

Backtester는 Grid Search / Random Search로 최적 파라미터를 탐색합니다.
예: SMA 골든크로스 전략에서 `fast_period`와 `slow_period`의 최적값 탐색.

> 최적화 결과는 과거 데이터에 최적화된 값입니다.
> 과적합(overfitting) 위험을 항상 고려하세요.

---

### 3.3 전략 실행 — 모의투자 검증 후 실전

**Strategy Builder `/execute` 페이지에서:**

1. 검증된 전략 선택
2. 종목 입력
3. BUY/SELL/HOLD 시그널 확인
4. **먼저 모의투자로 주문 실행** (설정에서 `vps` 모드 선택)
5. 일정 기간 모의투자 결과 확인 후 실전 전환

```
모의투자 충분히 검증 → 실전투자
vps 모드              prod 모드
```

---

## 4. MCP 서버 — AI 에이전트 연동

이 프로젝트는 Claude Code, Cursor 등 AI 에이전트에서 직접 거래 작업을 수행할 수 있는 MCP(Model Context Protocol) 서버를 세 가지 제공합니다.

### 4.1 KIS Trading MCP

`MCP/Kis Trading MCP/` — 국내주식, 해외주식, ETF/ETN, ELW, 채권, 선물/옵션 거래 API를 AI 에이전트에서 직접 호출할 수 있습니다.

지원 상품:

- 국내 주식 / 해외 주식
- ETF/ETN / ELW
- 국내채권 / 국내 선물·옵션 / 해외 선물·옵션

### 4.2 KIS Code Assistant MCP

`MCP/KIS Code Assistant MCP/` — KIS Open API 문서를 AI가 검색하고 사용 방법을 안내합니다.
새로운 API 함수를 찾거나 파라미터를 확인할 때 사용합니다.

### 4.3 Backtester MCP

`backtester/kis_mcp/` — AI 에이전트에서 백테스트를 직접 실행합니다.

```bash
bash backtester/scripts/start_mcp.sh  # http://127.0.0.1:3846/mcp
```

주요 도구:

| 도구 | 설명 |
|------|------|
| `list_presets` | 10개 프리셋 전략 목록 |
| `run_backtest` | YAML 전략 백테스트 실행 |
| `get_backtest_result` | 결과 조회 |
| `get_report` | HTML 리포트 생성 |

---

## 5. 권장 사용 순서

```
1. KIS API 키 발급 및 kis_devlp.yaml 설정
        ↓
2. Strategy Builder에서 프리셋 전략 불러오기
        ↓
3. Backtester에서 과거 3~5년 데이터로 전략 검증
        ↓
4. 샤프비율, MDD, 승률, CAGR 검토
   → 기준 미달 시 전략 수정 후 재검증
        ↓
5. 모의투자로 1~3개월 실시간 검증
        ↓
6. 모의투자 결과가 백테스트와 유사하면 실전 적용
        ↓
7. 포지션 크기와 손절 기준을 엄격히 지키며 운용
```

---

## 6. 리스크 관리 원칙

이 프로젝트의 Strategy Builder와 Backtester는 손절/익절 설정을 지원합니다.
아래 원칙은 도구가 지원하는 기능에 기반한 일반적인 가이드입니다.

- **손절 설정 필수**: Strategy Builder에서 `stop_loss` 퍼센트를 반드시 설정하세요.
- **한 종목 집중 금지**: Backtester의 포트폴리오 분석 기능으로 분산투자 효과를 확인하세요.
- **과적합 경계**: 최적화된 파라미터가 과거 데이터에만 맞는지 Out-of-sample 검증을 하세요.
- **MDD 확인**: 백테스트에서 MDD가 본인이 감당할 수 있는 수준인지 먼저 확인하세요.
- **모의투자 선행**: 실전투자 전에 반드시 `vps` 모드로 모의투자를 먼저 수행하세요.

---

## 7. 관련 문서

| 문서 | 위치 | 내용 |
|------|------|------|
| 프로젝트 설정 | `README.md` | API 키 설정, 환경 구성 |
| Strategy Builder 상세 | `strategy_builder/README.md` | 빌더 사용법, API 엔드포인트 |
| Backtester 상세 | `backtester/README.md` | 백테스트 실행, 결과 해석, Python 라이브러리 |
| KIS MCP 연결 방법 | `MCP/MCP AI 도구 연결 방법.md` | AI 에이전트 MCP 설정 |
| KOSPI/KOSDAQ API | `docs/kospi-kosdaq-realtime-api.md` | 지수 실시간 API 사용법 |
| 파일 구조 | `docs/file-tree.md` | 전체 저장소 구조 |
