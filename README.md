# AI HTML — 임원 보고용 1-pager 컬렉션

AI(Claude)에게 긴 글·블로그·연구 자료를 던지면, **임원 보고용 self-contained HTML 1-pager** 로 정리해 모아두는 저장소다. 모든 문서는 외부 CDN/이미지 없이 단일 HTML로 작성되어 있어 브라우저에서 바로 열거나 그대로 메일/PDF로 공유할 수 있다.

## 왜 이 형식인가

- **5분 안에 읽힌다** — 한 화면에 6 섹션, 핵심 수치는 KPI 칩으로 강조.
- **자료들이 비교 가능하다** — 모든 문서가 같은 카드형 레이아웃·색 팔레트·6 섹션 골격을 따른다.
- **어디서나 열린다** — 외부 의존이 없어 사내망·오프라인·이메일 첨부 어디서든 동작한다.
- **모바일에서도 읽힌다** — 폭 ≤820px 에서 카드가 1열로 재배치된다.
- **인쇄가 깔끔하다** — `@media print` 로 그림자·배경을 정리, 1~2장 분량으로 떨어진다.

## 현재 컬렉션

| 파일 | 주제 | 한 줄 요약 |
|---|---|---|
| [`index.html`](./index.html) | 엔터프라이즈 AI 에이전트 도입 | Anthropic "Building AI agents for the enterprise" 의 핵심 — 3 Pillars · 6개월 도입 프레임워크 · 리스크 |
| [`llm-wiki.html`](./llm-wiki.html) | LLM-wiki 개념 + 온톨로지 비교 | LLM-wiki = 에이전트가 자동 작성·유지하는 위키. 온톨로지의 *대체가 아닌 상보* |
| [`llm-wiki-strategy.html`](./llm-wiki-strategy.html) | 개인·팀·AI Co-Scientist 활용 전략 | "가설↔증거↔비판" 루프와 "ingest·query·lint" 가 구조적으로 동형 — 조건부 적용 가능 |
| [`llm-wiki-executive-brief.html`](./llm-wiki-executive-brief.html) | LLM-Wiki 임원 브리프 | LLM-Wiki는 RAG와 온톨로지 사이의 지식 축적 계층 |

## 공통 디자인 시스템

모든 문서는 동일한 토큰을 공유한다 (CSS 변수로 정의되어 있어 새 문서를 만들 때 그대로 복사하면 된다).

- **레이아웃**: 12-컬럼 카드 그리드 (`.col-12 / .col-8 / .col-6 / .col-4`), ≤820px 에서 1-컬럼.
- **컴포넌트**: `Hero` 카드(그라데이션) · `KPI 칩` · `콜아웃`(info / warn / ok / amber) · `배지`(High / Med / Low) · `체크리스트` · `비교 표`.
- **6 섹션 표준**:
  1. 한 줄 요약
  2. 왜 중요한가
  3. 시스템 구조
  4. 기대 효과
  5. 리스크와 대응
  6. 다음 액션

## 보는 방법

### 1) 브라우저로 직접 열기
```bash
# Linux
xdg-open index.html

# macOS
open index.html

# Windows (PowerShell)
start index.html
```
또는 주소창에 `file:///<절대경로>/index.html` 입력.

### 2) 간이 로컬 서버
```bash
cd ai_html
python3 -m http.server 8000
# → http://localhost:8000/
```

### 3) PDF 로 변환
브라우저로 연 뒤 **인쇄(Ctrl/Cmd+P) → "PDF로 저장"**. 인쇄용 CSS 가 적용되어 그림자·배경이 정리된 채 저장된다.

## 새 문서 만들기 (체크리스트)

기존 문서를 복제해 시작하는 것이 가장 빠르다.

- [ ] 기존 HTML 한 개를 새 파일명으로 복사 (CSS 토큰 재사용)
- [ ] 6 섹션 골격 유지 — 헤더 표기, 카드 클래스명, KPI 4개, 푸터 출처 표기
- [ ] 외부 리소스 0건 인지 DevTools Network 탭에서 확인
- [ ] ≤820px 에서 카드가 1열로 재배치되는지, KPI 가 2열로 떨어지는지 확인
- [ ] 인쇄 미리보기에서 1~2장 안에 떨어지는지 확인
- [ ] 인용 수치(통계·날짜)는 본문/푸터에 출처 표기 — 과장 금지

## 톤·표기 원칙

- **기술적으로 정확하되 경영진이 이해 가능한 수준**으로 — 약어는 처음 등장 시 풀어 쓴다.
- **과장 금지** — 외부 인용 수치는 출처와 함께 *인용임을 명시*.
- **회의론도 균형 있게 포함** — 도구·표준의 한계를 숨기지 않는다.
- **벽 같은 텍스트 지양** — 표·콜아웃·체크리스트로 분해.

## 디렉터리 구조

```
ai_html/
├── README.md                       ← 이 문서
├── index.html                      ← 엔터프라이즈 AI 에이전트
├── llm-wiki.html                   ← LLM-wiki 개념 + 온톨로지 비교
├── llm-wiki-strategy.html          ← LLM-wiki 활용 전략 + Co-Scientist 검토
└── llm-wiki-executive-brief.html   ← LLM-Wiki 임원 브리프 (RAG ↔ 온톨로지 사이 축적 계층)
```

## 만드는 방식

새 자료를 정리하고 싶을 때는 Claude(또는 동급 LLM)에게 **원문 링크/텍스트** 와 함께 다음만 던지면 된다:

> "아래 내용을 바탕으로 단일 HTML 문서를 만들어줘. 임원 보고용 1페이지, self-contained, 외부 CDN 금지, 카드형, 모바일 반응형. 섹션은 (1) 한 줄 요약 (2) 왜 중요한가 (3) 시스템 구조 (4) 기대 효과 (5) 리스크와 대응 (6) 다음 액션. 톤은 기술적으로 정확하되 과장 금지, 표와 콜아웃 적극 활용."

이 저장소의 기존 문서가 같은 프롬프트로 만들어진 산출물이다.
