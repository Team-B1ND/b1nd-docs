# 커밋 컨벤션

> Team-B1ND 통일 커밋 메시지 작성 규칙

## 📋 기본 원칙

### 1. 간결하고 명확하게
커밋 메시지는 **무엇을 왜 변경했는지** 한눈에 알 수 있어야 합니다.

### 2. 일관된 형식 사용
모든 프로젝트(Web/Android/iOS/Server)에서 동일한 형식을 사용합니다.

### 3. 한글 사용 권장
팀 내부 프로젝트이므로 **한글**로 작성하여 이해도를 높입니다.

## 📝 커밋 메시지 형식

### 기본 구조
```
타입: 제목

본문 (선택사항)

푸터 (선택사항)
```

### 상세 규칙

#### 제목 (Title)
```
타입: 변경 내용 요약
```

- **타입**: 소문자로 작성
- **구분자**: 콜론(`:`) 뒤 공백 1칸
- **제목**: 한글 또는 영어, 50자 이내
- **마침표 없음**: 제목 끝에 마침표(`.`) 사용하지 않음
- **명령문 사용**: "~했음" (X) → "~함" (O)

#### 본문 (Body) - 선택사항
```
- 변경한 이유
- 어떻게 문제를 해결했는지
- 주의할 점이나 side effect
```

- 제목과 본문 사이 **빈 줄 1줄** 필수
- 72자마다 줄바꿈 권장
- 상세한 설명이 필요한 경우에만 작성

#### 푸터 (Footer) - 선택사항
```
Resolves: #이슈번호
See also: #관련이슈
```

- 이슈 트래커 연동
- Breaking Changes 명시

## 🏷️ 커밋 타입 (Type)

Team-B1ND는 다음 **7가지 타입**을 사용합니다.

### 1. `feat` - 기능 추가

새로운 기능을 추가하는 경우

```bash
feat: 심야자습 신청 기능 추가
feat: 급식 알레르기 정보 표시 기능 구현
feat: 외출 신청 시 사유 입력 필드 추가
```

**범위**: 사용자에게 영향을 주는 새 기능

### 2. `fix` - 버그 수정

버그나 오류를 수정하는 경우

```bash
fix: 급식 박스 클릭 시 닫히는 오류 수정
fix: 로그인 시 토큰 갱신 실패 문제 해결
fix: Android 13에서 알림 권한 요청 오류 수정
```

**범위**: 기존 기능의 오동작 수정

### 3. `design` - UI/UX 변경

디자인 시스템 적용, 레이아웃 변경, 스타일 개선

```bash
design: 로그인 페이지 레이아웃 개선
design: DDS 버튼 컴포넌트 적용
design: 다크모드 색상 팔레트 수정
```

**범위**: UI/UX 관련 변경 (DDS 관련 작업 포함)

### 4. `refactor` - 리팩토링

기능 변경 없이 코드 구조 개선

```bash
refactor: 사용자 인증 로직 함수 분리
refactor: API 응답 처리 유틸 모듈화
refactor: 중복 코드 제거 및 함수 통합
```

**범위**: 동작은 동일하나 코드 품질 향상

### 5. `test` - 테스트 추가/수정

테스트 코드 작성 및 수정

```bash
test: 로그인 API 통합 테스트 추가
test: 외출 신청 유효성 검증 단위 테스트 작성
test: E2E 테스트 시나리오 업데이트
```

**범위**: 테스트 코드 관련 변경

### 6. `docs` - 문서 수정

README, API 문서, 주석 등 문서 작업

```bash
docs: API 엔드포인트 문서 업데이트
docs: 프로젝트 README 기여 가이드 추가
docs: 컴포넌트 사용법 주석 작성
```

**범위**: 코드 외 문서 관련 변경

### 7. `chore` - 기타 작업

빌드, 설정, 의존성 등 기타 변경사항

```bash
chore: Gradle 버전 8.0으로 업그레이드
chore: ESLint 규칙 추가
chore: CI/CD 파이프라인 스크립트 수정
```

**범위**: 비즈니스 로직과 무관한 작업

## 🎯 스코프 (Scope) - 선택사항

대규모 프로젝트나 모노레포에서 **변경 범위를 명시**할 때 사용합니다.

### 형식
```
타입(스코프): 제목
```

### 예시

**모듈별 스코프**
```bash
feat(student): 외출 신청 기능 추가
feat(teacher): 학생 목록 조회 기능 추가
fix(admin): 권한 검증 로직 오류 수정
```

**플랫폼별 스코프** (멀티플랫폼 프로젝트)
```bash
feat(android): FCM 푸시 알림 구현
feat(ios): 로컬 알림 스케줄링 추가
fix(web): 반응형 레이아웃 깨짐 수정
feat(server): 외출 신청 API 추가
```

**기능별 스코프**
```bash
feat(auth): OAuth 로그인 추가
fix(meal): 급식 정보 로딩 오류 수정
design(nightstudy): 심야자습 신청 화면 개선
```

### 스코프 사용 권장 사항

- **사용 필수 아님**: 명확하지 않으면 생략 가능
- **일관성 유지**: 프로젝트 내에서 동일한 스코프명 사용
- **간결하게**: 3-10자 내외의 짧은 이름

## ✅ Good Examples

### 기본 형식
```bash
feat: 기상송 신청 마감 시간 자동 계산 기능 추가
fix: 외출 신청 시 날짜 검증 로직 오류 수정
design: 메인 페이지 카드 레이아웃 DDS 적용
refactor: API 에러 핸들링 로직 개선
test: 심야자습 신청 검증 로직 테스트 추가
docs: 기여 가이드라인 문서 작성
chore: React 18로 업그레이드
```

### 본문 포함
```bash
feat: 외출 신청 시 급식 여부 선택 기능 추가

수요일 외출 신청 시 급식 수요조사를 함께 진행할 수 있도록
급식 여부 체크박스를 추가했습니다.

- 외출 신청 폼에 급식 체크박스 추가
- 급식 여부에 따른 API 파라미터 전송
- 선택 여부를 로컬 스토리지에 저장

Resolves: #234
```

### 스코프 사용
```bash
feat(android): 생체 인증 로그인 지원
fix(server): JWT 토큰 갱신 시 만료 시간 오류 수정
design(ios): 메인 탭바 아이콘 변경
```

### Breaking Change
```bash
feat!: 인증 API 버전 2.0 적용

BREAKING CHANGE:
기존 /api/v1/auth 엔드포인트가 /api/v2/auth로 변경되었습니다.
모든 클라이언트는 새로운 API를 사용해야 합니다.
```

## ❌ Bad Examples

### 피해야 할 패턴

```bash
❌ HOTFix :: 배포 오류 수정
   → fix: 배포 오류 수정

❌ Update: API 수정함
   → fix: API 응답 오류 수정

❌ 리프레쉬 에러 해결
   → fix: 토큰 갱신 실패 오류 수정

❌ origin/feature/#100
   → (브랜치명은 커밋 메시지가 아님)

❌ feat :: 로그인 기능 추가했음.
   → feat: 로그인 기능 추가

❌ Feat: Add login feature (대문자 타입)
   → feat: 로그인 기능 추가

❌ feat:로그인추가 (공백 없음)
   → feat: 로그인 기능 추가
```

### 흔한 실수

1. **타입 대문자 사용**: `Feat:` (X) → `feat:` (O)
2. **구분자 불일치**: `feat ::`, `feat-` (X) → `feat:` (O)
3. **과거형 사용**: `feat: 로그인 추가했음` (X) → `feat: 로그인 추가` (O)
4. **애매한 제목**: `feat: 수정`, `fix: 오류` (X)
5. **너무 긴 제목**: 50자 초과 시 본문으로 이동

## 🔧 실무 적용 가이드

### 1. 첫 커밋부터 바로 적용

```bash
# 나쁜 예
git commit -m "update"

# 좋은 예
git commit -m "feat: 외출 신청 검증 로직 추가"
```

### 2. 원자적(Atomic) 커밋

하나의 커밋은 **하나의 논리적 변경**만 포함해야 합니다.

```bash
# 나쁜 예: 여러 작업을 한 커밋에
git commit -m "feat: 로그인 추가, 버그 수정, 문서 업데이트"

# 좋은 예: 작업별로 분리
git commit -m "feat: 로그인 기능 추가"
git commit -m "fix: 로그인 토큰 검증 오류 수정"
git commit -m "docs: 로그인 API 문서 작성"
```

### 3. 커밋 메시지 템플릿 설정 (선택사항)

```bash
# Git 커밋 템플릿 설정
git config commit.template ~/.gitmessage

# ~/.gitmessage 파일 내용
# 타입: 제목 (50자 이내)
#
# 본문 (선택사항, 72자마다 줄바꿈)
#
# Resolves: #이슈번호
```

### 4. IDE/에디터 플러그인 활용

- **VSCode**: Conventional Commits 확장 프로그램
- **IntelliJ/Android Studio**: Git Commit Template 플러그인
- **Vim**: Fugitive + 커스텀 매핑

## 📚 참고 자료

본 컨벤션은 다음 표준을 참고하여 Team-B1ND에 최적화했습니다:

- [Conventional Commits](https://www.conventionalcommits.org/)
- [Angular Commit Guidelines](https://github.com/angular/angular/blob/main/CONTRIBUTING.md)
- [Udacity Git Commit Message Style Guide](https://udacity.github.io/git-styleguide/)

## 🤔 FAQ

### Q1. 여러 파일을 수정했는데 타입이 다르면?
**A**: 커밋을 분리하세요. `git add -p`로 부분 스테이징 활용

### Q2. 타입이 애매할 때는?
**A**: 가장 주요한 변경사항을 기준으로 판단

### Q3. 이미 잘못 작성한 커밋은?
**A**: `git commit --amend`로 수정 (Push 전에만 가능)

### Q4. 영어로 작성해도 되나요?
**A**: 가능하지만, 팀 내 일관성을 위해 **한글 권장**

### Q5. 기존 프로젝트는 언제부터 적용?
**A**: 새로운 커밋부터 바로 적용, 과거 커밋은 수정 불필요

---

**다음 단계**: [브랜치 전략 보기](./02-branch-strategy.md)
