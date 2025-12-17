---
description: Team-B1ND 커밋 컨벤션에 맞춰 커밋하고 원격 저장소에 푸시합니다
allowed-tools: Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(git status:*), Bash(git diff:*)
argument-hint: [스코프] (선택사항)
---

Team-B1ND 커밋 컨벤션에 맞춰 변경사항을 커밋하고 즉시 원격 저장소에 푸시해주세요.

## 커밋 컨벤션 규칙

다음 타입 중 하나를 사용하세요:
- **feat**: 새로운 기능 추가
- **fix**: 버그 수정
- **design**: UI/UX 변경 (DDS 포함)
- **refactor**: 리팩토링
- **test**: 테스트 추가/수정
- **docs**: 문서 수정
- **chore**: 빌드, 설정 변경

## 커밋 메시지 형식

```
타입: 제목 (한글 50자 이내)

본문 (선택사항, 상세 설명)

푸터 (선택사항, 이슈 연결)
```

## 스코프 (선택사항)

스코프가 제공된 경우: `타입(스코프): 제목`

인자: $ARGUMENTS

## 작업 순서

1. `git status`로 변경된 파일 확인
2. `git diff`로 변경 내용 파악
3. 변경 내용 분석 후 적절한 타입 선택
4. 간결하고 명확한 커밋 메시지 작성
5. `git add`로 파일 스테이징
6. `git commit`으로 커밋 (HEREDOC 사용)
7. `git push origin [현재브랜치]`로 원격 저장소에 푸시

## 주의사항

- 제목은 명령문으로 작성 ("~함", "~추가")
- 제목 끝에 마침표 없음
- 한글 사용 권장
- 여러 파일 변경 시 원자적(atomic) 커밋 고려
- main/develop 브랜치는 직접 push 주의

커밋 및 푸시 후 성공 여부를 알려주세요.
