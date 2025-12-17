# 머지 규칙

> Team-B1ND 통일 머지 전략 및 코드 리뷰 가이드

## 🎯 머지 규칙 개요

Team-B1ND는 코드 품질 유지와 안전한 배포를 위해 체계적인 머지 규칙을 적용합니다.

### 핵심 원칙
1. **모든 코드는 리뷰를 거친다** - main 직접 push 금지
2. **테스트 통과 필수** - CI 통과 후 머지
3. **깔끔한 히스토리 유지** - Squash merge 권장

## 🔀 머지 방식

GitHub는 3가지 머지 방식을 제공합니다. Team-B1ND는 프로젝트 특성에 따라 선택합니다.

### 1. Squash and Merge (권장)

#### 개념
여러 커밋을 **하나의 커밋으로 합쳐서** main에 병합

```
Before:
feature/123 → [커밋1] [커밋2] [커밋3]

After:
main → [Squashed 커밋]
```

#### 장점
- ✅ **깔끔한 히스토리**: main 브랜치가 PR 단위로 정리됨
- ✅ **쉬운 롤백**: 문제 발생 시 하나의 커밋만 revert
- ✅ **명확한 변경**: PR 단위로 변경 사항 추적 용이

#### 단점
- ❌ **개별 커밋 소실**: feature 브랜치의 세부 커밋은 사라짐
- ❌ **기여도 집계**: 여러 공동 작업자가 있을 때 불편

#### 권장 프로젝트
- 대부분의 웹/앱 프로젝트
- 빠른 개발 사이클
- PR 단위 관리가 중요한 경우

#### 설정 방법
```yaml
# GitHub Repository Settings
Settings → General → Pull Requests
☑️ Allow squash merging
  Default to pull request title and description
```

#### 사용 예시
```bash
# PR #123: feat: 심야자습 신청 기능 추가
# 포함된 커밋:
# - feat: 신청 폼 UI 추가
# - feat: API 연동
# - fix: 날짜 검증 오류 수정
# - chore: 코드 리뷰 반영

# Squash merge 후:
git log --oneline
abc1234 feat: 심야자습 신청 기능 추가 (#123)
```

### 2. Rebase and Merge

#### 개념
feature 브랜치의 **모든 커밋을 순차적으로** main에 병합

```
Before:
feature/123 → [커밋1] [커밋2] [커밋3]

After:
main → [커밋1] [커밋2] [커밋3]
```

#### 장점
- ✅ **선형 히스토리**: 깔끔한 직선 커밋 히스토리
- ✅ **커밋 보존**: 모든 커밋이 main에 남음
- ✅ **상세 추적**: 세부 변경 사항 추적 가능

#### 단점
- ❌ **커밋 품질 의존**: 각 커밋이 의미 있어야 함
- ❌ **복잡한 롤백**: 여러 커밋을 개별적으로 revert 필요

#### 권장 프로젝트
- 오픈소스 프로젝트
- 커밋 히스토리가 중요한 경우
- 팀원들이 atomic commit에 익숙한 경우

### 3. Create a Merge Commit

#### 개념
feature 브랜치를 **머지 커밋으로** main에 병합

```
Before:
main → [A] → [B]
feature → [C] → [D]

After:
main → [A] → [B] → [Merge]
               ↘  [C] [D] ↗
```

#### 장점
- ✅ **완전한 히스토리**: 모든 브랜치 구조 보존
- ✅ **명확한 병합 지점**: 언제 어떤 기능이 병합됐는지 명확

#### 단점
- ❌ **복잡한 히스토리**: 머지 커밋으로 인한 복잡성
- ❌ **노이즈**: git log가 지저분해질 수 있음

#### 권장 프로젝트
- 대규모 프로젝트
- 여러 팀이 협업하는 경우
- 브랜치 히스토리 보존이 중요한 경우

## 🎨 Team-B1ND 권장 전략

### 프로젝트 유형별 권장사항

| 프로젝트 유형 | 권장 머지 방식 | 이유 |
|-------------|--------------|------|
| dodamdodam-web | Squash and Merge | 빠른 개발, PR 단위 관리 |
| dodamdodam-android | Squash and Merge | 앱 릴리스 단위 관리 |
| dodamdodam-ios | Squash and Merge | 앱 릴리스 단위 관리 |
| dodamdodam-server | Rebase and Merge | 세밀한 커밋 추적 필요 |
| dds-* | Rebase and Merge | 디자인 시스템 변경 추적 |

### 일반 원칙

```
✅ Squash and Merge를 기본으로 사용
❓ 특별한 이유가 있을 때만 다른 방식 고려
⚠️ Create Merge Commit은 최소화
```

## 🔐 브랜치 보호 규칙

### main 브랜치 설정

GitHub Repository Settings에서 다음 설정 적용:

```yaml
Branch Protection Rules for 'main':

Required Pull Request Reviews:
  ☑️ Require a pull request before merging
  ☑️ Require approvals: 1
  ☑️ Dismiss stale pull request approvals when new commits are pushed
  ☑️ Require review from Code Owners (선택)

Status Checks:
  ☑️ Require status checks to pass before merging
  ☑️ Require branches to be up to date before merging
  Required checks:
    - CI Build
    - Unit Tests
    - Lint

Additional Rules:
  ☑️ Require conversation resolution before merging
  ☑️ Require signed commits (선택)
  ☑️ Include administrators
  ☑️ Restrict who can push to matching branches
  ☐ Allow force pushes: ❌ 절대 금지
  ☐ Allow deletions: ❌ 절대 금지
```

### develop 브랜치 설정 (사용 시)

```yaml
Branch Protection Rules for 'develop':

Required Pull Request Reviews:
  ☑️ Require a pull request before merging
  ☑️ Require approvals: 1

Status Checks:
  ☑️ Require status checks to pass before merging
  Required checks:
    - CI Build
    - Unit Tests

Additional Rules:
  ☑️ Require conversation resolution before merging
  ☐ Include administrators (develop은 관리자 예외 허용)
```

## 👥 코드 리뷰 가이드

### 리뷰어 지정

#### 자동 지정
**CODEOWNERS** 파일 활용:

```
# .github/CODEOWNERS

# Backend
*.java @team-b1nd/backend-team
*.kt @team-b1nd/backend-team
*.rs @team-b1nd/backend-team

# Frontend
*.ts @team-b1nd/frontend-team
*.tsx @team-b1nd/frontend-team
*.vue @team-b1nd/frontend-team

# Android
*.kt @team-b1nd/android-team
**/android/** @team-b1nd/android-team

# iOS
*.swift @team-b1nd/ios-team
**/ios/** @team-b1nd/ios-team

# Design System
**/dds/** @team-lead @design-team

# Infrastructure
Dockerfile @team-b1nd/devops
*.yml @team-b1nd/devops
```

#### 수동 지정
```bash
# GitHub CLI로 리뷰어 지정
gh pr create --reviewer @username1,@username2

# 팀 지정
gh pr create --reviewer @team-b1nd/frontend-team
```

### 리뷰 체크리스트

#### 리뷰어가 확인할 사항

**기능 검증**
- [ ] PR 설명과 코드 변경이 일치하는가?
- [ ] 의도한 대로 동작하는가?
- [ ] 엣지 케이스를 고려했는가?
- [ ] Breaking Changes가 명시되어 있는가?

**코드 품질**
- [ ] 코딩 컨벤션을 준수하는가?
- [ ] 변수명, 함수명이 명확한가?
- [ ] 불필요한 주석이나 콘솔 로그가 없는가?
- [ ] 중복 코드가 없는가?
- [ ] 적절한 추상화 수준인가?

**테스트**
- [ ] 테스트가 충분한가?
- [ ] 테스트가 실제로 의미 있는 검증을 하는가?
- [ ] 모든 테스트가 통과하는가?

**보안**
- [ ] 민감한 정보(API 키, 비밀번호)가 노출되지 않는가?
- [ ] 입력 검증이 적절한가?
- [ ] SQL 인젝션, XSS 등 취약점은 없는가?

**성능**
- [ ] 불필요한 API 호출이 없는가?
- [ ] 메모리 누수 가능성은 없는가?
- [ ] 대용량 데이터 처리 시 성능 이슈는 없는가?

**문서**
- [ ] 복잡한 로직에 주석이 있는가?
- [ ] API 문서가 업데이트되었는가?
- [ ] README가 최신인가?

### 리뷰 코멘트 작성법

#### 효과적인 코멘트

**1. 구체적으로 작성**
```markdown
❌ 나쁜 예: "이 부분 수정 필요"
✅ 좋은 예: "null 체크가 필요합니다. user가 undefined일 경우 에러가 발생할 수 있습니다."
```

**2. 제안과 함께**
```markdown
💡 Suggestion:
\`\`\`typescript
// 현재 코드
if (user && user.name) {
  return user.name;
}

// 제안 코드
return user?.name ?? 'Unknown';
\`\`\`
```

**3. 우선순위 표시**
```markdown
🔴 Critical: 보안 이슈가 있습니다. 반드시 수정 필요
🟡 Minor: 개선하면 좋을 것 같습니다
💚 Nice: 좋은 접근입니다!
🤔 Question: 이 로직의 의도를 설명해주실 수 있나요?
```

**4. 칭찬도 함께**
```markdown
👍 깔끔한 리팩토링입니다!
💯 테스트 커버리지가 높네요!
⚡ 성능 개선 굿!
```

### 리뷰 응답 (PR 작성자)

```markdown
✅ 좋은 지적입니다. 수정했습니다. (abc1234)
🤔 의도는 ~입니다. 더 나은 방법이 있을까요?
📝 README에 설명을 추가했습니다.
⚠️ 이 부분은 다음 PR에서 처리하겠습니다. (#456)
```

## ⚡ 머지 프로세스

### 일반적인 머지 플로우

```
1. PR 생성
   ↓
2. CI/CD 실행 (자동)
   - 빌드
   - 린트
   - 테스트
   ↓
3. 코드 리뷰 요청
   ↓
4. 리뷰어 검토
   - 코멘트 작성
   - 변경 요청 or 승인
   ↓
5. 피드백 반영 (필요시)
   - 수정 커밋 push
   - 다시 리뷰
   ↓
6. 승인 완료 (Approved)
   ↓
7. 최종 확인
   - CI 통과 확인
   - 충돌 해결
   - 브랜치 업데이트
   ↓
8. Squash and Merge
   ↓
9. 브랜치 삭제 (자동)
   ↓
10. 배포 (자동/수동)
```

### 긴급 핫픽스 플로우

```
1. hotfix 브랜치 생성 (from main)
   ↓
2. 최소한의 수정
   ↓
3. 빠른 리뷰 (1명)
   ↓
4. 즉시 머지 및 배포
   ↓
5. develop에도 반영
```

## 🔧 머지 시 주의사항

### 1. 충돌 해결

```bash
# main 브랜치 최신화
git checkout main
git pull origin main

# feature 브랜치에 main 반영
git checkout feature/123-my-feature
git merge main

# 충돌 해결
# ... 파일 수정 ...

git add .
git commit -m "chore: merge main into feature/123"
git push origin feature/123-my-feature
```

### 2. 커밋 정리 (Squash 전)

불필요한 커밋이 많다면 로컬에서 정리:

```bash
# 최근 3개 커밋을 하나로 합치기
git rebase -i HEAD~3

# 에디터에서:
pick abc1234 feat: 기능 추가
squash def5678 fix: 오타 수정
squash ghi9012 chore: 리뷰 반영

# 저장 후 force push
git push origin feature/123 --force-with-lease
```

> ⚠️ **주의**: force push는 본인 브랜치에서만!

### 3. 대규모 PR 처리

```markdown
## 전략 1: Stacked PRs
feature/123-base
  ↓ PR #1
feature/123-part1
  ↓ PR #2
feature/123-part2

## 전략 2: Feature Flag
전체를 한 번에 머지하되, Feature Flag로 점진적 활성화
```

## 📊 머지 메트릭

### 추적할 지표

```yaml
Cycle Time:
  - PR 생성 → 첫 리뷰: 목표 4시간 이내
  - PR 생성 → 머지: 목표 1일 이내

Review Quality:
  - 리뷰어 수: 최소 1명
  - 코멘트 수: 평균 3-5개
  - 승인률: 90% 이상

PR Size:
  - 변경 라인 수: 300줄 이하 권장
  - 변경 파일 수: 10개 이하 권장
```

### GitHub Insights 활용

```
Settings → Insights → Pulse
- PR 머지 현황
- 리뷰 활동
- 기여자 통계
```

## 🤔 FAQ

### Q1. 리뷰 승인 없이 급하게 머지해야 하는 경우는?
**A**: 프로덕션 크리티컬 이슈인 경우에만 관리자 권한으로 가능. 단, 사후에 리뷰 진행 필수

### Q2. 리뷰어가 응답이 없으면?
**A**:
1. 24시간 대기
2. 다른 리뷰어에게 요청
3. 팀 채널에 리마인드

### Q3. 리뷰 의견에 동의하지 않으면?
**A**:
1. 이유를 명확히 설명
2. 대안 제시
3. 팀 토론으로 해결
4. 최종적으로는 리드의 결정을 따름

### Q4. 여러 사람이 동시에 같은 파일을 수정하면?
**A**:
1. 먼저 머지된 PR이 우선
2. 나중 PR은 충돌 해결 필요
3. 가능하면 사전에 조율

### Q5. Squash 후 feature 브랜치는 어떻게 되나요?
**A**: 자동으로 삭제됩니다. 로컬에서도 정리:
```bash
git branch -d feature/123
git fetch --prune
```

## 📚 참고 자료

- [GitHub: About pull request merges](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges)
- [Google: Code Review Guidelines](https://google.github.io/eng-practices/review/)
- [Thoughtbot: Code Review Guide](https://github.com/thoughtbot/guides/tree/main/code-review)

---

**다음 단계**: [도입 기대 효과 보기](./06-expected-benefits.md)
