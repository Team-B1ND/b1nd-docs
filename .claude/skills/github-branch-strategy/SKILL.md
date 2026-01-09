---
name: github-branch-strategy
description: Team-B1ND 브랜치 전략 및 Git Flow를 자동으로 적용합니다. 사용자가 브랜치 생성, 브랜치 전환, Git Flow 작업 등을 요청할 때 이 스킬을 사용하여 브랜치 명명 규칙(feature, fix, refactor, hotfix, release)과 kebab-case subject 규칙을 자동으로 준수하도록 합니다.
allowed-tools:
  - Bash
  - Read
  - Grep
---

# Team-B1ND GitHub 브랜치 전략

이 스킬은 Team-B1ND의 Git Flow 기반 브랜치 전략을 자동으로 적용하여 일관된 브랜치 관리를 도와줍니다.

## 브랜치 구조 (Git Flow)

```
main (production)
  ↑
develop (staging)
  ↑
feature/*  (기능 개발)
fix/*      (기능 오류 수정)
refactor/* (기능 수정)
hotfix/*   (긴급 수정)
release/*  (릴리즈 준비)
```

## 브랜치 타입 설명

| 브랜치명 | 설명 | PR 대상 | 비고 |
|---------|------|---------|------|
| **main** | 프로덕션 서버 코드 | - | 직접 커밋 금지 |
| **develop** | 내부 개발 단계 코드 | - | 작은 프로젝트는 생략 가능 |
| **feature** | 기능 개발 | develop | 각 이슈 1:1 매핑 |
| **fix** | 기능 오류 수정 | develop | 각 이슈 1:1 매핑 |
| **refactor** | 기능 수정/개선 | develop | 각 이슈 1:1 매핑 |
| **hotfix** | 긴급 오류 해결 | main, develop | 예외적으로 양쪽 가능 |
| **release** | 제품 릴리즈 준비 | main | 필요한 프로젝트만 사용 |

**중요**: main, develop을 제외한 모든 브랜치는 **하나의 이슈와 1:1 매핑**되어야 합니다.

## 브랜치 명명 규칙

### 기본 형식

```
<branchname>/#<number>-<subject>
```

### 컴포넌트 설명

**1. branchname** - 브랜치 타입
- feature, fix, refactor, hotfix, release 중 하나

**2. number** - 이슈 번호
- 해당 브랜치의 이슈 번호 (# 포함)
- release는 예외: `v` 사용 (예: `release/v2.0.0`)

**3. subject** - 작업 설명
- **영어만 사용 가능** (한국어 불가)
- **kebab-case 필수** (단어를 하이픈으로 연결)
- **소문자만 사용** (대문자 불가)
- **띄어쓰기 불가**
- **단어로 짧게** 작성 (문장 형식 X)
- **마침표 사용 금지**

## 좋은 예시

```
feature/#123-webview-camera-bridge
feature/#456-push-notification-system
fix/#234-login-token-refresh
refactor/#567-alarm-service-msa
hotfix/#789-critical-auth-bug
release/v2.0.0
```

## 나쁜 예시

```
❌ Feature/#123-test → 대문자 사용, 너무 모호함
❌ feature/345-background-worker → # 미포함
❌ feature/#123-카메라API → 한국어 사용
❌ feature/#123-Camera_API → 대문자, snake_case 사용
❌ feature/#123-implement-camera-api-for-webview. → 너무 김, 마침표
❌ release/#2.0.0 → release는 v 사용
```

## 스킬 적용 시나리오

### 1. 브랜치 생성 요청 시

사용자가 "브랜치 만들어줘", "새 브랜치 생성", "feature 브랜치" 등을 요청할 때:
1. 브랜치 타입 확인 (feature, fix, refactor, hotfix, release)
2. 이슈 번호 확인
3. subject를 kebab-case로 자동 변환
4. 브랜치명 검증 (영어, 소문자, 하이픈만)
5. `git checkout -b` 명령 실행

### 2. Subject 자동 변환

**한글 → 영어 자동 번역** (필요시):
```
"카메라 API" → "camera-api"
"로그인 토큰" → "login-token"
"푸시 알림 시스템" → "push-notification-system"
```

**kebab-case 자동 적용**:
```
"Camera API" → "camera-api"
"Login Token Refresh" → "login-token-refresh"
"background_worker" → "background-worker"
```

### 3. 브랜치 타입 선택 가이드

**feature vs fix**:
- feature: 새로운 기능 추가
- fix: 기존 기능의 버그 수정

**fix vs hotfix**:
- fix: 일반 버그 수정 (develop에 PR)
- hotfix: 프로덕션 긴급 수정 (main에 PR)

**feature vs refactor**:
- feature: 완전히 새로운 기능
- refactor: 기존 기능 개선/구조 변경

### 4. Git Flow 작업 흐름

**일반 기능 개발**:
```
develop → feature/#123-new-feature → (PR) → develop
```

**버그 수정**:
```
develop → fix/#456-bug-fix → (PR) → develop
```

**긴급 수정 (hotfix)**:
```
main → hotfix/#789-critical-fix → (PR) → main, develop
```

**릴리즈**:
```
develop → release/v2.0.0 → (PR) → main
```

## 브랜치 검증 체크리스트

브랜치 생성 시 자동으로 다음을 검증합니다:

- ✅ 브랜치 타입이 올바른가? (feature, fix, refactor, hotfix, release)
- ✅ 이슈 번호가 포함되어 있는가? (release 제외)
- ✅ subject가 kebab-case인가?
- ✅ subject에 대문자가 없는가?
- ✅ subject에 한글이 없는가?
- ✅ subject에 띄어쓰기가 없는가?
- ✅ subject가 너무 길지 않은가?
- ✅ subject에 마침표가 없는가?

## 자동 적용 프로세스

1. 사용자 요청 분석 (브랜치 생성, 전환 등)
2. 브랜치 타입 결정
3. 이슈 번호 확인
4. subject를 kebab-case로 변환
5. 브랜치명 검증
6. 검증 통과 시 브랜치 생성/전환
7. 검증 실패 시 규칙 안내 및 재입력 요청

## 소규모 프로젝트 예외

기여자가 1-2명인 작은 프로젝트는 develop 브랜치를 생략할 수 있습니다:

```
main
  ↑
feature/* → (PR) → main
fix/* → (PR) → main
```

프로젝트가 커지면 develop 브랜치를 추가하세요.
