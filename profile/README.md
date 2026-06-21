![All-In-Market 대문](image/allinmarket.png)
---
# 1. 👨‍👩‍👧‍👦 팀원 소개

| 이름  | 역할 | 담당 기능                                                     | GitHub     | GitLab |
|-----|----|-----------------------------------------------------------|------------|---------------|
| 김세현 | 팀장 | 관리자 서버 / 알림 서버 / WebSocket / Flyway 도입                    | [GitHub](https://github.com/ginsengcandy) | [GitLab](https://gitlab.com/kimsparadise0202) |
| 함형우 | 팀원 | 고객 서버 API / CI/CD / Infra / Terraform                     | [GitHub](https://github.com/hyuham1335-stack) | [GitLab](https://gitlab.com/hyuham1335) |
| 배주원 | 팀원 | 고객 서버 API / 채팅 서버 / WebSocket / Redis Pub/Sub / 정산, 일일 통계 | [GitHub](https://github.com/bjw446) | [GitLab](https://gitlab.com/yourmylife1211) |
| 이준연 | 팀원 | 고객 서버 API / LangChain4j / Vector Embedding / Outbox 패턴 적용 | [GitHub](https://github.com/LeeJun14) | [GitLab](https://gitlab.com/777ljy777) |

<br>

---

# 2. 📌 프로젝트 개요

## 프로젝트 소개

### “높은 트래픽 환경에서도 안정적인 주문 처리를 보장하는 이커머스 백엔드 구축”

`AllInMarket`은 구매자/판매자 도메인을 분리한 멀티 벤더 이커머스 백엔드 프로젝트입니다.

실제 이커머스 실무에서 발생하는 재고 차감 시 동시성 문제, 주문 상태 전이, 판매자별 주문 분리 문제, 실시간 알림 서비스 등이 구현되어 있습니다.

## 핵심 기술 스택

| 영역 | 기술 |
|---|---|
| Language / Framework | Java 21, Spring Boot 4, Spring MVC, Spring Security |
| Persistence | Spring Data JPA, Querydsl, PostgreSQL, Flyway |
| Cache / Lock | Redis, Redisson |
| Auth / Security | JWT, Refresh Token Rotation, Redis blacklist, Login rate limit |
| Docs / Test | JUnit 5, Mockito, Spring REST Docs, Asciidoctor |
| Observability / Infra | Actuator, Micrometer, Prometheus, CloudWatch, Grafana, Terraform, k6 |

## 실행 및 검증

```bash
# 전체 테스트
./gradlew test

# REST Docs 생성
./gradlew asciidoctor

# 애플리케이션 실행
./gradlew bootRun

# k6 시나리오 실행은 로컬 인프라 준비 후 수행
docker compose -f docker-compose-k6.yml up --abort-on-container-exit
```

필수 환경변수 예시는 `DB_PASSWORD`, `JWT_SECRET`, `SELLER_ID`, `SELLER_PASSWORD`, `SERVER_SECRET_KEY`입니다. 로컬 실행 시 PostgreSQL, Redis 등 외부 의존성이 필요합니다.
<br>



## 프로젝트 기간

- 2026.04.07 ~ 2026.05.15
---

# 3. 🏗️ Architecture
![architecture](image/AllInMarket-Architecture.png)

<br>

---

# 4. 📦 Repository 구조

| Repository      | Description             |
|-----------------|-------------------------|
| customer-server | 구매자 / 판매자 / 상품 API      |
| chat-server     | AI 및 실시간 채팅             |
| notification-server    | 재입고 및 이벤트 알림            |
| admin-server    | 관리자 API                 |

<br>

## 🔗 Server README

- Customer Server README → [바로가기](https://gitlab.com/allinone322020/e-commerce-final-project/-/blob/dev/README.md)
- Chat Server README → [바로가기](https://gitlab.com/allinone322020/chat-server/-/blob/main/README.md)
- Notification Server README → [바로가기](https://gitlab.com/allinone322020/notification-server/-/blob/dev/README.md)
- Admin Server README → [바로가기](https://gitlab.com/allinone322020/admin-server/-/blob/dev/README.md)

<br>

---

# 5. 🚀 핵심 기능

## 365일 24시간 응대 가능한 AI 챗봇 서비스

- AI 챗봇에게 반품, 교환 및 서비스 정책에 대한 모든 궁금한 사항을 일상 대화처럼 자유롭게 물어보고, 정확한 답변을 받을 수 있습니다.

<br>

## 판매 현황 대시보드 제공

- 판매 대시보드를 통해 판매량, 주문 수, 매출 등의 데이터를 집계해 볼 수 있습니다. 일 단위 통계 데이터를 자동으로 집계하여 판매자는 자신의 운영 현황을 손쉽게 확인할 수 있습니다.

<br>

## 판매 데이터를 기반으로 정산 금액을 자동 계산 및 관리

- 일일 통계 데이터를 기반으로 월 2회 판매자 정산 금액을 자동 계산 합니다. 정산 과정과 내역을 체계적으로 관리할 수 있도록 설계하여 운영 효율성과 데이터 신뢰성을 높였습니다.

<br>

## 판매자와의 1:1 실시간 채팅

- 실시간 채팅 기능을 통해 구매자는 상품 문의를 즉시 전달할 수 있고, 판매자는 빠르게 응답할 수 있습니다. 읽음 표시 여부로 읽지 않은 메세지를 빠르게 확인 할 수 있고, 이전에 나눴던 채팅 기록을 확인할 수 있습니다.

<br>

## 품절 상품의 재입고 여부를 실시간으로 알림 제공

- 구매자는 품절된 상품에 대해 재입고 알림을 구독할 수 있으며, 상품 재고가 다시 등록되면 즉시 알림을 받을 수 있습니다. 이를 통해 구매자의 재방문을 유도하고 판매 기회를 높였습니다.

<br>

---

# 6. 🛠️ 기술 스택

### Language
<img src="https://img.shields.io/badge/Java-21-orange?logo=openjdk&logoColor=white" style="height:60px; width:auto;"/>

### Backend
<img src="https://img.shields.io/badge/Spring%20Boot-3.0-green?logo=springboot&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/Spring%20Security-blue?logo=springsecurity&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/Spring%20Data%20JPA-lightgrey?logo=spring&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/Hibernate-brown?logo=hibernate&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/QueryDSL-darkblue?logo=graphql&logoColor=white" style="height:60px; width:auto;"/>

### Real-Time
<img src="https://img.shields.io/badge/WebSocket-black?logo=socketdotio&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/Redis%20Pub/Sub-red?logo=redis&logoColor=white" style="height:60px; width:auto;"/>

### AI Integration
<img src="https://img.shields.io/badge/OpenAI-API-black?logo=openai&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/OpenAI-Embeddings-blue?logo=openai&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/LangChain4j-purple?logo=apache&logoColor=white" style="height:60px; width:auto;"/>

### Cloud & Infrastructure
<img src="https://img.shields.io/badge/AWS-EC2-orange?logo=amazonaws&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/AWS-ECS-orange?logo=amazonaws&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/AWS-Fargate-orange?logo=amazonaws&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/AWS-RDS-orange?logo=amazonaws&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/AWS-ElasticCache-orange?logo=amazonaws&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/AWS-Route53-orange?logo=amazonaws&logoColor=white" style="height:60px; width:auto;"/>

### Database & Caching
<img src="https://img.shields.io/badge/PostgreSQL-15-blue?logo=postgresql&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/Redis-7-red?logo=redis&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/Flyway-grey?logo=flyway&logoColor=white" style="height:60px; width:auto;"/>

### IaC
<img src="https://img.shields.io/badge/Terraform-purple?logo=terraform&logoColor=white" style="height:60px; width:auto;"/>

### CI/CD
<img src="https://img.shields.io/badge/GitHub%20Actions-CI/CD-black?logo=githubactions&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/Docker-blue?logo=docker&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/AWS-ECR-orange?logo=amazonaws&logoColor=white" style="height:60px; width:auto;"/>

### Observability
<img src="https://img.shields.io/badge/Prometheus-orange?logo=prometheus&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/Grafana-yellow?logo=grafana&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/OpenTelemetry-purple?logo=opentelemetry&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/AWS-CloudWatch-orange?logo=amazonaws&logoColor=white" style="height:60px; width:auto;"/>

### Testing & Documentation
<img src="https://img.shields.io/badge/JUnit-5-green?logo=junit5&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/Spring%20REST%20Docs-lightgrey?logo=spring&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/K6-loadtest-blue?logo=k6&logoColor=white" style="height:60px; width:auto;"/> <img src="https://img.shields.io/badge/RAGAS-evaluation-purple?logo=openai&logoColor=white" style="height:60px; width:auto;"/>

### Collaboration Tools
<img src="https://img.shields.io/badge/GitHub-black?logo=github&logoColor=white" style="height:60px; width:auto;"/>



<br>

---

# 7. 🗂️ 전체 ERD


![ERD](image/AllInMarket-ERD.png)



---

# 8. 🧠 기술적 의사 결정

##  Flyway를 통한 DB 버전 관리 및 결제 데이터 정합성 강화

### 배경

현재 결제 시스템은 중복 결제 방지를 위해 애플리케이션 계층에서 3단계(비관적 락, 상태 게이트, 낙관적 락)의 방어 체인을 구축하고 있습니다.
하지만 이는 애플리케이션 로직에 전적으로 의존하는 구조로, 외부 시스템에 의한 직접적인 데이터 조작이나 DB 레벨에서의 예기치 못한 실패 상황에서는
정합성을 100% 보장하기 어려운 위험 지점이 존재했습니다.

### 기술 선택지

결제 정합성을 DB 레벨에서 강제하기 위해 부분 고유 인덱스(Partial Unique Index) 도입을 검토했으며, 이를 관리하기 위한 툴을 비교했습니다.

|비교 항목|옵션 1: JPA @Table (@Index)|옵션 2: Flyway / Liquibase|
|--------|--------------------------|-------------------------|
|SQL 제어권|제한적 (JPA 표준 범위 내 문법만 지원)|완전함 (순수 SQL을 직접 작성 및 실행 가능)|
|Partial Index 지원|불가능 (WHERE 조건절 지원 안 함)|가능 (DB 전용 문법 사용 가능)|
|버전 관리|불가능 (ddl-auto에 의존)|가능 (스크립트 이력 관리 및 롤백 용이)|
|도입 난이도|낮음|중간 (초기 설정 및 스크립트 관리 필요)|

### 선택 이유

- DB 전용 문법 활용: 한 주문에 대해 '성공(SUCCESS)' 상태인 결제건은 단 하나만 존재해야 합니다.
- 이를 위해 WHERE status = 'SUCCESS' 조건이 포함된 인덱스가 필요했으나, JPA 어노테이션은 이를 지원하지 않아 직접 SQL을 제어할 수 있는 Flyway가 필수적이었습니다.

- 구현 효율성: Liquibase에 비해 설정이 간결하고 순수 SQL 파일만으로 마이그레이션 이력을 관리할 수 있어 빠른 도입이 가능했습니다.

### 해결 및 결과

1. Partial Unique Index 적용: payments 테이블에 특정 조건에서만 유니크함을 보장하는 인덱스를 추가하여, 애플리케이션 로직을 우회하는 데이터 입력 시에도 중복 결제를 원천 차단했습니다.

    ```SQL
    CREATE UNIQUE INDEX uq_payments_order_success
    ON payments (order_id)
    WHERE status = 'SUCCESS';
    ```

2. 형상 관리 체계 구축: 서버 구동 시 Flyway 마이그레이션 스크립트를 통해 스키마를 생성하고, ddl-auto: validate 설정을 통해 애플리케이션과 DB 상태 간의 일관성을 검증하도록 설정했습니다.

3. 테스트 환경 최적화: PostgreSQL 전용 문법과의 호환성을 고려하여, 테스트 환경에서는 Flyway를 비활성화하고 JPA의 ddl-auto 기능을 활용함으로써 테스트 코드의 유연성을 확보했습니다.

4. 결과: DB 레벨에서 결제 성공 데이터의 유일성이 보장됨에 따라 시스템 전체의 데이터 신뢰도가 크게 향상되었습니다.

<br>

---

## ECS · EC2 · Fargate를 목적에 따라 분리 운영

### 배경

시스템의 핵심인 고객 서버, 알림 서버, 채팅 서버를 구축하면서 인프라 관리의 복잡성을 줄이고 개발 생산성을 극대화할 필요가 있었습니다.
동시에 관리자 전용 서버는 기존에 구축된 인프라 자산을 최대한 활용하면서도, 운영 비용을 최적화할 수 있는 실용적인 아키텍처 설계가 요구되었습니다.

### 기술 선택지

서비스의 성격과 트래픽 특성에 따라 AWS ECS의 두 가지 실행 유형(Launch Type)을 검토했습니다.

|비교 항목|옵션 1: ECS Fargate|옵션 2: ECS + EC2|
|--------|------------------|----------------|
|인프라 관리|서버리스 (AWS가 호스트 관리)|사용자가 직접 EC2 인스턴스 관리|
|운영 부담|매우 낮음 (애플리케이션에만 집중)|보통 (OS 패치, 런타임 관리 필요)|
|비용 구조|사용한 리소스(vCPU/GB)만큼 과금|인스턴스 단위 과금 (트래픽 적을 때 유리)|
|확장성|빠르고 유연한 확장 가능|인스턴스 클러스터 크기 조절 필요|

### 선택 이유

1. 고객/알림/채팅 서버 (Fargate 선택):

    - 운영 오버헤드 최소화: OS 패치, Docker 설치 등 서버 하위 레벨의 관리 부담을 없애고 비즈니스 로직 개발에 집중하고자 했습니다.

    - 장애 범위 축소: 인프라 레벨의 이슈를 AWS에 위임함으로써 운영 중 발생할 수 있는 문제 범위를 애플리케이션 영역으로 한정할 수 있었습니다.

2. 관리자 서버 (EC2 선택):

    - 인프라 자산 재사용: 이미 구축된 ECR, ECS 기반의 Terraform 코드와 GitHub Actions 배포 파이프라인을 그대로 활용하여 구축 속도를 높였습니다.

    - 비용 효율성: 트래픽 변동이 적고 24시간 상시 구동되어야 하는 관리자 서버의 특성상, 동일 리소스 대비 Fargate보다 저렴한 EC2 방식이 경제적이라고 판단했습니다.

### 해결 및 결과

- 운영 구조의 통일: 실행 방식은 다르지만 모두 ECS Cluster 내에서 Task 단위로 관리되므로, 모든 서버의 상태 모니터링과 배포 구조를 일관되게 유지할 수 있었습니다.

- 생산성 향상: 핵심 서비스는 Fargate를 통해 인프라 관리 없이 빠르게 배포하고, 관리자 서비스는 EC2를 통해 비용을 절감하는 전략적 운영이 가능해졌습니다.

- 결과: 서비스별 요구사항(비용, 운영 편의성, 생산성)에 최적화된 아키텍처를 구성하여 전체 시스템의 안정성과 효율성을 동시에 확보했습니다.

<br>

---

## Terraform 기반 IaC를 활용한 인프라 자동화 및 형상 관리

### 배경

기존의 AWS 콘솔(GUI) 기반 구축 방식은 직관적이지만, 동일한 환경을 여러 번 재현하기 어렵고 설정 변경 이력을 추적하기 힘들다는 단점이 있었습니다.
특히 인프라 유지 비용을 최적화하기 위해 테스트 시에만 인프라를 빠르게 생성하고 삭제할 수 있는 민첩한 운영 체계가 필요했습니다.

### 기술 선택지

인프라를 코드로 관리하기 위해 시장에서 널리 쓰이는 IaC(Infrastructure as Code) 도구들을 검토했습니다.

|비교 항목|옵션 1: AWS Console (수동)|옵션 2: AWS CloudFormation|옵션 3: Terraform|
|--------|------------------------|-------------------------|-----------------|
|재현성|낮음 (수동 작업 실수 가능성)|높음|높음|
|형상 관리|불가능|가능 (JSON/YAML)|가능 (HCL)|
|유연성|-|AWS 전용|멀티 클라우드 및 서드파티 지원|
|상태 관리|없음|AWS 내부 관리|State 파일을 통한 명시적 관리|

### 선택 이유

- 선언형 아키텍처: "어떤 상태가 되어야 한다"를 정의하면 Terraform이 현재 상태와의 차이(Diff)를 계산해 변경분만 적용하므로 운영 안정성이 매우 높습니다.

- 강력한 생태계 (Provider & Module): AWS 리소스뿐만 아니라 Grafana, GitHub 등 다양한 서드파티 리소스도 Provider를 통해 통합 관리할 수 있습니다.
  예를 들어, Grafana 대시보드와 데이터 소스를 코드로 자동 생성하여 관측성(Observability) 환경을 즉시 구축할 수 있었습니다.

- 운영 비용 절감: 인프라를 코드로 정의해 두었기 때문에 필요할 때만 전체 스택을 배포(apply)하고 사용 후 즉시 파괴(destroy)할 수 있어, 배포 테스트 비용을 획기적으로 줄일 수 있었습니다.

### 해결 및 결과

1. Git 기반 형상 관리: 모든 인프라 설정을 Git 리포지토리에서 관리함으로써 변경 이력을 추적하고, 팀원 간의 코드 리뷰를 통해 설정 오류를 사전에 방지하는 프로세스를 확립했습니다.

2. 표준화된 배포: 수동 설정 시 발생할 수 있는 'Human Error'를 원천 차단하고, 개발/스테이징/운영 환경의 일관성을 확보했습니다.

3. 유연한 확장성: 특정 클라우드 벤더에 종속되지 않는 구조를 채택하여, 향후 멀티 클라우드나 하이브리드 클라우드 전략으로 확장할 수 있는 기반을 마련했습니다.

4. 결과: 인프라 구축 및 변경 시간이 단축되었으며, 코드를 통한 자동화로 인프라 운영 전반의 신뢰성과 효율성을 극대화했습니다.

<br>

---

## CloudWatch와 Prometheus/Grafana 기반 계층별 모니터링 전략

### 배경

시스템의 안정성을 확보하기 위해서는 인프라의 물리적 상태부터 애플리케이션의 내부 로직까지 전 계층에 대한 가시성(Visibility)이 필요합니다.
AWS 인프라 리소스와 스프링 부트(Spring Boot) 애플리케이션 각각의 지표 특성이 다르기 때문에, 각 영역에 최적화된 도구를 조합하여 효율적인 모니터링 체계를 구축하고자 했습니다.

### 기술 선택지

모니터링 대상에 따라 두 가지 핵심 도구를 상호 보완적으로 배치했습니다.

|모니터링 층위|도구|수집 대상 및 지표|
|-----------|---|---------------|
|인프라 레벨|AWS CloudWatch|ALB(요청 수), ECS(CPU/Mem), RDS(커넥션), ElastiCache, 컨테이너 로그|
|애플리케이션 레벨|Prometheus|API 응답 시간, 에러율, JVM 메트릭, HikariCP 커넥션 풀, 스레드 사용량|
|시각화/분석|Grafana|Prometheus 메트릭 통합 대시보드 구성 및 PromQL 기반 심층 분석|

### 선택 이유

- 인프라 호환성: CloudWatch는 AWS 서비스와 네이티브하게 통합되어 있어 별도의 에이전트 설치 없이도 ALB, ECS 등의 메트릭을 즉시 수집하고 로그(CloudWatch Logs)를 관리할 수 있습니다.

- 유연한 쿼리 분석: CloudWatch는 디멘션(Dimension) 기반 조회의 제약으로 세부 애플리케이션 지표 분석이 까다롭습니다. 반면 Prometheus는 강력한 PromQL을 지원하여 라벨(Label) 기반으로 복잡한 집계 및 분석을 직관적으로 수행할 수 있습니다.

- 시각화 최적화: Grafana는 Prometheus와의 연동성이 뛰어나며, JVM이나 Spring Boot 관련 커뮤니티 대시보드 템플릿을 활용해 전문적인 관측성(Observability) 환경을 빠르게 구축할 수 있습니다.

### 해결 및 결과

1. 계층별 모니터링 분리: 인프라 상태 및 로그는 CloudWatch가 담당하고, 애플리케이션 성능 지표는 Prometheus가 수집하도록 역할을 분리하여 모니터링 시스템의 부하를 분산했습니다.

2. Spring Boot Actuator 연동: Micrometer를 통해 애플리케이션 메트릭을 Prometheus 포맷으로 노출하고, 이를 정기적으로 스크래핑(Scraping)하여 데이터를 축적했습니다.

3. 통합 대시보드 구축: Grafana를 통해 API 응답 시간(P99, P95), HTTP 상태 코드별 에러율, 힙(Heap) 메모리 사용량 등을 한눈에 파악할 수 있는 대시보드를 구성했습니다.

4. 결과: 장애 발생 시 인프라 문제인지 애플리케이션 로직 문제인지 빠르게 판별할 수 있게 되었으며, 병목 지점(예: DB 커넥션 풀 부족, 스레드 병목)을 정밀하게 타격하여 성능을 개선할 수 있는 기반을 마련했습니다.

<br>

---

## 도메인 특화 Narrow RAG 전략 채택

### 배경

멀티벤더 마켓플레이스의 고객 문의 챗봇을 구축하는 상황에서, 교환/환불/배송 등 정책 관련 질문에 정확한 답변을 제공해야 했다.

### 기술 선택지

| 비교 항목 | Wide & Diverse RAG | Narrow & Specialized RAG |
|---|---|---|
| 지식 범위 | 위키, 뉴스, 블로그 등 광범위한 데이터 | 검증된 도메인 문서만 사용 |
| 환각(Hallucination) 위험 | 높음 | 낮음 |
| 출처 검증 | 어려움 | 명확함 |
| 법적 분쟁 대응 | 어려움 | 구조적 차단 가능 |

### 선택 이유

Wide RAG는 다양한 질문에 답할 수 있지만, 정책처럼 정확성이 중요한 도메인에서는 환각(Hallucination) 위험이 높고 출처 검증이 어렵다.
반면 검증된 정책 문서만을 사용하면 답변의 출처가 명확해지고, 법적 분쟁 소지를 구조적으로 차단할 수 있다.

### 해결 및 결과

지식 베이스를 정책 문서로 한정함으로써 LLM이 학습 지식으로 추측하는 상황 자체를 제거했다.
정책에 없는 질문은 답변하지 않는 명확한 경계가 생겨 답변 일관성과 신뢰도가 높아졌다.

<br>

---

## Adaptive RAG로 질문 유형별 처리 전략 분기

### 배경

챗봇에 들어오는 질문은 정책 관련 질문만이 아니다. "안녕하세요", "감사합니다" 같은 일상적인 인사도 포함된다.

### 기술 선택지

| 비교 항목 | 단일 전략 | Adaptive RAG |
|---|---|---|
| 처리 방식 | 모든 질문에 RAG 파이프라인 적용 | 질문 유형 분류 후 처리 방식 분기 |
| 불필요한 검색 호출 | 발생 | 제거 |
| 자원 효율 | 낮음 | 높음 |

### 선택 이유

검색이 필요 없는 인사말에도 벡터 검색과 키워드 검색을 수행하면 불필요한 자원이 소비되고 응답 시간이 늘어난다.
Jeong et al. (2024) 논문(NAACL 2024)은 질문의 복잡도에 따라 검색 전략을 달리해야 한다는 것을 보여준다.

### 해결 및 결과

질문 유형별로 처리 전략을 분기함으로써 불필요한 검색 호출을 제거하고 자원 효율을 높였다.
모든 질문을 동일하게 처리하는 것이 항상 최선이 아님을 보여주는 설계 결정이었다.

<br>

---


## WAF + Login Rate Limit Filter를 활용한 로그인 API 보안 강화

### 배경

현재 시스템은 로그인 실패 시 구체적인 사유(예: 존재하지 않는 계정, 비밀번호 불일치 등)를 노출하고 있어, 공격자가 유효한 계정 정보를 추론할 수 있는 단서를 제공하고 있었습니다.
또한, 특정 IP에서의 대규모 트래픽 공격이나 분산 IP를 이용한 무차별 대입 공격(Brute Force Attack)에 대한 방어 체계가 부재하여 인프라 및 애플리케이션 레벨의 보호 대책이 시급했습니다.

### 기술 선택지

로그인 API를 보호하기 위해 인프라 계층과 애플리케이션 계층을 모두 아우르는 다중 방어 전략을 검토했습니다.

|비교 항목|AWS WAF (Infra)|Redis 기반 Filter (App)|
|--------|---------------|----------------------|
|차단 위치|서버 도달 전 (엣지)|서버 도달 후 (Spring Boot)|
|차단 단위|IP 단위 (Rate-based)|IP, 계정, IP+계정 복합 차단|
|제어 정밀도|단순 트래픽 제한|비즈니스 로직 기반 세밀한 제한|
|주요 목적|대규모 DDoS 및 스캐닝 방어|무차별 대입 공격 및 계정 잠금|

### 선택 이유

- 다중 방어 계층(Defense in Depth) 구축: AWS WAF를 통해 서버 리소스를 소모하기 전 대규모 공격을 일차적으로 걸러내고,
  애플리케이션 내부 필터에서 비즈니스 로직(계정별 실패 횟수 등)에 기반한 정밀한 차단을 수행하도록 설계했습니다.

- 계정 정보 유출 방지: 실패 사유를 "로그인 실패"로 통일하여 공격자의 정보 추론을 원천 차단했습니다.

- 보안 가시성 및 유연성: Redis 카운터를 사용하여 동일 공격자가 IP를 변경하며 특정 계정을 공격하거나,
  한 네트워크 내에서 여러 계정을 공격하는 시나리오를 모두 방어할 수 있습니다.

### 해결 및 결과

1. 실패 사유 통일 및 로깅: 클라이언트에는 일관된 실패 메시지를 반환하되, 내부 로그에는 상세 사유를 기록하여 운영 모니터링은 유지했습니다.

2. AWS WAF 적용: 5분 이내 1,000번 이상의 요청이 발생하는 IP를 인프라 레벨에서 즉시 차단하여 서버 부하를 방지했습니다.

3. Redis 기반 중첩 차단 로직 구현:

    - IP + 계정: 5분 내 5회 실패 시 5분간 차단 (동일 공격자의 집중 공격 방어)

    - 계정 전용: 5분 내 10회 실패 시 5분간 차단 (IP 변조를 통한 분산 공격 방어)

4. 보안 취약점 보완:

    - X-Forwarded-For 스푸핑 방지: ALB의 동작 방식을 고려하여 헤더의 마지막 IP를 신뢰하도록 로직을 강화했습니다.

    - 대용량 페이로드 차단: 8KB 초과 요청 시 413 에러를 반환하여 메모리 고갈 공격을 방지했습니다.

    - 개인정보 보호: Redis 저장 시 이메일을 SHA-256으로 해싱하여 데이터 유출 시에도 개인정보를 보호했습니다.

5. 결과: 무차별 대입 공격에 대한 방어 성공률이 크게 향상되었으며, 비정상적인 로그인 시도로부터 시스템 리소스를 안전하게 보호할 수 있게 되었습니다.

<br>

---

# 9. ⚡ 성능 개선 / 최적화

## 분산 락 중복 적용 제거를 통한 결제 프로세스 성능 최적화

### 문제

- 현상: 부하 테스트 결과, 구매 플로우의 초당 트래픽 처리 속도(RPS)가 목표치인 100에 미달하는 74.71을 기록했습니다.

- 영향: 대량의 결제 요청이 집중될 경우 응답 지연이 발생하고, 처리되지 못한 요청들이 실패로 이어져 사용자 경험과 매출에 부정적인 영향을 미쳤습니다.

### 해결

- 이중 락 구조 진단: 성능 저하의 원인을 분석한 결과, 결제 로직 진입점(Facade)에서 Redisson 분산 락을 획득한 후, 내부 비즈니스 로직(OrderService)에서 다시 한번 DB 비관적 락(Pessimistic Lock)을 점유하는 중복 잠금 구조를 확인했습니다.

- 락 메커니즘 단일화: 분산 환경에서 원자성을 보장하기 위해 도입한 Redisson 분산 락만 유지하고, 불필요한 DB 레벨의 대기 시간을 유발하는 비관적 락을 제거하여 트랜잭션 점유 시간을 단축했습니다.

### 성능 개선 결과

![분산락 개선](image/RedisLock-throughput.png)
![분산락 개선2](image/RedisLock-rps.png)

![분산락 개선3](image/RedisLock-p95-med-avg.png)

중복 락 제거 후 동일 조건에서 부하 테스트를 진행한 결과, 모든 지표에서 유의미한 성능 향상을 확인했습니다.

- 응답 속도 획기적 단축: 평균 응답 시간이 2.89s에서 1.35s로 53.3% 감소하여 사용자 대기 시간이 절반 이하로 줄어들었습니다.

- 지연 시간 편차 개선: P95 지표가 5.03s에서 4.07s로 19.1% 개선되어 극한의 부하 상황에서도 안정적인 응답성을 확보했습니다.

- 시스템 처리량(Throughput) 증대: 전체 처리량이 8,399건에서 10,624건으로 26.5% 향상되었습니다.

- 처리 실패율 감소: 불필요한 락 대기 및 타임아웃으로 인한 처리 실패 건수가 5,130건에서 2,905건으로 43.4% 감소했습니다.

- 목표 RPS 달성: 초당 요청 처리 속도(RPS)가 74.71에서 104.62로 40% 개선되어 초기 목표치(100 RPS)를 상회하는 결과를 얻었습니다.

<br>

---

## Virtual Thread 도입을 통한 RAG 파이프라인 I/O 블로킹 문제 해결

### 문제

- 현상: RAG(Retrieval-Augmented Generation) 파이프라인의 핵심인 벡터 검색, 키워드 검색, LLM API 호출이 모두 순차적인 I/O 집약적(I/O-Bound) 로직으로 구성되어 있어, 요청이 몰릴 경우 급격한 응답 지연이 발생함.

- 원인: 기존 ThreadPoolTaskExecutor 방식은 OS 스레드와 1:1로 매핑되는 플랫폼 스레드를 사용하므로 maxPoolSize가 고정되어 있습니다.
  이로 인해 동시 요청이 스레드 풀 크기를 초과하면 신규 요청은 큐에서 대기하게 되며, 특히 외부 API 호출과 같은 I/O 대기 구간에서도 스레드를 계속 점유(Blocking)하여 자원 낭비가 심화되었습니다.

- 영향: 가상 유저 20명 기준 부하 테스트 시 p95 응답 시간이 9.84s까지 치솟아 실시간 서비스 제공에 한계가 있었습니다.

### 해결

- Virtual Thread(JEP 444) 도입: Java 21의 경량 스레드인 Virtual Thread를 적용하여 I/O 효율성을 극대화했습니다.

- Non-blocking 컨텍스트 스위칭: Virtual Thread는 I/O 작업으로 인해 대기 상태가 되면 실제 OS 스레드(Carrier Thread)를 점유하지 않고 즉시 반납합니다.
  덕분에 대기 시간 동안 다른 요청을 처리할 수 있어 시스템의 처리량(Throughput)이 대폭 향상되었습니다.

- 생산성 유지: 리액티브 프로그래밍(WebFlux 등)과 달리 기존의 직관적인 동기 코드 스타일을 그대로 유지하면서도 비동기 방식의 성능 이점을 얻을 수 있어 코드 복잡도를 낮게 유지했습니다.

### 성능 개선 결과

![VirtualThread](image/VirtualThread-p95-med-avg.png)

Virtual Thread 전환 후 동일한 부하 테스트(VU 20) 조건에서 지연 시간 지표가 약 50% 이상 개선되었습니다.

- 응답 속도 획기적 단축: p95 응답 시간이 9.84s에서 4.74s로 52% 감소하여 고부하 상황에서도 안정적인 속도를 확보했습니다.

- 평균 대기 시간 최적화: 평균 응답 시간이 6.25s에서 3.13s로 50% 감소했습니다.

- 안정성 유지: 리소스 점유 방식이 개선되었음에도 에러율 0%를 유지하며 데이터 무결성과 시스템 안정성을 입증했습니다.

- 처리 용량 증대: 스레드 부족으로 인한 대기 현상이 해소되어, 동일한 하위 리소스 사양 내에서 더 많은 동시 접속을 수용할 수 있는 기반을 마련했습니다.

<br>

---

## RAG 파이프라인 정교화를 통한 챗봇 응답 품질 및 신뢰성 개선

### 문제

- 현상: 멀티벤더 마켓플레이스 고객 문의 챗봇의 응답 품질을 RAGAS 프레임워크로 측정한 결과, Faithfulness(충실도) 0.65, Answer Relevancy(답변 관련성) 0.73이라는 낮은 수치를 기록함.

- 원인:

    1. 의미 단절: 단순 고정 크기 청킹(Fixed-size Chunking)으로 인해 정책 문서의 맥락이 잘려 검색 품질이 저하됨.

    2. 할루시네이션: LLM이 제공된 컨텍스트가 아닌 내부 학습 지식에 의존하여 추측성 답변을 생성함.

    3. 불안정한 응답: 특정 질문에 대해 답변을 회피하거나 실제 정책과 다른 오답을 반환하는 사례가 빈번함.

### 해결

RAG 파이프라인의 전 과정(데이터 전처리, 검색, 생성)을 고도화하여 응답의 정확도를 높였습니다.

1. Semantic Chunking 도입: 단순 글자 수가 아닌 문장 간 의미적 유사도를 기준으로 데이터를 분할하여, 정책 항목이 온전한 의미 단위로 유지되도록 개선했습니다.

2. 하이브리드 검색 및 RRF 적용: 벡터 검색(Semantic)과 키워드 검색(BM25)을 결합하고, RRF(Reciprocal Rank Fusion) 알고리즘을 통해 검색 결과의 순위를 재조정하여 검색 정확도를 극대화했습니다.

3. System Prompt 고도화: LLM에게 "제공된 컨텍스트에 답변 근거가 없을 경우 모른다고 명시할 것"과 "내부 지식을 배제하고 컨텍스트에만 기반할 것"을 명확히 정의하여 근거 기반 답변(Grounded Answer)을 강제했습니다.

### 성능 개선 결과

![RAG](image/RAG.png)

품질 지표 측정 도구인 RAGAS를 통해 정량적으로 검증한 결과, 모든 지표에서 괄목할만한 향상을 확인했습니다.

- 답변 신뢰성 완벽 확보: Faithfulness가 0.65에서 1.00으로 46% 향상되어, LLM이 오직 컨텍스트에 기반한 정확한 답변만 생성하게 되었습니다.

- 답변 관련성 최적화: Answer Relevancy가 0.73에서 0.85로 18% 향상되어 사용자 질문 의도에 부합하는 답변을 제공합니다.

- 검색 품질 유지: Context Recall 수치를 1.00으로 유지하며 필요한 정보를 누락 없이 검색하는 성능을 보존했습니다.

- 정확도 전환: 기존의 오답이나 빈 답변 사례가 사라지고, 실제 마켓플레이스 정책에 근거한 정확한 답변으로 모두 전환되었습니다.

<br>

---

## 아웃박스(Outbox) 스케줄러 주기 최적화를 통한 시스템 부하 감소 및 성능 개선

### 문제

- 현상: 백그라운드에서 동작하는 여러 스케줄러의 실행 빈도가 비정상적으로 잦아 시스템 전체의 리소스를 과도하게 점유함.

- 원인:

    1. Dashboard Outbox 스케줄러: 2초 주기로 동작하며 실시간에 가까운 업데이트를 시도했으나, 대시보드 데이터 특성상 불필요한 DB 조회를 반복함.

    2. TransactionHistory Outbox 스케줄러: 10초 주기로 동작하며 거래 이력을 처리했으나, 짧은 간격으로 인해 스케줄러 간의 경합 및 DB 커넥션 부하가 가중됨.

- 영향: 스케줄러 작업이 비즈니스 트랜잭션과 리소스를 경쟁하면서 전체적인 API 응답 지연과 처리 실패율 상승을 초래함.

### 해결

비즈니스 요구사항에 맞춰 데이터의 최종 일관성(Eventual Consistency) 허용 범위를 재정의하고 스케줄러 동작 빈도를 최적화했습니다.

1. Dashboard Outbox 주기 조정: 실행 빈도를 2초에서 1분으로 수정했습니다. 대시보드 통계의 경우 약간의 지연(1분)이 발생하더라도 시스템 전체 안정성을 확보하는 것이 더 이득이라고 판단했습니다.

2. TransactionHistory Outbox 주기 조정: 실행 빈도를 10초에서 5분으로 수정했습니다. 거래 이력 반영 속도를 조절함으로써 DB IOPS(Input/Output Operations Per Second) 부하를 획기적으로 낮추었습니다.

3. 리소스 효율화: 잦은 폴링(Polling)으로 인한 CPU 사용량과 DB 커넥션 점유 시간을 줄여 실질적인 결제 및 주문 트랜잭션이 가용 리소스를 충분히 활용할 수 있도록 개선했습니다.

### 성능 개선 결과

![스케줄러](image/scheduler-throughput.png)
![스케줄러2](image/scheduler-rps.png)

![스케줄러3](image/scheduler-p95-med-avg.png)

스케줄러 주기를 비즈니스 우선순위에 맞게 재설정한 결과, API 처리 성능과 안정성이 크게 향상되었습니다.

- 응답 속도 대폭 향상: 평균 응답 시간이 1.35s에서 781ms로 42.1% 감소하여 1초 미만의 안정적인 응답성을 확보했습니다.

- 지연 시간 편차 안정화: P95 지표가 4.07s에서 2.94s로 27.8% 개선되었습니다.

- 시스템 신뢰도 증가: 불필요한 리소스 경쟁이 사라지면서 처리 실패 건수가 2,905건에서 1,379건으로 52.6% 감소했습니다.

- 처리 용량 최적화: 초당 요청 처리 속도(RPS)가 104.62에서 120.46으로 15.1% 개선되었으며, 전체 처리량(Throughput) 역시 10,624건에서 12,150건으로 약 14.4% 향상되었습니다.

<br>

---

## HikariCP 커넥션 풀 최적화를 통한 DB 병목 현상 및 성능 개선

### 문제

- 현상: 부하 테스트를 진행한 결과, 급증하는 트래픽 상황에서 DB 커넥션 풀 고갈(Connection Pool Hell) 현상이 발생함.

- 원인: 기존에 설정된 HikariCP의 최대 커넥션 수(10개)가 애플리케이션의 동시 처리량을 수용하기에 부족했습니다.
  이로 인해 커넥션을 획득하지 못한 스레드들이 대기 상태(Connection Acquisition Timeout)에 빠지면서 시스템 전반의 지연이 발생했습니다.

- 영향: 요청이 몰리는 피크 타임에 응답 시간이 급격히 늘어나고, 대기 큐가 가득 차면서 일부 요청이 실패로 처리되는 안정성 문제가 확인되었습니다.

### 해결

- 커넥션 풀 확장: 애플리케이션의 처리 역량과 DB 서버의 가용 자원을 고려하여 HikariCP의 maximum-pool-size를 10에서 20으로 상향 조정했습니다.

- 자원 배분 최적화: 커넥션 수를 무작정 늘리는 대신, 부하 테스트를 통해 DB CPU 및 IOPS 부하가 허용 범위 내에 있음을 확인하고 애플리케이션이 병목 없이 쿼리를 실행할 수 있는 최적의 지점을 도출했습니다.

### 성능 개선 결과

![Hikari](image/HikariCP-throughput.png)
![Hikari2](image/HikariCP-rps.png)

![Hikari3](image/HikariCP-p95-med-avg.png)

커넥션 풀 확장 후, 대기 시간이 줄어들면서 전반적인 시스템 처리 효율이 향상되었습니다.

- 응답 속도 개선: 평균 응답 시간이 781ms에서 630.04ms로 19.4% 감소하여 더 빠른 사용자 경험을 제공하게 되었습니다.

- 지연 시간 편차 감소: P95 지표가 2.94s에서 2.6s로 11.6% 개선되어 고부하 시의 튀는 응답(Spike)이 완화되었습니다.

- 안정성 향상: 커넥션 획득 실패로 인한 처리 실패 건수가 1,379건에서 1,044건으로 24.3% 감소했습니다.

- 처리 효율 극대화: 초당 요청 처리 속도(RPS)가 122.86으로 소폭 상승했으며, 전체 처리량(Throughput)은 12,150건에서 12,486건으로 약 2.8% 향상되었습니다.

<br>

---

# 10. 🚨 트러블 슈팅

## ECS Task Resource Reservation 설정 오류로 인한 배포 실패 및 메모리 경쟁 문제

### 문제

- 현상: 관리자 서버를 ECS on EC2 방식으로 배포 시, 새 태스크 정의(Task Definition)는 정상 생성되었으나 ECS 서비스가 태스크를 실행하지 못하고
  service admin was unable to place a task because no container instance met all of its requirements 오류를 반복함.

- 영향: 새로운 버전의 애플리케이션이 배포되지 않고 서비스가 중단되거나 이전 버전에 머무르는 현상이 발생함.

### 원인

- 가용 리소스 산정 오류: 사용 중인 EC2 인스턴스(t3.small)의 전체 메모리는 2GB였으나, 태스크 정의의 메모리 예약(Memory Reservation) 값 또한 2GB로 설정되어 있었습니다.

- OS 및 에이전트 점유 메모리 간과: ECS on EC2 환경에서는 호스트 OS(Linux), Docker 데몬, ECS Agent 등 시스템 운영에 필수적인 프로세스들이 일정량의 메모리를 상시 점유합니다.

- 스케줄링 실패: ECS 스케줄러는 (인스턴스 전체 메모리) - (시스템 점유 메모리)를 가용 메모리로 계산하는데, 설정된 예약값이 이 가용 범위를 초과하여 태스크를 배치할 수 있는 적절한 인스턴스를 찾지 못한 것입니다.

### 해결

- 리소스 예약값 최적화: 태스크 정의의 메모리 예약 값을 1GB로 하향 조정하여 시스템 운영을 위한 최소한의 메모리 마진(Buffer)을 확보했습니다.

- 수치 기반 설정: 로컬 환경 및 테스트 서버에서 docker stats와 Spring Boot Actuator를 통해 실제 애플리케이션의 Peak 메모리 사용량을 측정하고, 이에 기반하여 안전한 예약 값을 산출해 적용했습니다.

### 결과

- 배포 정상화: ECS 스케줄러가 EC2 인스턴스 내의 가용 메모리 범위를 인식하게 되어 태스크가 정상적으로 배치 및 실행되었습니다.

- OOM(Out Of Memory) 방지: 태스크가 사용할 리소스를 명시적으로 제한함으로써, 특정 컨테이너가 호스트의 모든 메모리를 점유하여 OS나 다른 핵심 프로세스가 강제 종료되는 메모리 경쟁 상황을 미연에 방지했습니다.

- 관측성 강화: CloudWatch와 Grafana를 통한 지속적인 메트릭 모니터링 체계를 구축하여, 향후 트래픽 증가에 따른 적정 리소스 크기를 데이터 기반으로 조정할 수 있는 기반을 마련했습니다.

<br>

---

## ECS Rolling 배포 중 RDS Connection Pool 고갈 해결

### 문제

- 현상: 채팅 서버 배포 시 GitHub Actions의 amazon-ecs-deploy-task-definition 스텝에서 10분 이상 지연되다가 TIMEOUT 발생과 함께 CD 실패.

- 영향: 신규 버전의 태스크가 실행되지 못하고 재시작을 반복하며, 무중단 배포(Rolling Update)가 완료되지 않아 서비스 안정화가 불가능해짐.

### 원인

- RDS 커넥션 한도 초과: RDS의 최대 커넥션 슬롯이 고갈되어 FATAL: remaining connection slots are reserved... 에러 발생.

- 임시 설정의 전파: 부하 테스트를 위해 고객 서버의 maximum-pool-size를 50으로 상향했던 설정이 유지되어 대량의 커넥션을 선점함.

- Rolling 배포의 특성: 무중단 배포 시 구버전 태스크와 신규 버전 태스크가 일시적으로 동시에 가동됩니다. 이때 두 버전의 태스크가 각각 설정된 최대 풀(Max Pool) 만큼 커넥션을 점유하려 시도하면서 RDS의 임계치를 초과하게 된 것입니다.

- 순환 오류: 커넥션을 확보하지 못한 신규 태스크가 Healthy 상태가 되지 못해 기존 태스크가 종료되지 않았고, 결과적으로 DB 커넥션 자원이 반납되지 않아 배포가 무한 루프에 빠짐.

### 해결

단계별 분석을 통해 애플리케이션 설정 최적화와 수동 자원 정리를 병행했습니다.

1. 커넥션 풀 사이즈 최적화: 모든 애플리케이션 서버의 hikari.maximum-pool-size를 10으로 하향 조정하여, 배포 시 여러 태스크가 동시에 떠 있어도 RDS 전체 한도를 넘지 않도록 여유분을 확보했습니다.

2. 임베딩 스토어 설정 개선: PgVectorEmbeddingStore가 별도의 커넥션을 생성하지 않고, 기존에 생성된 HikariDataSource를 주입받아 풀을 공유하도록 코드를 수정하여 불필요한 커넥션 낭비를 방지했습니다.

3. 수동 자원 회수: 이미 커넥션을 과도하게 점유 중인 기존 태스크를 강제 종료하여 RDS 커넥션을 즉시 확보한 후 재배포를 실행했습니다.

### 결과

- 배포 성공: RDS Connection 지표가 정상 범위로 회복되었으며, ECS 서비스 안정화 판단이 정상적으로 이루어져 모든 서버가 배포 완료되었습니다.

- 모니터링 강화: CloudWatch 경보와 Slack 알림을 통해 커넥션 고갈 징후를 사전에 포착할 수 있는 체계를 재확인했습니다.

- 인사이트 확보: 무중단 배포 시에는 '신구 버전의 자원 합계'가 인프라(DB, Memory 등)의 물리적 한계를 넘지 않아야 한다는 점을 학습하고, 배포 전략 수립 시 이를 필수 고려 사항으로 포함했습니다.

<br>

---

## ECS Container Instance의 클러스터 등록 실패 및 실행 시점 정합성 문제

### 문제

- 현상: EC2 User Data를 통해 ECS 클러스터 설정을 완료했음에도 불구하고, 생성된 EC2 인스턴스가 ECS 클러스터의 컨테이너 인스턴스(Container Instance) 목록에 나타나지 않음.

- 영향: ECS 서비스가 태스크를 배치할 컴퓨팅 리소스를 확보하지 못해 애플리케이션 배포 및 실행이 불가능한 상태가 됨.

### 원인

- 레이스 컨디션(Race Condition) 발생: EC2 부팅 시 systemd에 의해 관리되는 ECS Agent의 자동 시작 시점과 User Data 스크립트에 의해 설정 파일(/etc/ecs/ecs.config)이 생성되는 시점이 충돌함.

- 설정 참조 실패: ECS Agent가 실행되는 순간에 클러스터 이름이 명시된 설정 파일이 아직 존재하지 않거나 작성 중인 경우, 에이전트는 대상 클러스터를 찾지 못해 등록 프로세스를 정상적으로 완료하지 못함.

- 부팅 시점의 비동기성: User Data는 부팅 과정 중 실행되지만, systemctl enable된 서비스들의 시작 시점과 엄밀하게 동기화되지 않아 발생하는 전형적인 초기화 순서 문제임.

### 해결

설정 파일이 완전히 생성된 후 ECS Agent가 실행되도록 실행 시점에 지연 시간(Delay)을 부여했습니다.

1. 명시적 실행 지연: systemctl enable로 서비스 자동 시작만 설정해둔 뒤, User Data의 가장 마지막 단계에서 sleep 명령어를 조합해 에이전트 시작을 늦춤.

2. 백그라운드 실행 보장: nohup과 &를 사용하여 User Data 프로세스가 종료된 후에도 에이전트 시작 명령이 별도의 프로세스에서 안전하게 실행되도록 구성함.

    ```Bash
    # ECS Agent 활성화 (부팅 시 자동 시작 설정)
    systemctl enable ecs
    
    # 설정 파일 생성 완료를 기다린 후 에이전트 시작 (10초 지연)
    nohup bash -c 'sleep 10; systemctl start ecs' \
    > /var/log/ecs-start-later.log 2>&1 &
    ```

### 결과

- 클러스터 등록 성공: User Data에 의해 설정 파일이 확실히 생성된 후 ECS Agent가 구동됨으로써, EC2 인스턴스가 지정된 ECS 클러스터에 컨테이너 인스턴스로 정상 등록됨.

- 초기화 안정성 확보: 부팅 시 시스템 서비스와 커스텀 스크립트 간의 실행 순서 의존성 문제를 해결하여 인프라 프로비저닝의 신뢰성을 높임.

- 디버깅 체계 마련: ecs-start-later.log를 통해 에이전트의 지연 시작 과정을 기록함으로써 추후 발생할 수 있는 초기화 관련 이슈의 추적 가능성을 확보함.

<br>

---

## CloudWatch SEARCH() 표현식의 Dimension 스키마 불일치 문제 해결

### 문제

- 현상: CloudWatch Dashboard 구성을 위해 SEARCH() 표현식을 사용했으나, 지표 패널에 아무런 데이터가 출력되지 않거나 일부 지표가 누락되는 현상이 발생함.

- 영향: 실시간 애플리케이션 모니터링이 불가능해져 장애 감지 및 성능 분석에 차질이 생김.

### 원인

- Dimension 조합의 엄격성: CloudWatch Metrics는 지표를 저장할 때 사용된 Dimension의 전체 조합(Schema)이 조회 시의 조건과 정확히 일치해야 데이터를 반환합니다.

- 스키마 불일치: Micrometer(Spring Boot)가 전송한 실제 메트릭의 Dimension 스키마(예: method, status, uri 모두 포함)와 대시보드 쿼리에서 지정한 Dimension 목록이 서로 달라 검색 결과가 '0'으로 처리되었습니다.

- 추상화의 차이: CloudWatch는 저장된 데이터의 구조를 그대로 따라야 하는 반면, 사용자는 필요한 일부 Dimension만으로 필터링이 가능할 것이라고 오판한 것이 원인이었습니다.

### 해결

- 메트릭 스키마 전수 조사: CloudWatch Metrics 콘솔에서 실제로 수집되고 있는 메트릭의 구체적인 Dimension 조합을 먼저 확인했습니다.

- SEARCH() 표현식 정교화: 확인된 실제 스키마를 바탕으로 namespace와 dimension 목록을 수정하여 쿼리 정확도를 높였습니다.

- 비교 분석을 통한 최적화: Prometheus/Grafana 방식과의 비교를 통해 각 도구의 특성을 파악하고 상황에 맞는 쿼리 전략을 수립했습니다.

- 쿼리 비교 예시 (HTTP 요청 수 상태 코드별 집계)

  | 도구         | 쿼리 예시                                                                                                | 특징                                |
          |------------|------------------------------------------------------------------------------------------------------|-----------------------------------|
  | CloudWatch | SEARCH('{http_server_requests, method, status, uri} MetricName=""http_server_requests""', 'Sum', 60) | 엄격함: 저장된 모든 Dimension을 명시해야 조회 가능 |
  | Prometheus | sum by(status) (http_server_requests_seconds_count)                                                  | 유연함: Label 기반으로 필요한 지표만 선택적 집계 가능 |

### 결과

- 시각화 정상화: 수정된 SEARCH() 표현식을 통해 CloudWatch Dashboard에서 애플리케이션 지표가 실시간으로 정상 출력되었습니다.

- 모니터링 효율성 제고: AWS 리소스(ALB, RDS)는 CloudWatch로, 세밀한 애플리케이션 로직은 Prometheus/Grafana로 이원화하여 각 도구의 장점을 극대화한 모니터링 체계를 구축했습니다.

- 데이터 이해도 향상: CloudWatch의 엄격한 Dimension 구조를 이해하게 됨으로써, 향후 커스텀 메트릭 설계 시 발생할 수 있는 시행착오를 미연에 방지할 수 있게 되었습니다.

<br>

---

## Context Recall 0.9 기반 검색 품질 문제

### 문제

RAGAS 평가 중 Context Recall이 0.9로 측정되어, 정책 문서에 명확히 존재하는 정보임에도 검색하지 못하는 누락이 발생했다.

### 원인

Semantic Chunking은 인접한 텍스트 간의 임베딩 유사도를 기준으로 청크를 병합한다.
원본 문서에서 섹션 4(교환 신청 방법)의 마지막 문장 "반품 상품을 포장하여 택배로 발송합니다"와 섹션 5(교환 처리 기간)의 첫 문장 "교환 상품이 도착한 후..."는 둘 다 배송/도착 맥락을 가지고 있어 임베딩 유사도가 0.75로 측정됐다.
이 값이 SIMILARITY_THRESHOLD인 0.7을 초과하면서 두 섹션이 하나의 청크로 병합됐고, 그 결과 "교환 처리 기간"이라는 섹션 제목이 사라져 검색 시 매칭되지 않았다.

### 해결

임계값 조정이나 코드 레벨 강제 분리보다 문서 구조 자체를 명확히 하는 방향을 선택했다.
섹션 4의 "반품 상품"을 "교환 상품"으로 수정해 섹션 5와의 의미적 연결을 끊었고, 섹션 5에는 처리 완료 후 액션까지 포함한 내용을 보강해 독립적인 청크로 분리되도록 했다.
DB 재인제스천 후 "교환 처리 기간" 청크가 독립적으로 생성된 것을 확인했다.

### 결과

Context Recall이 0.90에서 1.00으로 개선되었고, 누락 답변이 0건으로 해소되었다. 평균 RAGAS 점수도 0.76에서 0.94로 24% 향상되었다.
코드가 아닌 입력 데이터의 품질을 개선하는 것이 더 근본적인 해결책이 될 수 있다는 점을 확인한 사례였다.

<br>

---

## 와일드카드 패턴 검색에서 인덱스를 사용할 수 없는 구조적 문제

### 문제

하이브리드 검색의 키워드 검색에서 `ILIKE '%keyword%'` 패턴을 사용하고 있었다.
선행 와일드카드로 인해 B-Tree 인덱스를 사용할 수 없어 전체 테이블 스캔이 발생하는 구조였고, 데이터가 증가할수록 응답 시간이 선형적으로 저하될 위험이 있었다.

### 원인

B-Tree 인덱스는 접두사 검색(`LIKE 'abc%'`)에만 효과적이고, `LIKE '%abc%'`와 같은 선행 와일드카드 패턴에서는 인덱스를 사용할 수 없다.
`EXPLAIN ANALYZE`결과에서`Seq Scan`이 발생하는 것을 확인했고, 현재는 데이터가 10개로 적어 차이가 없지만 데이터가 100만 건으로 증가하면 응답 시간이 5초 이상으로 늘어나는 구조적 문제였다.

### 해결

`pg_trgm` 확장과 GIN 인덱스를 도입했다. `pg_trgm`은 텍스트를 트리그램(3글자) 단위로 분해해 부분 매칭 검색을 최적화하고, GIN 인덱스는 역색인 구조로 `LIKE '%abc%'` 패턴 검색을 가속한다.
변경은 Flyway 마이그레이션(V17__add_trigram_index.sql)으로 버전 관리하여 적용했다.

- `CREATE EXTENSION IF NOT EXISTS pg_trgm`으로 확장을 설치했다.
- `USING gin(text gin_trgm_ops)`으로 GIN 인덱스를 생성했다.
- `ANALYZE`로 통계를 갱신한 뒤 `EXPLAIN ANALYZE`로 인덱스 사용 여부를 검증했다.

### 결과

데이터 규모가 커질수록 Seq Scan 대비 최대 100배의 성능 개선이 기대된다.
현재 데이터 규모에서는 차이가 없지만 데이터 증가에 강한 구조를 확보했고, Flyway를 통한 표준 절차로 DB 변경을 관리해 팀 협업과 버전 관리 측면에서도 안정성을 높였다.

<br>

---

## STOMP Subscribe 프레임에서 accessor.getUser() 가 null 이 되는 문제

### 문제

`CONNECT` 프레임에서는 `accessor.getUser()`가 정상적으로 존재했지만, 이후 `SUBSCRIBE` 프레임에서는 `null`로 확인되어 `convertAndSendToUser()`가 메시지를 전달할 세션을 식별하지 못할 가능성이 있었다.

### 원인

`CONNECT`와 `SUBSCRIBE`의 `sessionId`가 동일함을 확인해 재연결 문제는 아니었고, 같은 세션 안에서 `Principal`만 유지되지 않는 것이 문제였다.

- 기존 코드는 `StompHeaderAccessor.wrap(message)` 방식으로 accessor를 가져오고 있었다.
- 이 방식은 메시지에 실제로 연결된 accessor를 가져오는 것이 아니라 새 wrapper를 생성하기 때문에, `Principal`과 같은 session-bound header 상태가 이후 처리 흐름에 유지되지 않았다.

### 해결

`StompHeaderAccessor.wrap()` 대신 `MessageHeaderAccessor.getAccessor()`를 사용해 메시지에 이미 연결된 accessor를 직접 가져오도록 수정했다.

- `StompHeaderAccessor.wrap(message)` → `MessageHeaderAccessor.getAccessor(message, StompHeaderAccessor.class)` 로 변경했다.
- `accessor.setLeaveMutable(true)`를 추가하고, 변경된 헤더를 포함한 새 메시지를 반환하도록 수정했다.
- `UserPrincipal`의 `getName()`이 `convertAndSendToUser()`에서 사용하는 userId 문자열과 일치하도록 구현했다.

### 결과

`SUBSCRIBE` 프레임에서 사용자 정보가 정상적으로 유지되었고, 실시간 채팅 세션에 인증된 사용자 정보가 정상적으로 연결되어 특정 사용자에게 채팅 메시지를 전송할 수 있게 되었다.

<br>

---


# 11. 🏗️ Infra

## 시스템 아키텍처

- 고객 서버 / 채팅 서버 / 알림 서버는 ECS Fargate 기반으로 운영
- 관리자 서버는 ECS on EC2 방식으로 별도 운영
- ALB + Route53 + ACM 기반 HTTPS 구성
- RDS(PostgreSQL), ElastiCache(Redis) 기반 데이터 계층 구성
- CloudFront + S3 기반 상품 이미지 CDN 구성
- Terraform 기반 IaC로 전체 인프라 관리
- GitHub Actions + ECR + ECS 기반 CI/CD 자동화 구성
- CloudWatch + AMP + Grafana 기반 모니터링 구성

---

## 인프라 구성 요소

| 영역 | 사용 기술 |
|---|---|
| Container Orchestration | ECS Fargate / ECS on EC2 |
| Container Registry | ECR |
| Networking | VPC, Public/Private Subnet, NAT Gateway, ALB |
| Database | RDS PostgreSQL |
| Cache | ElastiCache Redis |
| CDN / Storage | CloudFront, S3 |
| DNS / HTTPS | Route53, ACM |
| IaC | Terraform |
| CI/CD | GitHub Actions |
| Monitoring | CloudWatch, Amazon Managed Prometheus, Grafana |
| Security | IAM, WAF, Security Group |

---

# 12. 🧩 인프라 설계 의도

## Terraform 기반 IaC로 인프라 관리

동일한 인프라 환경을 반복적으로 재현하고 Git 기반 형상 관리를 수행하기 위해 Terraform 기반 IaC 방식을 사용하였다.

기존 AWS Console 기반 수동 구축 방식은 빠르게 시작할 수 있다는 장점은 있었지만, 동일한 환경을 반복적으로 재현하기 어렵고 변경 이력을 체계적으로 관리하기 어렵다는 문제가 있었다.

Terraform을 선택한 이유는 다음과 같다.

- 선언형 방식 기반으로 현재 상태와 원하는 상태의 차이만 반영 가능
- Git 기반 버전 관리 및 코드 리뷰 가능
- AWS Provider 생태계가 잘 구축되어 있어 빠른 인프라 구성 가능
- 특정 클라우드 환경에 종속되지 않는 구조로 확장 가능

---

## ECS · EC2 · Fargate를 목적에 따라 분리 운영

고객 서버, 채팅 서버, 알림 서버는 ECS Fargate 방식으로 운영하였다.

선택 이유는 다음과 같다.

- 서버 운영 부담 감소
- OS 패치 및 Docker 런타임 관리 최소화
- 인프라 관리보다 애플리케이션 개발에 집중 가능
- 장애 범위를 애플리케이션 레벨로 축소 가능

반면 관리자 서버는 ECS on EC2 방식으로 운영하였다.

- 기존 ECS/ECR 기반 배포 코드 재사용 가능
- 하나의 ECS Cluster 내부에서 통합 관리 가능
- 관리자 서버 특성상 트래픽 변동성이 적어 Fargate보다 EC2가 비용 효율적이라고 판단

---

## Private Subnet 기반 애플리케이션 운영

ECS Task, RDS, Redis는 모두 Private Subnet 내부에서 운영하도록 구성하였다.

이를 통해:

- 외부에서 직접 접근 불가능
- ALB만 Public 접근 허용
- 내부 리소스 보안 강화
- NAT Gateway를 통한 Outbound 통신만 허용

구조로 설계하였다.

---

## CloudFront 기반 CDN 구성

상품 이미지 조회 성능 개선 및 Origin(S3) 부하 감소를 위해 CloudFront CDN을 구성하였다.

구성 목적:

- 사용자와 가까운 CDN 캐시 서버를 통한 이미지 응답 속도 개선
- 캐시 기반 Origin 요청 감소
- S3 트래픽 비용 절감

---

## WAF 기반 보안 구성

ALB 앞단에 WAF를 구성하여 비정상적인 요청을 제한하였다.

적용 정책 예시:

- Rate-Based Rule 기반 IP 요청 제한 (5분당 동일 IP 최대 1000회)
- 비정상적인 과도한 요청 차단
- ALB 레벨 트래픽 보호

---

# 13. 🚀 CI/CD

## 배포 파이프라인 구성

GitHub Actions 기반 CI/CD 파이프라인을 구성하였다.

배포 흐름:

```text
GitHub Push
    ↓
GitHub Actions 실행
    ↓
Docker Image Build
    ↓
ECR Push
    ↓
Task Definition 생성
    ↓
ECS Service Rolling Update
```

---

## 사용 기술

- GitHub Actions
- Docker
- ECR
- ECS
- OIDC 기반 AWS 인증

---

## OIDC 기반 AWS 인증 적용

GitHub Actions에서 AWS Access Key를 직접 저장하지 않고 OIDC 기반 AssumeRole 방식을 사용하였다.

이를 통해:

- 장기 Access Key 제거
- GitHub Secret 노출 위험 감소
- 최소 권한 기반 인증 가능

구조로 구성하였다.

---

## ECS Rolling Deployment 적용

ECS Rolling Deployment를 통해 무중단 배포를 구성하였다.

배포 시:

- 신규 Task 기동
- Health Check 통과
- 기존 Task 종료

순서로 서비스 중단 없이 배포되도록 구성하였다.

---

# 14. 📊 모니터링

## CloudWatch + Prometheus/Grafana 혼합 전략

인프라 리소스와 애플리케이션 메트릭 특성이 다르다고 판단하여 모니터링 시스템을 분리하였다.

---

## CloudWatch

CloudWatch는 다음 영역 모니터링에 사용하였다.

- ECS
- ALB
- RDS
- ElastiCache
- ECS Container Logs

AWS 리소스와 기본 연동이 자연스럽다는 장점이 있었다.

---

## Prometheus + Grafana

![Grafana](image/grafana.png)

Prometheus + Grafana는 애플리케이션 내부 메트릭 분석에 사용하였다.

수집 메트릭 예시:

- API 응답 시간
- HTTP 상태 코드 비율
- JVM Heap 사용량
- HikariCP 상태
- Thread 사용량

Prometheus는 PromQL 기반 Label 조회가 가능하여 CloudWatch보다 애플리케이션 메트릭 분석이 유연하고직관적이었다.

---

## Alert 시스템 구성

![CloudWatch](image/CloudWatch.png)

CloudWatch Alarm 기반 알림 시스템을 구성하였다.

주요 알림 항목:

- RDS Connection 사용률
- ECS CPU/Memory 사용률
- ALB 에러율
- 애플리케이션 ERROR 로그 발생율

Email, Slack 연동을 통해 실시간 장애 감지가 가능하도록 구성하였다.

---
