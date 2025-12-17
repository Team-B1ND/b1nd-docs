# 브랜치 전략

> Team-B1ND 통일 브랜치 관리 규칙

## 🌳 브랜치 전략 개요

Team-B1ND는 **Git Flow 기반의 간소화된 브랜치 전략**을 사용합니다.

### 핵심 원칙
1. **명확한 네이밍**: 브랜치 이름만으로 목적 파악 가능
2. **일관된 구조**: 모든 프로젝트에서 동일한 규칙 적용
3. **이슈 연동**: 브랜치명에 이슈 번호 포함 권장

## 📋 브랜치 유형

### 주요 브랜치 (Protected Branches)

#### 1. `main` - 프로덕션 브랜치
```
역할: 프로덕션 배포용 안정 버전
보호: 직접 커밋 금지, PR을 통해서만 병합
태그: 릴리스 시 버전 태그 생성
```

**특징**
- 항상 배포 가능한 상태 유지
- CI/CD 자동 배포 트리거
- 직접 push 금지 (브랜치 보호 규칙 적용)

#### 2. `develop` - 개발 통합 브랜치 (선택사항)
```
역할: 다음 릴리스를 위한 개발 브랜치
사용: 대규모 프로젝트에서 권장
병합: feature, fix 브랜치들이 병합됨
```

**특징**
- 개발 중인 기능들의 통합 환경
- 개발 서버 자동 배포
- 안정화 후 main으로 병합

> **Note**: 소규모 프로젝트는 `develop` 없이 `main`만 사용 가능

### 작업 브랜치 (Working Branches)

#### 3. `feature/` - 기능 개발
```bash
형식: feature/이슈번호-간단한설명
예시: feature/123-nightstudy-apply
     feature/456-meal-allergy-info
```

**용도**
- 새로운 기능 개발
- 사용자에게 영향을 주는 변경사항

**생명주기**
```bash
# 생성
git checkout -b feature/123-nightstudy-apply develop

# 작업 후 병합
PR 생성 → develop으로 병합 → 브랜치 삭제
```

#### 4. `fix/` - 버그 수정
```bash
형식: fix/이슈번호-간단한설명
예시: fix/234-login-token-error
     fix/567-meal-box-crash
```

**용도**
- 버그 수정
- 기존 기능의 오동작 해결

**생명주기**
```bash
# 생성 (develop 또는 main에서 분기)
git checkout -b fix/234-login-token-error develop

# 병합 후 삭제
```

#### 5. `hotfix/` - 긴급 수정
```bash
형식: hotfix/이슈번호-간단한설명
예시: hotfix/789-critical-server-error
     hotfix/101-payment-failure
```

**용도**
- 프로덕션 긴급 버그 수정
- 즉시 배포가 필요한 크리티컬 이슈

**생명주기**
```bash
# main에서 직접 분기
git checkout -b hotfix/789-critical-server-error main

# 수정 후 main과 develop 양쪽에 병합
PR → main 병합 → develop에도 병합
```

**특징**
- main에서 직접 분기
- 수정 후 main과 develop 양쪽 병합
- 버전 태그 생성

#### 6. `release/` - 릴리스 준비
```bash
형식: release/버전
예시: release/3.9.0
     release/2.1.0-beta
```

**용도**
- 릴리스 전 최종 테스트
- 버전 번호 업데이트
- 문서 정리

**생명주기**
```bash
# develop에서 분기
git checkout -b release/3.9.0 develop

# QA 후 main과 develop에 병합
PR → main 병합 → 태그 생성 → develop에도 병합
```

## 📝 브랜치 네이밍 규칙

### 기본 형식
```
타입/이슈번호-설명
```

### 상세 규칙

#### 1. 타입 (Type)
- **소문자** 사용: `feature`, `fix`, `hotfix`, `release`
- **단수형**: `features` (X) → `feature` (O)

#### 2. 이슈 번호
- GitHub 이슈 번호 포함 권장: `#123` (X) → `123` (O)
- 이슈 없는 경우 생략 가능: `feature/improve-performance`

#### 3. 설명 (Description)
- **kebab-case** 사용: 소문자 + 하이픈
- **간결하게**: 2-4단어 권장
- **명확하게**: 브랜치 목적이 드러나도록

### ✅ 좋은 예시

```bash
feature/123-nightstudy-apply          # 명확한 기능 설명
feature/456-oauth-login               # 간결하고 명확
fix/234-token-refresh-error           # 버그 내용 명시
fix/567-android-notification-crash    # 플랫폼 명시
hotfix/789-payment-api-timeout        # 긴급 이슈 명확
release/3.9.0                         # 버전 명시
```

### ❌ 나쁜 예시

```bash
Feature/123-nightstudy                # 대문자 사용 (X)
feature/s/123-apply                   # 불필요한 prefix (X)
origin/feature/123                    # 원격 브랜치명 혼동 (X)
feature/심야자습-신청                   # 한글 사용 피하기
fix/bug                               # 너무 모호함
feature-123-very-long-description-that-is-hard-to-read  # 너무 김
```

## 🔄 워크플로우

### 패턴 1: 기본 기능 개발 (main만 사용)

```bash
# 1. 이슈 생성 (#123)
# 2. 브랜치 생성
git checkout main
git pull origin main
git checkout -b feature/123-nightstudy-apply

# 3. 개발 및 커밋
git add .
git commit -m "feat: 심야자습 신청 폼 UI 구현"
git commit -m "feat: 심야자습 신청 API 연동"

# 4. 원격 푸시
git push origin feature/123-nightstudy-apply

# 5. PR 생성 (feature/123 → main)
# 6. 리뷰 및 병합
# 7. 로컬 브랜치 정리
git checkout main
git pull origin main
git branch -d feature/123-nightstudy-apply
```

### 패턴 2: develop 브랜치 사용

```bash
# 1. 브랜치 생성
git checkout develop
git pull origin develop
git checkout -b feature/456-meal-allergy

# 2. 개발
git commit -m "feat: 알레르기 정보 모델 추가"

# 3. PR 생성 (feature/456 → develop)
# 4. develop에서 충분히 테스트 후
# 5. release 브랜치 생성
git checkout -b release/3.9.0 develop

# 6. 버전 업데이트 및 QA
git commit -m "chore: 버전 3.9.0으로 업데이트"

# 7. PR 생성 (release/3.9.0 → main)
# 8. main 병합 후 태그 생성
git tag -a v3.9.0 -m "Release 3.9.0"
git push origin v3.9.0

# 9. develop에도 병합
git checkout develop
git merge main
```

### 패턴 3: 긴급 수정 (Hotfix)

```bash
# 1. main에서 브랜치 생성
git checkout main
git pull origin main
git checkout -b hotfix/789-critical-error

# 2. 수정 및 커밋
git commit -m "fix: 서버 크리티컬 오류 긴급 수정"

# 3. 즉시 테스트 후 PR 생성
# PR: hotfix/789 → main

# 4. main 병합 및 태그
git tag -a v3.8.1 -m "Hotfix 3.8.1"

# 5. develop에도 반영 (있다면)
git checkout develop
git merge main
```

## 🔐 브랜치 보호 규칙

### main 브랜치 보호 설정

GitHub 저장소 설정에서 다음 규칙 적용:

```yaml
Branch Protection Rules:
  - Branch name pattern: main
  - Require pull request reviews: 1명 이상
  - Require status checks to pass: ✅
    - CI/CD build
    - Unit tests
  - Require branches to be up to date: ✅
  - Include administrators: ✅
  - Restrict pushes: 직접 push 금지
  - Allow force pushes: ❌
  - Allow deletions: ❌
```

### develop 브랜치 보호 설정 (선택)

```yaml
Branch Protection Rules:
  - Branch name pattern: develop
  - Require pull request reviews: 1명 이상
  - Require status checks to pass: ✅
  - Allow force pushes: ❌
```

## 🏷️ 버전 태그 규칙

### Semantic Versioning 사용

```
v메이저.마이너.패치
```

**예시**
```bash
v3.9.0    # 새 기능 추가 (마이너 버전업)
v3.9.1    # 버그 수정 (패치 버전업)
v4.0.0    # Breaking change (메이저 버전업)
```

### 태그 생성 방법

```bash
# Annotated tag 생성 (권장)
git tag -a v3.9.0 -m "Release 3.9.0: 심야자습 신청 기능 추가"

# 원격 푸시
git push origin v3.9.0

# 모든 태그 푸시
git push origin --tags
```

### 태그 네이밍

```bash
v3.9.0           # 정식 릴리스
v3.9.0-beta      # 베타 버전
v3.9.0-rc.1      # Release Candidate
v3.9.0-alpha.2   # 알파 버전
```

## 💡 실무 팁

### 1. 브랜치 이름 자동 생성

GitHub CLI 활용:
```bash
# 이슈 생성 및 브랜치 자동 생성
gh issue create --title "심야자습 신청 기능" --body "..."
# 생성된 이슈 번호 확인 후
gh issue develop 123 --checkout
```

### 2. 작업 중인 브랜치 확인

```bash
# 로컬 브랜치 목록
git branch

# 원격 포함 모든 브랜치
git branch -a

# 최근 커밋 정보와 함께
git branch -v
```

### 3. 오래된 브랜치 정리

```bash
# 병합된 로컬 브랜치 삭제
git branch --merged | grep -v "main\|develop" | xargs git branch -d

# 원격에서 삭제된 브랜치 정리
git fetch --prune
```

### 4. 브랜치 이름 변경

```bash
# 로컬 브랜치명 변경
git branch -m old-name new-name

# 원격에도 반영
git push origin :old-name new-name
git push origin -u new-name
```

## 🤔 FAQ

### Q1. feature 브랜치는 언제 삭제하나요?
**A**: PR 병합 후 즉시 삭제합니다. GitHub에서 자동 삭제 설정 가능

### Q2. develop 브랜치를 꼭 사용해야 하나요?
**A**: 아니요. 소규모 프로젝트는 main만 사용해도 충분합니다.

### Q3. 브랜치명에 한글을 사용해도 되나요?
**A**: 기술적으로 가능하지만, 호환성을 위해 **영어 권장**

### Q4. 여러 이슈를 한 브랜치에서 작업하면?
**A**: 피하는 것이 좋습니다. 이슈별로 브랜치 분리 권장

### Q5. main에서 직접 작업한 경우?
**A**: 즉시 브랜치 생성 후 이동
```bash
git checkout -b feature/123-my-work
git push origin feature/123-my-work
```

## 📚 참고 자료

- [Git Flow 원문](https://nvie.com/posts/a-successful-git-branching-model/)
- [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow)
- [Semantic Versioning](https://semver.org/lang/ko/)

---

**다음 단계**: [이슈 템플릿 보기](./03-issue-templates.md)
