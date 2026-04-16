**[당사에서 제공하는 샘플코드에 대한 유의사항]**

- 샘플 코드는 한국투자증권 Open API(KIS Developers)를 연동하는 예시입니다. 고객님의 개발 부담을 줄이고자 참고용으로 제공되고 있습니다.
- 샘플 코드는 별도의 공지 없이 지속적으로 업데이트될 수 있습니다.
- 샘플 코드를 활용하여 제작한 고객님의 프로그램으로 인한 손해에 대해서는 당사에서 책임지지 않습니다.

# KIS Open API — KOSPI / KOSDAQ 지수 API 참고

[한국투자증권 Open API 포털 바로가기](https://apiportal.koreainvestment.com/)

이 저장소에서 KOSPI / KOSDAQ 실시간 지수 API를 사용하는 방법은 아래 문서를 참고하세요.

→ [`docs/kospi-kosdaq-realtime-api.md`](docs/kospi-kosdaq-realtime-api.md)

---

## 1. 사전 환경설정

### 1.1. Python 환경 요구사항

- **Python 3.11 이상** 필요
- **uv** 패키지 매니저 사용 권장 (빠르고 간편한 의존성 관리)

### 1.2. uv 설치 방법

```bash
# Windows (PowerShell)
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"

# macOS/Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# 설치 확인
uv --version
```

### 1.3. 프로젝트 클론 및 환경 설정

```bash
git clone https://github.com/koreainvestment/open-trading-api
cd open-trading-api
uv sync
```

### 1.4. KIS Open API 신청 및 설정

🍀 [서비스 신청 안내 바로가기](https://apiportal.koreainvestment.com/about-howto)
1. 한국투자증권 **계좌 개설 및 ID 연결**
2. 한국투자증권 홈페이지 or 앱에서 **Open API 서비스 신청**
3. **앱키(App Key)**, **앱시크릿(App Secret)** 발급
4. **모의투자** 및 **실전투자** 앱키 각각 준비

### 1.5. kis_devlp.yaml 설정

- 본인의 계정 설정을 위해 `kis_devlp.yaml` 파일을 수정합니다.
- 기본 경로는 `~/KIS/config/kis_devlp.yaml`입니다. 폴더가 없으면 생성해 주세요.

```bash
mkdir -p ~/KIS/config
cp kis_devlp.yaml ~/KIS/config/
```

1. `~/KIS/config/kis_devlp.yaml` 파일 열기
2. **앱키와 앱시크릿** 정보 입력
3. **HTS ID** 정보 입력
4. **계좌번호** 정보 입력 (앞 8자리와 뒤 2자리 구분)
5. **저장** 후 닫기

```yaml
# 실전투자
my_app: "여기에 실전투자 앱키 입력"
my_sec: "여기에 실전투자 앱시크릿 입력"

# 모의투자
paper_app: "여기에 모의투자 앱키 입력"
paper_sec: "여기에 모의투자 앱시크릿 입력"

# HTS ID(KIS Developers 고객 ID) - 체결통보, 나의 조건 목록 확인 등에 사용됩니다.
my_htsid: "사용자 HTS ID"

# 계좌번호 앞 8자리
my_acct_stock: "증권계좌 8자리"
my_paper_stock: "모의투자 증권계좌 8자리"

# 계좌번호 뒤 2자리
my_prod: "01" # 종합계좌

# User-Agent(기본값 사용 권장, 변경 불필요)
my_agent: "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
```

### 1.6. 인증 설정

```python
import kis_auth as ka

# 실전투자 인증
ka.auth(svr="prod", product="01")  # 모의투자: svr="vps"
```

---

## 2. 문제 해결

### 토큰 오류 시

```python
import kis_auth as ka

# 토큰 재발급 - 1분당 1회 발급됩니다.
ka.auth(svr="prod")  # 또는 "vps"
```

### 설정 파일 오류 시

- `kis_devlp.yaml` 파일의 앱키, 앱시크릿이 올바른지 확인
- 계좌번호 형식이 맞는지 확인 (앞 8자리 + 뒤 2자리)
- 실시간 시세(WebSocket) 이용 중 'No close frame received' 오류가 발생하는 경우, `kis_devlp.yaml`에 입력하신 HTS ID가 정확한지 확인

### 의존성 오류 시

```bash
uv sync --reinstall
```

---

## 3. Java 기반 API 서비스 (Java-based API Service)

> **상태**: 설계 계획 단계 (코드 스캐폴딩 미완료)
>
> 이 섹션은 Java 소비자를 위한 KIS Open API 서비스 뼈대의 요구사항을 기록합니다.
> 실제 소스 파일 및 빌드 설정은 오픈 질문 해결 후 별도 실행 단계에서 작성됩니다.

### 3.1. 스택 요구사항 (Stack Requirements)

| 항목 | 요구사항 |
|------|----------|
| JDK | 21 (LTS) |
| 빌드 도구 | Gradle (Kotlin DSL 또는 Groovy DSL) |
| WAS | Tomcat 10.x (Jakarta EE 10) 권장 — 버전 확인 필요 ※ |
| 의존성 주입 | Spring Framework 또는 경량 DI 프레임워크 (미정) |

※ 원 요청에 "Tomcat 4 이상"으로 기재되어 있으나, Tomcat 4.x는 구형(Servlet 2.3)입니다.
현대적 Jakarta EE 10 대응을 위해 **Tomcat 10.x** 사용을 권장하며, 최종 버전은 인간 검토 후 확정합니다.

### 3.2. 예정 디렉터리 구조 (Planned Directory Layout)

```
open-trading-api-hantu/
└── java/                        # Java 서비스 루트 (미생성)
    ├── build.gradle(.kts)       # Gradle 빌드 스크립트
    ├── gradle/
    │   └── wrapper/             # Gradle Wrapper
    ├── src/
    │   └── main/
    │       ├── java/
    │       │   └── com/kis/openapi/   # KIS Open API Java 패키지
    │       │       ├── auth/          # 인증 모듈
    │       │       └── api/           # API 호출 모듈
    │       └── resources/
    │           └── application.yml    # 설정 파일
    └── src/
        └── test/
            └── java/                  # 테스트 코드
```

> 위 구조는 계획 단계의 초안입니다. 실제 스캐폴딩 시 변경될 수 있습니다.

### 3.3. 미결 질문 (Open Questions — 실행 전 확인 필요)

1. **Tomcat 버전**: "Tomcat 4 이상"은 Tomcat 10.x(Jakarta EE 10)를 의미하는지, 또는 특정 버전이 있는지 확인 필요.
2. **디렉터리 배치**: Java 소스를 `java/` 하위 디렉터리에 배치할지, 루트 프로젝트 구조를 대체할지 결정 필요.
3. **KIS API 커버리지**: Java 뼈대가 전체 API를 커버할지, 또는 인증 + 최소 엔드포인트 예시만 구현할지 결정 필요.

### 3.4. 지연된 작업 (Deferred)

아래 항목은 위 미결 질문 해결 후 별도 실행 단계에서 진행됩니다:

- `java/` 디렉터리 생성 및 Gradle 빌드 파일 작성
- Gradle Wrapper 초기화
- 인증 모듈 (`/oauth2/tokenP`) 최소 구현
- Tomcat 배포 설정 (`web.xml` 또는 Spring Boot 내장 Tomcat)
- 의존성 목록 확정 및 `build.gradle` 작성

### 3.5. `.gitkeep` 플레이스홀더 파일

이 저장소의 일부 빈 디렉터리에는 `.gitkeep` 파일이 포함되어 있습니다.

Git은 빈 디렉터리를 추적하지 않습니다. `.gitkeep` 파일은 내용이 없는 빈 파일로, 디렉터리 자체를 Git이 인식하고 추적할 수 있도록 관례적으로 사용하는 플레이스홀더입니다. 실제 소스 파일이 해당 디렉터리에 추가되면 `.gitkeep` 파일은 삭제됩니다.

> **Git does not track empty directories.** A `.gitkeep` file is an empty placeholder that allows an otherwise-empty directory to be committed to the repository. It is removed once real source files occupy the directory.

---

# 📧 문의사항

- [💬 한국투자증권 Open API 챗봇](https://chatgpt.com/g/g-68b920ee7afc8191858d3dc05d429571-hangugtujajeunggweon-open-api-seobiseu-gpts)에 언제든 궁금한 점을 물어보세요.
