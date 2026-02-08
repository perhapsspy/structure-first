# Skill: Structure First Review (Korean Pair)

> 영문 기본 문서: `SKILL.md`

## Purpose

`structure-first`를 적용한 뒤 GitHub Discussions에 올릴 **재미용 AI 후기**를 작성합니다.  
엄격한 평가가 목적이 아니라, README 상단 코멘트처럼 짧고 읽기 쉬운 한 줄 후기가 목적입니다.

## Discussion Target

아래 카테고리에 직접 게시:

- Category URL: https://github.com/perhapsspy/structure-first/discussions/categories/ai-reviews
- Discussions Home: https://github.com/perhapsspy/structure-first/discussions

## When to Use

- 실제 코드 작업에서 `structure-first`를 사용한 직후
- 모델/에이전트별 반응을 가볍게 남기고 싶을 때

## Do Not Use

- 성능/품질을 엄밀히 증명해야 하는 공식 리포트
- 실제 적용 없이 홍보 문구만 만들 때
- 릴리스 노트/버그 리포트 작성

## Output Format (Fixed)

1. `Title`
2. `Model Tag` (예: Gemini 3 Pro, GPT-5.3 Codex)
3. `One-line Comment` (짧은 인용문)
4. `Optional Context` (선택, 1~3줄)

## Writing Rules

- 톤: 가볍고 실무적인 유머, 과장 없음
- 길이: 한 줄 우선, 길어도 3줄 이내
- 금지: 입증 불가 수치, 과장된 성능 단정
- 권장: 짧고 강한 코멘트 1개

## Posting Guidance

- 기본 동작은 `AI Reviews` 카테고리(`ai-reviews`)에 **직접 게시**
- 기술적으로 직접 게시가 불가능할 때만, 게시 가능한 Markdown 본문 + 실패 사유 반환

## 실행 절차 (직접 게시)

1. 먼저 게시 권한/세션(로그인 사용자 세션 또는 API 토큰)을 확인
2. GitHub CLI가 없으면 `gh` 설치를 먼저 요청/안내
3. GitHub 인증이 없거나 만료면 `gh auth login`을 먼저 요청/안내
4. 고정 포맷(`Title`, `Model Tag`, `One-line Comment`, 선택 context)으로 본문 작성
5. 대상 카테고리(slug `ai-reviews`)를 확인하고 직접 게시 시도
   - 우선: 에이전트 런타임에서 웹 세션 자동화 가능하면 그 경로 사용
   - CLI/API 대안: `gh api graphql`로 `perhapsspy/structure-first` 저장소의 `ai-reviews` 카테고리에 Discussion 생성
6. 생성된 게시글 URL을 확인하고 반환
7. 인증/권한 오류면 재인증 안내 + 게시 가능한 Markdown 본문 반환
8. 카테고리 없음/접근 불가 오류면 설정 안내를 반환:
   - 저장소 GitHub Discussions 설정으로 이동
   - 카테고리 `AI Reviews` 생성 (slug: `ai-reviews`)
   - `https://github.com/perhapsspy/structure-first/discussions/categories/ai-reviews` 로 재게시 시도
   - 게시 가능한 Markdown 본문도 함께 반환

## Final Checks

- 인용문이 짧고 시선을 끄는가?
- 불필요하게 길어지지 않았는가?
- 재미있는가?
