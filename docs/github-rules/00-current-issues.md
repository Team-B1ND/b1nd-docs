# 현재 문제점 분석

> Team-B1ND GitHub 운영 현황 및 개선 필요 사항

## 📊 Team-B1ND 현황

### 조직 구성
- **총 멤버**: 30명
- **팀 구성**: 4개 팀
  - Android Team
  - Back-end Team
  - Front-end Team
  - iOS Team

### 주요 프로젝트
- **도담도담(dodamdodam)**: 스마트 스쿨 플랫폼
  - Server (Java/Spring Boot) - 19 stars
  - Web (TypeScript/React) - 22 stars
  - Android (Kotlin) - 24 stars
  - iOS (Swift) - 35 stars
- **DDS (Dodam Design System)**: 멀티플랫폼 디자인 시스템
- **DGIT**: GitHub 랭킹 서비스
- **DAuth**: 인증 시스템
- 기타 15개 이상의 활성 프로젝트

### 기술 스택
- **Backend**: Java, Kotlin, Rust
- **Frontend**: TypeScript, React, Vue
- **Mobile**: Kotlin (Android), Swift (iOS)

## 🔍 식별된 문제점

### 1. 커밋 메시지 일관성 부족

#### 현재 상황
프로젝트별로 다양한 커밋 패턴이 혼재되어 있습니다.

**dodamdodam-server (Java/Spring Boot)**
```
✅ 표준 패턴 사용
feat: delete
fix: night-study duplication check
chore: rollback

❌ 비표준 패턴 혼재
Merge pull request #324 from Team-B1ND/Feature/#323
```

**dodamdodam-web (TypeScript/React)**
```
❌ 일관성 없는 패턴
HOTFix :: 배포 버전 에러 고치기 위한 재배포
리프레쉬 에러 해결
fix :: refresh error
refactor :: bg-color cookie => localStorage
```

**dodamdodam-android (Kotlin)**
```
✅ 일부 표준 패턴 사용
fix: Add missing navigation parameters
chore: bump app version to 3.9.0

❌ 브랜치 정보 포함
Merge pull request #366 from Team-B1ND/develop
[Student] Release 3.9.0
```

#### 문제 분석
- **타입 불일치**: `feat`, `fix`, `HOTFix`, `Origin/feature` 등 다양한 표현 사용
- **언어 혼용**: 한글과 영어가 무분별하게 혼합
- **구분자 불일치**: `:`, `::`, 공백 등 다양한 구분자 사용
- **대소문자 불일치**: `feat` vs `Feat` vs `HOTFIX`

#### 영향
- 커밋 히스토리 검색 어려움
- 자동화 도구(CI/CD, changelog 생성) 적용 불가
- 신규 팀원 혼란

### 2. 이슈 템플릿 부재

#### 현재 상황
```bash
$ gh api repos/Team-B1ND/.github/contents
# 결과: profile/README.md만 존재
# ISSUE_TEMPLATE/ 폴더 없음
```

#### 문제 분석
- 이슈 작성 시 필수 정보 누락
- 버그 리포트에 재현 방법 미기재
- 플랫폼 정보(Web/Android/iOS/Server) 불명확
- 이슈 분류 및 라벨링 어려움

#### 실제 사례
팀원들이 이슈 작성 시 다음과 같은 정보가 자주 누락됩니다:
- 발생 환경 (OS, 버전, 디바이스)
- 재현 단계
- 예상 동작 vs 실제 동작
- 관련 로그나 스크린샷

### 3. PR 템플릿 불일치

#### 현재 상황

**dodamdodam-android PR 형식**
```markdown
## Overview (Required)
-  fix conflict

## Issue
- close #367
```

**dodamdodam-web PR 형식**
```markdown
##### 📘 한 내용
- 화면 모드 localstorage에 저장
- 리프레쉬 에러 완벽하게 고쳤습니다
```

**dodamdodam-server PR 형식**
```
(템플릿 없음, 자유 형식)
```

#### 문제 분석
- **플랫폼별 상이한 템플릿**: Android는 `## Overview`, Web은 `📘 한 내용`
- **필수 정보 누락**: 테스트 방법, 체크리스트 부재
- **일관성 부족**: 같은 팀원이 프로젝트를 옮길 때마다 다른 양식 학습 필요

#### 영향
- 리뷰어가 PR 내용 파악에 추가 시간 소요
- 중요 정보(breaking change, 테스트 여부) 누락
- 신규 기여자의 PR 작성 장벽 증가

### 4. 브랜치 전략 불명확

#### 현재 상황
다양한 브랜치 네이밍 패턴이 혼재:
```
✅ 의미 있는 패턴
feature/123-nightstudy
fix/456-meal-click-error

❌ 불명확한 패턴
feature/s/367-fix-conflict
origin/feature/encryption/#100
hotfix/#98 refresh token
```

#### 문제 분석
- 브랜치 네이밍 규칙 부재
- 이슈 번호 포함 여부 불일치
- `feature/s/`, `origin/feature/` 등 비표준 prefix 사용
- 브랜치 목적 파악 어려움

### 5. 코드 리뷰 프로세스 미정립

#### 현재 상황
- 브랜치 보호 규칙 설정 여부 불명확
- 최소 리뷰어 수 미지정
- 머지 방식(Squash/Rebase/Merge Commit) 통일 안 됨

#### 영향
- 리뷰 없이 main 브랜치 직접 수정 가능
- 코드 품질 관리 어려움
- 협업 문화 정착 저해

## 📈 정량적 분석

### 커밋 메시지 패턴 분석

최근 30개 커밋 분석 결과 (dodamdodam-web):

| 패턴 | 비율 | 예시 |
|-----|------|------|
| 표준 컨벤션 사용 | 20% | `fix :: refresh error` |
| 한글 자유 형식 | 45% | `리프레쉬 에러 해결` |
| 비표준 prefix | 25% | `HOTFix ::`, `Origin/feature` |
| Merge commit | 10% | `Merge pull request #...` |

### 프로젝트별 템플릿 현황

| 프로젝트 | 이슈 템플릿 | PR 템플릿 | CONTRIBUTING |
|---------|------------|-----------|--------------|
| dodamdodam-server | ❌ | ❌ | ❌ |
| dodamdodam-web | ❌ | ✅ (비공식) | ❌ |
| dodamdodam-android | ❌ | ✅ (비공식) | ❌ |
| dodamdodam-ios | ❌ | ❌ | ❌ |
| .github (org) | ❌ | ❌ | ❌ |

**결론**: 조직 레벨의 표준화된 템플릿이 전무합니다.

## 🎯 개선 필요 영역 요약

### 긴급 (High Priority)
1. **커밋 컨벤션 통일**: 즉시 적용 가능, 효과 큼
2. **브랜치 네이밍 규칙**: 프로젝트 관리 효율 증대

### 중요 (Medium Priority)
3. **PR 템플릿 표준화**: 리뷰 품질 향상
4. **이슈 템플릿 도입**: 이슈 관리 효율화

### 권장 (Low Priority)
5. **브랜치 보호 규칙**: 코드 품질 관리
6. **CONTRIBUTING 가이드**: 신규 기여자 온보딩

## 💡 해결 방향

본 건의안은 위 문제들을 다음과 같이 해결하고자 합니다:

1. **통일된 규칙 제공**: 모든 플랫폼에 적용 가능한 단일 규칙
2. **간결하고 실용적**: 복잡한 규칙보다는 쉽게 따를 수 있는 가이드
3. **점진적 도입**: 강제보다는 권장, 단계적 적용
4. **자동화 지원**: CI/CD 통합 가능한 구조

---

**다음 단계**: [커밋 컨벤션 제안 보기](./01-commit-convention.md)
