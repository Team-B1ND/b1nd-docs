---
description: Team-B1ND 커밋 컨벤션에 맞춰 커밋하고 원격 저장소에 푸시합니다
allowed-tools: Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(git status:*), Bash(git diff:*)
argument-hint: [스코프] (선택사항)
---

Team-B1ND 커밋 컨벤션에 맞춰 변경사항을 커밋하고 즉시 원격 저장소에 푸시해주세요.

## 커밋 컨벤션 규칙

다음 타입 중 하나를 **반드시** 사용하세요:

| Type | 설명 | 예시 |
|------|------|------|
| **feat** | 새로운 기능 추가 | feat: 백그라운드 푸시알람 구현 |
| **fix** | 버그 수정 | fix: 토큰 만료 처리 오류 수정 |
| **docs** | 레포지토리 내 문서 수정 | docs: 인증 api docs 업데이트 |
| **style** | 코드 포맷팅 (UI 아님!) | style: prettier 적용 |
| **refactor** | 코드 리팩토링 | refactor: 유저 서비스 책임 분리 |
| **chore** | 빌드, 설정 변경 | chore: netty socket 의존성 추가 |
| **perf** | 성능 개선 | perf: 캐싱 최적화 |
| **ci** | CI/CD 설정 | ci: git action workflow 추가 |
| **revert** | 커밋 되돌리기 | revert: feat: 푸시알림 구현 |
| **merge** | 브랜치 병합 | merge: main |

## 커밋 메시지 형식

```
<type>: <subject>
```

### Subject 작성 규칙
1. 한국어, 영어 모두 사용 가능
2. 띄어쓰기 사용 가능
3. 개조식으로 작성 (문장식 X)
4. 마침표나 쉼표 사용 금지
5. **50자 이내**로 작성

## 스코프 (선택사항)

스코프가 제공된 경우: `타입(스코프): 제목`

인자: $ARGUMENTS

## 좋은 예시
```
feat: 웹뷰 브릿지 카메라 API 구현
fix: 로그인 시 토큰 갱신 오류 수정
docs: 사용자 API 엔드포인트 문서 추가
refactor: 알림 서비스 MSA로 분리
```

## 나쁜 예시
```
추가 → type, subject 누락
feat: 기능 추가 → 너무 모호함
feat: 로그아웃 버튼 추가 #82 → 이슈번호 포함 금지
feat(mobile): 로그인 버튼 클릭했을 때 화면이 잘 나오도록 수정했어요. → 너무 김, 과거형
fix: bug fixed. → 구체적이지 않음, 마침표
```

## 작업 순서

1. `git status`로 변경된 파일 확인
2. `git diff`로 변경 내용 파악
3. 변경 내용 분석 후 적절한 타입 선택
4. 간결하고 명확한 커밋 메시지 작성 (50자 이내)
5. `git add`로 파일 스테이징
6. `git commit`으로 커밋 (HEREDOC 사용 필수)
7. `git push origin [현재브랜치]`로 원격 저장소에 푸시

## 커밋 단위

커밋은 `되돌려도 프로그램이 정상 작동하는 단위`로 주기적으로 해주세요.
- 기능 완료 후 한꺼번에 커밋 X
- 개발 과정에서 주기적으로 커밋 O

## 주의사항

- 제목은 개조식으로 작성 ("웹뷰 API 구현", "로그인 오류 수정")
- 제목 끝에 마침표 없음
- 한글/영어 모두 가능
- 여러 타입이 섞여있으면 커밋 분리 (`git add -p` 활용)
- 의미없는 메시지 금지 (ex: fix: asdsadasds)
- **main/develop 브랜치는 직접 push 금지** (PR 사용)

## FAQ
- **여러 파일, 다른 타입?** → 커밋 분리 (`git add -p`)
- **타입이 애매할 때?** → 가장 주요한 변경사항 기준
- **잘못 작성한 커밋?** → `git commit --amend` (Push 전만 가능)

커밋 및 푸시 후 성공 여부를 알려주세요.
