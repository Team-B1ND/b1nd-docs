# 이슈 템플릿

> Team-B1ND 통일 이슈 템플릿 가이드

## 📋 템플릿 개요

Team-B1ND는 **3가지 표준 이슈 템플릿**을 제공합니다:

1. **버그 리포트** - 버그 및 오류 보고
2. **기능 제안** - 새로운 기능 제안
3. **개선 제안** - 기존 기능 개선

## 🎯 이슈 템플릿의 목적

### 작성자 관점
- 무엇을 작성해야 할지 명확한 가이드
- 필수 정보 누락 방지
- 작성 시간 단축

### 관리자 관점
- 일관된 형식으로 빠른 이슈 파악
- 우선순위 판단에 필요한 정보 확보
- 자동 라벨링 및 분류 가능

## 📁 파일 위치

이슈 템플릿은 다음 위치에 생성합니다:

```
Team-B1ND/.github/
└── ISSUE_TEMPLATE/
    ├── bug_report.yml
    ├── feature_request.yml
    └── enhancement.yml
```

> **조직 레벨 템플릿**: `.github` 저장소에 생성하면 모든 프로젝트에 자동 적용

## 🐛 1. 버그 리포트 템플릿

### 사용 시점
- 기능이 예상대로 동작하지 않을 때
- 에러 메시지가 표시될 때
- 앱이 크래시되거나 멈출 때

### 템플릿 코드

**파일명**: `bug_report.yml`

```yaml
name: 버그 리포트
description: 버그나 오류를 발견하셨나요? 상세히 알려주세요.
title: "[Bug] "
labels: ["bug"]
assignees: []

body:
  - type: markdown
    attributes:
      value: |
        ## 버그 리포트 작성 가이드
        버그를 재현하고 수정하는데 필요한 정보를 자세히 작성해주세요.

  - type: dropdown
    id: platform
    attributes:
      label: 발생 플랫폼
      description: 버그가 발생한 플랫폼을 선택해주세요.
      options:
        - Web
        - Android
        - iOS
        - Server
        - 기타
    validations:
      required: true

  - type: textarea
    id: description
    attributes:
      label: 버그 설명
      description: 어떤 문제가 발생했는지 간단히 설명해주세요.
      placeholder: "예: 급식 박스를 클릭하면 앱이 강제 종료됩니다."
    validations:
      required: true

  - type: textarea
    id: steps
    attributes:
      label: 재현 방법
      description: 버그를 재현하는 단계를 순서대로 작성해주세요.
      placeholder: |
        1. 메인 화면에서 급식 메뉴를 탭합니다
        2. 급식 상세 페이지에서 알레르기 정보를 클릭합니다
        3. 앱이 멈춥니다
    validations:
      required: true

  - type: textarea
    id: expected
    attributes:
      label: 예상 동작
      description: 어떻게 동작해야 한다고 생각하시나요?
      placeholder: "예: 알레르기 정보 모달이 표시되어야 합니다."
    validations:
      required: true

  - type: textarea
    id: actual
    attributes:
      label: 실제 동작
      description: 실제로 어떻게 동작했나요?
      placeholder: "예: 앱이 강제 종료되었습니다."
    validations:
      required: true

  - type: textarea
    id: screenshots
    attributes:
      label: 스크린샷
      description: 가능하다면 스크린샷이나 화면 녹화를 첨부해주세요.
      placeholder: 이미지를 드래그하여 첨부할 수 있습니다.

  - type: input
    id: environment
    attributes:
      label: 환경 정보
      description: OS 버전, 앱 버전, 디바이스 모델 등
      placeholder: "예: Android 14, 도담도담 3.9.0, Galaxy S24"
    validations:
      required: false

  - type: textarea
    id: logs
    attributes:
      label: 로그 및 에러 메시지
      description: 관련된 로그나 에러 메시지가 있다면 첨부해주세요.
      render: shell

  - type: textarea
    id: additional
    attributes:
      label: 추가 정보
      description: 이 버그와 관련된 다른 정보가 있나요?
```

### 작성 예시

```markdown
발생 플랫폼: Android

버그 설명:
심야자습 신청 시 날짜 선택 캘린더가 과거 날짜를 선택할 수 있는 문제

재현 방법:
1. 심야자습 신청 메뉴 진입
2. 날짜 선택 버튼 클릭
3. 캘린더에서 어제 날짜 선택
4. 신청 버튼 클릭 시 에러 발생

예상 동작:
과거 날짜는 선택 불가능해야 하며, 최소 선택 가능 날짜는 오늘이어야 함

실제 동작:
과거 날짜 선택 가능하며, 서버에서 에러 응답 (400 Bad Request)

환경 정보:
Android 13, 도담도담 3.8.5, Galaxy S22
```

## ✨ 2. 기능 제안 템플릿

### 사용 시점
- 완전히 새로운 기능을 제안할 때
- 현재 없는 기능이 필요할 때

### 템플릿 코드

**파일명**: `feature_request.yml`

```yaml
name: 기능 제안
description: 새로운 기능을 제안해주세요!
title: "[Feature] "
labels: ["feature"]
assignees: []

body:
  - type: markdown
    attributes:
      value: |
        ## 기능 제안 가이드
        어떤 기능이 필요한지 자세히 설명해주세요.

  - type: dropdown
    id: platform
    attributes:
      label: 대상 플랫폼
      description: 어느 플랫폼에 적용될 기능인가요?
      options:
        - Web
        - Android
        - iOS
        - Server
        - 전체 플랫폼
        - 기타
      multiple: true
    validations:
      required: true

  - type: textarea
    id: feature-description
    attributes:
      label: 기능 설명
      description: 어떤 기능을 추가하고 싶으신가요?
      placeholder: "예: 외출 신청 시 동반 학생을 추가할 수 있는 기능"
    validations:
      required: true

  - type: textarea
    id: problem
    attributes:
      label: 해결하고자 하는 문제
      description: 이 기능이 왜 필요한가요? 어떤 불편함을 해결하나요?
      placeholder: "예: 현재는 여러 명이 함께 외출할 때 각자 신청해야 하는 불편함이 있습니다."
    validations:
      required: true

  - type: textarea
    id: solution
    attributes:
      label: 제안하는 해결 방법
      description: 어떻게 동작하면 좋을까요?
      placeholder: |
        예:
        1. 외출 신청 화면에 "동반 학생 추가" 버튼 표시
        2. 버튼 클릭 시 학생 검색 화면 표시
        3. 동반 학생 선택 후 추가
        4. 신청 시 동반 학생 정보도 함께 전송
    validations:
      required: true

  - type: textarea
    id: alternatives
    attributes:
      label: 대안
      description: 다른 방법으로 해결할 수 있는 방법이 있나요?
      placeholder: "예: 외출 신청 후 메시지로 동반 학생에게 알림"

  - type: textarea
    id: mockup
    attributes:
      label: 디자인 또는 참고 자료
      description: UI 스케치, 참고할 만한 다른 서비스 등

  - type: textarea
    id: additional
    attributes:
      label: 추가 정보
      description: 이 기능과 관련된 다른 정보가 있나요?
```

### 작성 예시

```markdown
대상 플랫폼: Web, Android, iOS

기능 설명:
기상송 신청 시 요일별 다른 곡 설정 기능

해결하고자 하는 문제:
현재는 한 주 동안 같은 기상송만 들을 수 있어서 지루합니다.
요일마다 다른 기상송을 듣고 싶다는 학생들의 요청이 많습니다.

제안하는 해결 방법:
1. 기상송 신청 화면에서 "요일별 설정" 탭 추가
2. 월~금 각 요일별로 곡 선택 가능
3. 기본값은 모든 요일 동일한 곡 (기존 방식)
4. 원하는 요일만 개별 설정 가능

대안:
여러 곡을 등록하고 랜덤 재생하는 방식
```

## 🔧 3. 개선 제안 템플릿

### 사용 시점
- 기존 기능의 개선이 필요할 때
- UI/UX를 더 좋게 만들고 싶을 때
- 성능 개선이 필요할 때

### 템플릿 코드

**파일명**: `enhancement.yml`

```yaml
name: 개선 제안
description: 기존 기능을 개선해주세요!
title: "[Enhancement] "
labels: ["enhancement"]
assignees: []

body:
  - type: markdown
    attributes:
      value: |
        ## 개선 제안 가이드
        기존 기능을 어떻게 개선하면 좋을지 알려주세요.

  - type: dropdown
    id: platform
    attributes:
      label: 대상 플랫폼
      description: 어느 플랫폼의 개선인가요?
      options:
        - Web
        - Android
        - iOS
        - Server
        - 전체 플랫폼
        - 기타
      multiple: true
    validations:
      required: true

  - type: dropdown
    id: category
    attributes:
      label: 개선 분야
      description: 어떤 분야의 개선인가요?
      options:
        - UI/UX
        - 성능
        - 접근성
        - 보안
        - 코드 품질
        - 문서
        - 기타
    validations:
      required: true

  - type: textarea
    id: current
    attributes:
      label: 현재 상황
      description: 현재 어떻게 동작하고 있나요?
      placeholder: "예: 급식 정보를 불러올 때 로딩 인디케이터가 없어서 응답이 느린지 알 수 없습니다."
    validations:
      required: true

  - type: textarea
    id: improvement
    attributes:
      label: 개선 제안
      description: 어떻게 개선하면 좋을까요?
      placeholder: "예: API 호출 중 스켈레톤 UI를 표시하여 로딩 상태를 명확히 전달"
    validations:
      required: true

  - type: textarea
    id: benefit
    attributes:
      label: 기대 효과
      description: 이 개선으로 얻을 수 있는 이점은 무엇인가요?
      placeholder: |
        예:
        - 사용자 경험 향상
        - 앱이 느리다는 오해 방지
        - 체감 속도 개선

  - type: textarea
    id: screenshots
    attributes:
      label: 참고 자료
      description: 스크린샷, 참고 링크, 디자인 시안 등

  - type: textarea
    id: additional
    attributes:
      label: 추가 정보
      description: 다른 정보가 있나요?
```

### 작성 예시

```markdown
대상 플랫폼: Android, iOS

개선 분야: UI/UX

현재 상황:
외출 신청 목록에서 승인/거절 상태를 색상으로만 구분하고 있습니다.
색맹 사용자나 어두운 화면에서는 구분이 어렵습니다.

개선 제안:
1. 승인: 초록색 + 체크 아이콘
2. 거절: 빨간색 + X 아이콘
3. 대기: 회색 + 시계 아이콘

기대 효과:
- 접근성 향상 (색맹 사용자 고려)
- 직관적인 상태 파악
- DDS 아이콘 컴포넌트 활용
```

## 🚀 템플릿 적용 방법

### 1. `.github` 저장소 생성 (조직 레벨)

```bash
# Team-B1ND/.github 저장소 생성
# GitHub에서 "New repository" → ".github" 이름으로 생성
```

### 2. 템플릿 파일 추가

```bash
# 로컬에서 작업
git clone https://github.com/Team-B1ND/.github.git
cd .github

# 폴더 생성
mkdir -p ISSUE_TEMPLATE

# 템플릿 파일 작성 (위 코드 복사)
# ISSUE_TEMPLATE/bug_report.yml
# ISSUE_TEMPLATE/feature_request.yml
# ISSUE_TEMPLATE/enhancement.yml

# 커밋 및 푸시
git add ISSUE_TEMPLATE/
git commit -m "feat: 이슈 템플릿 추가"
git push origin main
```

### 3. 개별 프로젝트에 적용 (선택)

특정 프로젝트만 다른 템플릿을 사용하려면:

```bash
# 프로젝트 저장소 내부에 생성
cd dodamdodam-web
mkdir -p .github/ISSUE_TEMPLATE
# 템플릿 파일 추가
```

> **우선순위**: 프로젝트 내 템플릿 > 조직 템플릿

### 4. 템플릿 테스트

1. GitHub 저장소 → Issues 탭
2. "New issue" 클릭
3. 템플릿 선택 화면 확인
4. 각 템플릿 작성 테스트

## 🏷️ 라벨 및 분류

### 기본 라벨

이슈 템플릿과 함께 사용할 라벨:

```yaml
bug:
  color: d73a4a
  description: 버그 또는 오류

feature:
  color: a2eeef
  description: 새로운 기능 제안

enhancement:
  color: 84b6eb
  description: 기존 기능 개선

documentation:
  color: 0075ca
  description: 문서 관련

question:
  color: d876e3
  description: 질문
```

### 플랫폼 라벨

```yaml
web:
  color: fbca04
  description: Web 플랫폼

android:
  color: 3DDC84
  description: Android 플랫폼

ios:
  color: 000000
  description: iOS 플랫폼

server:
  color: c5def5
  description: Server/Backend
```

### 우선순위 라벨

```yaml
priority: critical:
  color: b60205
  description: 최우선 해결 필요

priority: high:
  color: d93f0b
  description: 높은 우선순위

priority: medium:
  color: fbca04
  description: 중간 우선순위

priority: low:
  color: 0e8a16
  description: 낮은 우선순위
```

## 💡 실무 팁

### 1. 이슈 템플릿 선택 화면 커스터마이징

**config.yml** 추가:

```yaml
# .github/ISSUE_TEMPLATE/config.yml
blank_issues_enabled: false
contact_links:
  - name: 팀 채팅
    url: https://team-b1nd-chat-link
    about: 간단한 질문은 팀 채팅을 이용해주세요
  - name: 문서
    url: https://docs.team-b1nd.com
    about: 사용법은 문서를 참고해주세요
```

### 2. 자동 담당자 할당

**CODEOWNERS** 파일 활용:

```
# .github/CODEOWNERS
*.yml @team-b1nd/backend-team
*.tsx @team-b1nd/frontend-team
*.kt @team-b1nd/android-team
*.swift @team-b1nd/ios-team
```

### 3. 이슈 자동 관리

GitHub Actions로 자동화:

```yaml
# .github/workflows/issue-labeler.yml
name: Issue Labeler
on:
  issues:
    types: [opened]
jobs:
  label:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/labeler@v4
```

## 🤔 FAQ

### Q1. 템플릿이 너무 길어서 작성이 귀찮아요
**A**: 필수 항목만 채우고 선택 항목은 생략 가능합니다.

### Q2. 템플릿을 사용하지 않고 이슈를 작성하려면?
**A**: `config.yml`에서 `blank_issues_enabled: true` 설정

### Q3. 템플릿 수정 후 반영이 안 돼요
**A**: 브라우저 캐시 삭제 또는 시크릿 모드에서 확인

### Q4. 여러 플랫폼에 걸친 이슈는?
**A**: 대상 플랫폼에서 다중 선택 사용

### Q5. 기존 이슈에 템플릿 적용?
**A**: 기존 이슈는 수동으로 편집 필요

---

**다음 단계**: [PR 템플릿 보기](./04-pr-template.md)
