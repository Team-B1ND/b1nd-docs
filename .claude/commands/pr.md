---
description: Team-B1ND PR 템플릿에 맞춰 Pull Request를 생성합니다
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(gh pr create:*)
argument-hint: [타겟브랜치] (기본값: main)
---

Team-B1ND PR 템플릿에 맞춰 Pull Request를 생성해주세요.

## PR 템플릿 구조

```markdown
## 📝 변경 내용
(무엇을 변경했는지 간단히 요약)

## 🔗 관련 이슈
- Resolves #이슈번호

## 🧪 테스트 방법
- [ ] 단위 테스트 추가/수정
- [ ] 통합 테스트 완료
- [ ] 수동 테스트 완료

## 📸 스크린샷 (UI 변경 시)
(있다면 첨부)

## ✅ 체크리스트
- [ ] 코드가 프로젝트의 코딩 스타일을 따릅니다
- [ ] 자체 코드 리뷰를 완료했습니다
- [ ] 변경 사항에 대한 테스트를 추가했습니다
- [ ] 모든 테스트가 통과합니다
- [ ] 문서를 업데이트했습니다 (필요한 경우)
- [ ] Breaking Changes가 없습니다

## 💬 기타 사항
(리뷰어가 특별히 주의해서 봐야 할 부분)
```

## 작업 순서

1. 현재 브랜치와 변경 내용 확인
2. `git log` 또는 `git diff main...HEAD`로 모든 커밋 분석
3. 변경 내용을 명확하게 요약
4. PR 제목을 커밋 컨벤션에 맞춰 작성 (예: `feat: 심야자습 신청 기능 추가`)
5. 템플릿 각 섹션을 채워서 PR 생성
6. `gh pr create` 명령으로 PR 생성 (HEREDOC 사용)

## 인자

타겟 브랜치: $ARGUMENTS (기본값: main)

## PR 제목 형식

커밋 컨벤션과 동일:
- `feat: 제목`
- `fix: 제목`
- `design: 제목`
등

PR 생성 후 URL을 알려주세요.
