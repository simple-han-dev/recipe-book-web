# Recipe Book

레시피 관리 서비스를 위한 프론트엔드 웹 애플리케이션입니다.<br>
본 프로젝트는 단순한 CRUD 웹앱이 아니라,<br/>
확장성과 아키텍처 실험을 목적으로 한 포트폴리오 프로젝트입니다.

인프라 구축을 계획하고 **의도적으로 구조를 세분화하여 설계**했습니다.

## 프로젝트 목표

- 도메인 중심 설계를 프론트엔드에 적용
- UI / 비즈니스 / 공통 로직의 분리
- 확장성을 고려한 구조 설계

```
서비스 전환시 발생했던 구조적 문제를 고려하여 
유지보수와 확장성을 고려해 과잉설계로 보일 수 있습니다.
```

## Tech Stack

- Language: typescript
- Front-end: Nuxt
- Package Manager: pnpm
- Style: nuxt ui
- State: rxjs

## 디렉토리 구조 설계

| 경로 | 설명                                                   |
|:--|:-----------------------------------------------------|
| /domain | 비즈니스 도메인 레이어 (Entity/Core/Domain 공통 규격)              |
| /common | Front-end 공통 레이어 (DTO/VO/Enum/Utils/Model/Decorator) |
| /composables | 로직 조합 레이어 (Application Service/Adapter 역할)           |
| /components | 재사용 UI 컴포넌트 레이어 (표현 중심, 로직 최소화)                      |
| /pages | 라우팅 엔트리(화면 단위) — 페이지 조합 및 데이터 연결                     |
| /layouts | 페이지 공통 레이아웃(App Shell) — 헤더/푸터/네비 등                  |
| /middleware | 라우트 접근 제어/가드 (인증/인가/리다이렉트 정책)                        |
| /plugins | Nuxt 플러그인(외부 라이브러리/클라이언트 초기화)                        |
| /server | 서버 레이어(API route/서버 미들웨어)                            |
| /assets | 빌드 타임 자산(SCSS, 폰트 등)                                 |
| /public | 정적 파일(그대로 서빙되는 리소스)                                  |
| /observables | 전역 UI 이벤트 채널(RxJS 기반: modal/snackbar 등)              |
| /tasks | 개발/운영 스크립트 모음 (환경별 실행 작업)                            |
| /nuxt.config.ts | Nuxt 설정(모듈/빌드/런타임 설정)                                |

## 아키텍처

- **Hexagonal Architecture** 지향
    - `domain` 레이어를 중심으로 비즈니스 로직 구성
    - `composables`를 통해 프레임워크 및 외부 의존 로직을 흡수

- **Domain Driven Design(DDD)** 지향
    - 도메인 모델 중심의 구조 유지
    - UI/프레임워크 의존성을 도메인 레이어로부터 격리

- UX/UI는 변화가 잦아서 추상화가 독이 되는 경우가 많았음
  - 중복 제거(DRY) 보다 유지보수 비용을 우선하기로 함
  - 추상화는 규칙을 통해 승격하는 것을 고려하기로 함
  - domain 레벨에서는 중복을 허용하려 함