---
name: github-commit-convention
description: Team-B1ND 커밋 컨벤션을 자동으로 적용합니다. 사용자가 커밋 생성, 커밋 메시지 작성, 변경사항 커밋 등의 작업을 요청할 때 이 스킬을 사용하여 10가지 커밋 타입(feat, fix, docs, style, refactor, chore, perf, ci, revert, merge)과 subject 작성 규칙을 자동으로 준수하도록 합니다.
allowed-tools:
  - Bash
  - Read
  - Grep
---

# Team-B1ND GitHub 커밋 컨벤션

이 스킬은 Team-B1ND의 커밋 컨벤션을 자동으로 적용하여 일관된 커밋 메시지를 작성하도록 도와줍니다.

## 커밋 형식

```
<type>: <subject>
```

## 커밋 타입 (Type)

다음 10가지 타입 중 하나를 **반드시** 사용해야 합니다:

| Type | 설명 | 예시 |
|------|------|------|
| **feat** | 새로운 기능 추가 | feat: 백그라운드 푸시알람 구현 |
| **fix** | 버그 수정 | fix: 토큰 만료 처리 오류 수정 |
| **docs** | 레포지토리 내 문서 수정 | docs: 인증 api docs 업데이트 |
| **style** | 코드 포맷팅 (UI 아님!) | style: prettier 적용 |
| **refactor** | 코드 리팩토링 | refactor: 유저 서비스 책임 분리 |
| **chore** | 빌드, 설정 변경 (코드 로직 제외) | chore: netty socket 의존성 추가 |
| **perf** | 성능 개선 | perf: 캐싱 최적화 |
| **ci** | CI/CD 설정 | ci: git action workflow 추가 |
| **revert** | 커밋 되돌리기 | revert: feat: 푸시알림 구현 |
| **merge** | 브랜치 병합 | merge: main |

## Subject 작성 규칙

1. **한국어, 영어 모두 사용 가능**
2. **띄어쓰기 사용 가능**
3. **개조식으로 작성** (문장식 X)
   - ✅ "웹뷰 API 구현"
   - ❌ "웹뷰 API를 구현했습니다"
4. **마침표나 쉼표 사용 금지**
5. **50자 이내**로 작성
6. **명확하고 구체적**으로 작성

## 좋은 예시

```
feat: 웹뷰 브릿지 카메라 API 구현
fix: 로그인 시 토큰 갱신 오류 수정
docs: 사용자 API 엔드포인트 문서 추가
style: prettier 코드 포맷팅 적용
refactor: 알림 서비스 MSA로 분리
chore: Docker 환경 설정 추가
perf: 이미지 로딩 캐싱 최적화
ci: GitHub Actions 워크플로우 추가
```

## 나쁜 예시

```
❌ 추가 → type, subject 누락
❌ feat: 기능 추가 → 너무 모호함
❌ feat: 로그아웃 버튼 추가 #82 → 이슈번호 포함 금지
❌ feat(mobile): 로그인 버튼 클릭했을 때 화면이 잘 나오도록 수정했어요. → 너무 김, 과거형
❌ fix: bug fixed. → 구체적이지 않음, 마침표
```

## 커밋 단위

- 커밋은 `되돌려도 프로그램이 정상 작동하는 단위`로 주기적으로 수행
- 기능 완료 후 한꺼번에 커밋 ❌
- 개발 과정에서 주기적으로 커밋 ✅
- fix 타입은 예외

## 스킬 적용 시나리오

### 1. 커밋 메시지 작성 시
사용자가 "커밋해줘", "변경사항 커밋", "git commit" 등의 요청을 할 때:
- git diff로 변경 내용 분석
- 적절한 타입 자동 선택
- 50자 이내 명확한 subject 작성
- 개조식 형식 준수
- HEREDOC 사용하여 커밋 메시지 작성

### 2. 타입 선택 가이드

**feat vs fix**:
- feat: 새로운 기능이나 API 추가
- fix: 기존 기능의 버그나 오류 수정

**refactor vs perf**:
- refactor: 코드 구조 개선 (성능 변화 없음)
- perf: 성능 개선이 주 목적

**style vs refactor**:
- style: 코드 포맷팅만 변경 (prettier, eslint 등)
- refactor: 코드 로직 구조 변경

**chore vs ci**:
- chore: 빌드 도구, 패키지, 설정 파일 변경
- ci: CI/CD 파이프라인 관련 변경

### 3. 여러 타입이 섞인 경우
- 가장 주요한 변경사항 기준으로 타입 선택
- 또는 커밋 분리 제안 (`git add -p` 활용)

## FAQ

**Q: 여러 파일을 수정했는데 타입이 다르면?**
A: 커밋을 분리하세요. `git add -p`로 부분 스테이징 활용

**Q: 타입이 애매할 때는?**
A: 가장 주요한 변경사항을 기준으로 판단

**Q: 이미 잘못 작성한 커밋은?**
A: `git commit --amend`로 수정 (Push 전에만 가능)

## 자동 적용 프로세스

1. 변경 파일 분석 (`git status`, `git diff`)
2. 변경 내용의 성격 파악
3. 적절한 타입 자동 선택
4. 명확하고 구체적인 subject 작성 (50자 이내)
5. 개조식 형식으로 변환
6. 최종 검증 후 커밋 메시지 생성
