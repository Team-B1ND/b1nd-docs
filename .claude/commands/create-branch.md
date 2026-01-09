---
description: Team-B1ND 브랜치 규칙에 맞춰 브랜치를 생성하고 체크아웃합니다
allowed-tools: Bash(git branch:*), Bash(git checkout:*), Bash(git status:*)
argument-hint: <type> <issue-number> <subject>
---

Team-B1ND 브랜치 규칙에 맞춰 새 브랜치를 생성해주세요.

## 브랜치 형식

```
<branchname>/#<number>-<subject>
```

## 브랜치 타입

| 타입 | 용도 | PR 대상 |
|------|------|---------|
| **feature** | 새로운 기능 개발 | develop |
| **fix** | 기능 오류 수정 | develop |
| **refactor** | 기능 수정/개선 | develop |
| **hotfix** | 긴급 오류 수정 | main, develop |
| **release** | 제품 릴리즈 준비 | main |

## Subject 작성 규칙

1. **영어만 사용** (한국어 불가)
2. **kebab-case 필수** (단어를 하이픈(-)으로 연결)
3. **소문자만 사용** (대문자 불가)
4. **띄어쓰기 불가**
5. **단어로 짧게** 작성 (문장 형식 X)
6. **마침표 사용 금지**

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
Feature/#123-test → 대문자 사용, 너무 모호함
feature/345-background-worker → # 미포함
feature/#123-카메라API → 한국어 사용
feature/#123-Camera_API → 대문자, snake_case 사용
feature/#123-implement-camera-api-for-webview. → 너무 김, 마침표
release/#2.0.0 → release는 v 사용
```

## 인자

- **브랜치 타입**: $1 (feature, fix, refactor, hotfix, release)
- **이슈 번호**: $2 (숫자만, # 제외)
- **설명**: $3 (kebab-case 영어 단어)

전체 인자: $ARGUMENTS

## 작업 순서

1. 인자 파싱 (타입, 이슈번호, 설명)
2. **subject 검증**:
   - kebab-case 형식인지 확인
   - 소문자만 사용했는지 확인
   - 한글이 포함되지 않았는지 확인
   - 마침표가 없는지 확인
3. 브랜치명 생성:
   - release가 아닌 경우: `<type>/#<number>-<subject>`
   - release인 경우: `release/v<version>`
4. `git checkout -b <브랜치명>` 실행
5. `git status`로 브랜치 생성 확인

## 주의사항

- **release 브랜치**는 `release/v2.0.0` 형식으로 생성 (# 사용 안 함)
- **hotfix 브랜치**는 main 또는 develop 모두에 PR 가능
- 모든 브랜치는 **하나의 이슈와 1:1 매핑**
- 브랜치명이 규칙에 맞지 않으면 생성 거부

브랜치 생성 후 성공 여부와 브랜치명을 알려주세요.
