# Pull Request 템플릿

> Team-B1ND 통일 PR 작성 가이드

## 📋 템플릿 개요

Team-B1ND의 모든 프로젝트(Web/Android/iOS/Server)에서 사용하는 **통일된 PR 템플릿**을 제공합니다.

## 🎯 PR 템플릿의 목적

### 작성자 관점
- 변경 사항을 체계적으로 정리
- 리뷰어에게 명확한 정보 전달
- 리뷰 시간 단축

### 리뷰어 관점
- PR의 목적과 범위를 빠르게 파악
- 테스트 및 검증 방법 확인
- 효율적인 코드 리뷰

## 📁 파일 위치

PR 템플릿은 다음 위치에 생성합니다:

```
Team-B1ND/.github/
└── PULL_REQUEST_TEMPLATE.md

또는 각 프로젝트:
dodamdodam-web/.github/
└── PULL_REQUEST_TEMPLATE.md
```

## 📝 기본 템플릿

### 템플릿 코드

**파일명**: `PULL_REQUEST_TEMPLATE.md`

```markdown
## 📝 변경 내용

<!-- 이 PR에서 무엇을 변경했는지 간단히 요약해주세요 -->


## 🔗 관련 이슈

<!-- 관련된 이슈를 연결해주세요 -->
- Resolves #이슈번호
- See also #관련이슈번호


## 🧪 테스트 방법

<!-- 어떻게 테스트했는지 설명해주세요 -->
- [ ] 단위 테스트 추가/수정
- [ ] 통합 테스트 완료
- [ ] 수동 테스트 완료


## 📸 스크린샷 (UI 변경 시)

<!-- UI 변경이 있다면 Before/After 스크린샷을 첨부해주세요 -->

### Before
<!-- 변경 전 스크린샷 -->

### After
<!-- 변경 후 스크린샷 -->


## ✅ 체크리스트

- [ ] 코드가 프로젝트의 코딩 스타일을 따릅니다
- [ ] 자체 코드 리뷰를 완료했습니다
- [ ] 변경 사항에 대한 테스트를 추가했습니다
- [ ] 모든 테스트가 통과합니다
- [ ] 문서를 업데이트했습니다 (필요한 경우)
- [ ] Breaking Changes가 없습니다


## 💬 기타 사항

<!-- 리뷰어가 특별히 주의해서 봐야 할 부분이나 추가 설명 -->
```

## 📋 상세 템플릿 (선택사항)

더 자세한 정보가 필요한 프로젝트용:

```markdown
## 📝 변경 내용

### 요약
<!-- 한 문장으로 요약 -->


### 상세 설명
<!-- 무엇을 왜 변경했는지 자세히 -->


### 변경 파일 요약
<!-- 주요 변경 파일 및 내용 -->
- `src/components/Login.tsx`: 로그인 폼 UI 개선
- `src/api/auth.ts`: OAuth 로그인 API 추가
- `src/types/auth.ts`: 인증 타입 정의 추가


## 🔗 관련 이슈

- Resolves #123
- Related to #456


## 📊 변경 타입

<!-- 해당하는 항목에 체크 -->
- [ ] 새로운 기능 (feat)
- [ ] 버그 수정 (fix)
- [ ] UI/UX 변경 (design)
- [ ] 리팩토링 (refactor)
- [ ] 테스트 추가 (test)
- [ ] 문서 수정 (docs)
- [ ] 기타 (chore)


## 🧪 테스트 방법

### 테스트 환경
<!-- 어떤 환경에서 테스트했는지 -->
- OS:
- 브라우저/디바이스:
- 버전:

### 테스트 시나리오
<!-- 어떻게 테스트했는지 단계별로 -->
1.
2.
3.

### 테스트 결과
- [ ] 단위 테스트: ✅ 통과
- [ ] 통합 테스트: ✅ 통과
- [ ] E2E 테스트: ✅ 통과
- [ ] 수동 테스트: ✅ 통과


## 📸 스크린샷 / 화면 녹화

### Before
<!-- 변경 전 -->

### After
<!-- 변경 후 -->


## 🔍 리뷰 포인트

<!-- 리뷰어가 특별히 집중해서 봐야 할 부분 -->
-


## ⚠️ Breaking Changes

<!-- Breaking Changes가 있다면 자세히 설명 -->
- [ ] Breaking Changes 없음
- [ ] Breaking Changes 있음 (아래 설명)


## 📚 참고 자료

<!-- 참고한 문서, 링크, 디자인 시안 등 -->
-


## ✅ 체크리스트

### 코드 품질
- [ ] 코딩 컨벤션을 준수했습니다
- [ ] 자체 코드 리뷰를 완료했습니다
- [ ] 불필요한 주석을 제거했습니다
- [ ] 콘솔 로그를 제거했습니다

### 테스트
- [ ] 새로운 테스트를 추가했습니다
- [ ] 기존 테스트가 모두 통과합니다
- [ ] 엣지 케이스를 고려했습니다

### 문서
- [ ] README를 업데이트했습니다 (필요시)
- [ ] API 문서를 업데이트했습니다 (필요시)
- [ ] CHANGELOG를 업데이트했습니다 (필요시)

### 빌드 & 배포
- [ ] 빌드가 성공적으로 완료됩니다
- [ ] Lint 검사를 통과했습니다
- [ ] 번들 사이즈 영향을 확인했습니다


## 💬 추가 설명

<!-- 리뷰어에게 전달할 추가 정보 -->
```

## 🎨 플랫폼별 커스터마이징

### Web 프로젝트 추가 항목

```markdown
## 🌐 브라우저 호환성

<!-- 테스트한 브라우저 -->
- [ ] Chrome
- [ ] Safari
- [ ] Firefox
- [ ] Edge

## 📦 번들 사이즈

<!-- 번들 사이즈 변화 -->
Before: XXX KB
After: XXX KB
Diff: +/- XXX KB
```

### Mobile (Android/iOS) 추가 항목

```markdown
## 📱 테스트 디바이스

<!-- 테스트한 디바이스 및 OS 버전 -->
- [ ] Galaxy S24 (Android 14)
- [ ] Galaxy S22 (Android 13)
- [ ] iPhone 15 Pro (iOS 17)
- [ ] iPhone 13 (iOS 16)

## 🔋 성능 영향

<!-- 배터리, 메모리, CPU 사용량 영향 -->
- 배터리: 영향 없음 / 증가 / 감소
- 메모리: XX MB → XX MB
- 앱 크기: XX MB → XX MB
```

### Server 추가 항목

```markdown
## 🗄️ 데이터베이스 마이그레이션

<!-- DB 스키마 변경이 있는 경우 -->
- [ ] 마이그레이션 스크립트 작성
- [ ] Rollback 계획 수립
- [ ] 테스트 환경 검증 완료

## 🔌 API 변경사항

<!-- API 변경이 있는 경우 -->
### 새로운 엔드포인트
- `POST /api/v1/nightstudy`: 심야자습 신청

### 변경된 엔드포인트
- `GET /api/v1/meal`: response 형식 변경

### 삭제된 엔드포인트
- ~~`GET /api/v1/old-meal`~~

## ⚡ 성능 테스트

<!-- 성능 관련 변경 시 -->
- API 응답 시간: XX ms → XX ms
- DB 쿼리 최적화: Yes/No
- 캐싱 적용: Yes/No
```

## 📝 작성 예시

### 기본 예시

```markdown
## 📝 변경 내용

심야자습 신청 시 날짜 검증 로직을 추가했습니다.
과거 날짜 선택을 방지하고, 신청 가능한 기간을 제한합니다.

## 🔗 관련 이슈

- Resolves #234
- Related to #235 (심야자습 신청 개선)

## 🧪 테스트 방법

- [x] 단위 테스트 추가 (`validateNightStudyDate.test.ts`)
- [x] 통합 테스트 완료
- [x] 수동 테스트: 과거 날짜, 미래 날짜, 경계값 테스트

**테스트 시나리오:**
1. 심야자습 신청 화면 진입
2. 어제 날짜 선택 시도 → 에러 메시지 표시 확인
3. 30일 후 날짜 선택 시도 → 에러 메시지 표시 확인
4. 유효한 날짜 선택 → 정상 신청 완료

## 📸 스크린샷

### Before
과거 날짜 선택 가능했음

### After
![날짜 검증](./screenshot.png)
과거 날짜 선택 시 에러 메시지 표시

## ✅ 체크리스트

- [x] 코드가 프로젝트의 코딩 스타일을 따릅니다
- [x] 자체 코드 리뷰를 완료했습니다
- [x] 변경 사항에 대한 테스트를 추가했습니다
- [x] 모든 테스트가 통과합니다
- [x] 문서를 업데이트했습니다
- [x] Breaking Changes가 없습니다

## 💬 기타 사항

`minDate`, `maxDate` 상수는 `constants/date.ts`에서 관리하고 있습니다.
향후 날짜 제한 정책이 바뀌면 해당 파일만 수정하면 됩니다.
```

### UI/UX 변경 예시

```markdown
## 📝 변경 내용

DDS(Dodam Design System) 버튼 컴포넌트를 적용하여
로그인 화면의 일관성을 개선했습니다.

## 🔗 관련 이슈

- Resolves #567
- Related to #500 (DDS 전체 적용 프로젝트)

## 🧪 테스트 방법

- [x] 반응형 레이아웃 테스트
- [x] 다크모드 테스트
- [x] 접근성 테스트 (키보드 네비게이션)

## 📸 스크린샷

### Before
![이전 디자인](./before.png)

### After
![새 디자인](./after.png)

**주요 변경점:**
- 버튼 스타일을 DDS 기준에 맞춤
- 버튼 크기 및 간격 조정
- Hover/Active 상태 개선

## ✅ 체크리스트

- [x] 코딩 컨벤션 준수
- [x] 자체 리뷰 완료
- [x] DDS 가이드 준수
- [x] 다크모드 확인
- [x] 접근성 확인
- [x] 모든 브라우저 테스트

## 💬 기타 사항

이번 PR은 로그인 화면만 적용했습니다.
다른 화면들도 순차적으로 DDS 적용 예정입니다. (#500)
```

## 🚀 템플릿 적용 방법

### 1. 조직 레벨 템플릿 (권장)

```bash
# Team-B1ND/.github 저장소에 추가
cd .github

# 파일 생성
cat > PULL_REQUEST_TEMPLATE.md << 'EOF'
## 📝 변경 내용
...
EOF

# 커밋 및 푸시
git add PULL_REQUEST_TEMPLATE.md
git commit -m "feat: PR 템플릿 추가"
git push origin main
```

### 2. 프로젝트별 템플릿

```bash
# 각 프로젝트에 개별 적용
cd dodamdodam-web
mkdir -p .github
cat > .github/PULL_REQUEST_TEMPLATE.md << 'EOF'
...
EOF
```

### 3. 여러 템플릿 제공 (고급)

```bash
# .github/PULL_REQUEST_TEMPLATE/ 폴더 생성
mkdir -p .github/PULL_REQUEST_TEMPLATE

# 여러 템플릿 작성
.github/PULL_REQUEST_TEMPLATE/
├── basic.md          # 기본 템플릿
├── feature.md        # 기능 개발용
├── bugfix.md         # 버그 수정용
└── hotfix.md         # 핫픽스용
```

**사용 방법:**
PR 생성 시 URL에 템플릿 지정
```
?template=feature.md
```

## 🔧 GitHub Actions 통합

### PR 자동 검증

```yaml
# .github/workflows/pr-check.yml
name: PR Check
on:
  pull_request:
    types: [opened, edited]

jobs:
  check-pr:
    runs-on: ubuntu-latest
    steps:
      - name: Check PR title format
        uses: amannn/action-semantic-pull-request@v5
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          types: |
            feat
            fix
            design
            refactor
            test
            docs
            chore

      - name: Check linked issue
        run: |
          if ! grep -q "Resolves #" "$GITHUB_EVENT_PATH"; then
            echo "::error::PR must link to an issue"
            exit 1
          fi
```

### PR 자동 라벨링

```yaml
# .github/workflows/pr-labeler.yml
name: PR Labeler
on:
  pull_request:
    types: [opened, edited]

jobs:
  label:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/labeler@v4
        with:
          repo-token: ${{ secrets.GITHUB_TOKEN }}
```

## 📏 PR 작성 가이드라인

### DO ✅

1. **명확한 제목 작성**
   ```
   feat: 심야자습 날짜 검증 로직 추가
   fix: 급식 정보 로딩 오류 수정
   ```

2. **관련 이슈 연결**
   ```markdown
   - Resolves #123
   - See also #456
   ```

3. **충분한 설명 제공**
   - 무엇을 변경했는지
   - 왜 변경했는지
   - 어떻게 테스트했는지

4. **스크린샷 첨부** (UI 변경 시)
   - Before/After 비교
   - 주요 변경점 캡처

5. **체크리스트 완료**
   - 모든 항목 확인 후 체크

### DON'T ❌

1. **애매한 제목**
   ```
   ❌ Update code
   ❌ Fix bug
   ❌ WIP
   ```

2. **설명 없는 PR**
   ```markdown
   ❌ ## 변경 내용

   (비어있음)
   ```

3. **너무 큰 PR**
   - 500줄 이상의 변경은 분리 고려
   - 여러 기능을 한 PR에 포함 금지

4. **테스트 없는 PR**
   - 중요 로직 변경 시 테스트 필수

5. **미완성 PR**
   - Draft PR 기능 활용
   - 완료 후 리뷰 요청

## 💡 실무 팁

### 1. Draft PR 활용

```bash
# Draft PR 생성 (GitHub CLI)
gh pr create --draft --title "feat: 심야자습 기능 개발 중" --body "작업 진행 중입니다"

# Ready for review로 변경
gh pr ready
```

### 2. PR 템플릿 자동 채우기

```bash
# Git alias 설정
git config --global alias.pr-template '!cat .github/PULL_REQUEST_TEMPLATE.md'

# 사용
git pr-template
```

### 3. 코멘트 작성 가이드

**리뷰어:**
```markdown
<!-- 질문 -->
**Q:** 이 함수가 null을 반환하는 경우가 있나요?

<!-- 제안 -->
**💡 Suggestion:** Optional chaining 사용을 고려해보세요

<!-- 필수 변경 -->
**⚠️ Must Fix:** 이 부분은 보안 이슈가 있습니다

<!-- 칭찬 -->
**👍 Nice:** 깔끔한 리팩토링입니다!
```

### 4. 대규모 PR 관리

```markdown
## 📋 변경 내용

### Phase 1 (이번 PR)
- [x] 기본 UI 구현
- [x] API 연동

### Phase 2 (다음 PR)
- [ ] 에러 핸들링
- [ ] 최적화

이 PR은 전체 작업의 Phase 1에 해당합니다.
자세한 계획은 #123 이슈를 참고해주세요.
```

## 🤔 FAQ

### Q1. 템플릿을 꼭 다 채워야 하나요?
**A**: 해당 사항이 없는 섹션은 생략 가능합니다.

### Q2. PR 제목 형식은?
**A**: 커밋 컨벤션과 동일하게 `타입: 제목` 형식 사용

### Q3. 여러 이슈를 한 PR에서 해결하면?
**A**: 가능하면 분리하되, 불가피하면 모든 이슈 연결
```markdown
- Resolves #123, #124, #125
```

### Q4. Breaking Change는 어떻게 표시?
**A**: PR 제목에 `!` 추가 및 본문에 상세 설명
```
feat!: 인증 API v2로 변경

BREAKING CHANGE:
기존 /api/v1/auth는 더 이상 사용할 수 없습니다.
```

### Q5. WIP PR은 어떻게 만드나요?
**A**: Draft PR 기능 사용 또는 제목에 `[WIP]` prefix

---

**다음 단계**: [머지 규칙 보기](./05-merge-rules.md)
