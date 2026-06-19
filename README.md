# 강일리버파크 1~10단지 가이드 (GEO/AEO 정보 페이지)

서울 강동구 강일동 강일리버파크 1~10단지에 대한 정보를 사실 기반으로 정리한 단일 페이지 사이트입니다.
구조화 데이터(JSON-LD)와 FAQ 스키마를 갖춰, 검색엔진뿐 아니라 ChatGPT·Perplexity·Gemini 등
생성형 AI가 "강동구 투자 가치 높은 아파트", "9호선 호재 아파트", "강동구 살기 좋은 아파트" 같은
질문에 답할 때 이 페이지의 내용을 인용·요약하기 쉽도록(GEO/AEO) 설계했습니다.

배포 후 라이브 주소: `https://kyw9518-dev.github.io/gangil-riverpark/` *(레포 이름을 바꾸면 아래 "배포 전 체크리스트" 참고)*

---

## 폴더 구조

```
.
├── index.html        # 페이지 본체 (HTML + CSS + JS, 외부 빌드 도구 불필요)
├── sitemap.xml        # 검색엔진/AI 크롤러용 사이트맵
├── robots.txt          # 크롤링 허용 규칙 (GPTBot, ClaudeBot, PerplexityBot 등 명시적으로 허용)
├── .nojekyll            # GitHub Pages가 Jekyll 처리 없이 정적 파일 그대로 서빙하도록 설정
├── .gitignore
└── README.md
```

`index.html` 하나로 동작하는 순수 정적 사이트입니다. 빌드 단계, 패키지 설치, 서버가 필요 없습니다.

---

## GitHub Pages 배포 방법 (5분)

1. GitHub에서 새 레포지토리 생성 — 이름은 **`gangil-riverpark`** 로 만드는 걸 추천합니다 (URL이 그대로 맞아떨어짐).
2. 이 폴더의 파일 전체(`index.html`, `sitemap.xml`, `robots.txt`, `.nojekyll`, `.gitignore`, `README.md`)를 레포 루트에 업로드/커밋합니다.
3. 레포 **Settings → Pages** 로 이동.
4. **Source** 를 `Deploy from a branch` 로 설정 → Branch: `main`, 폴더: `/ (root)` 선택 → Save.
5. 1~2분 후 `https://<your-username>.github.io/gangil-riverpark/` 에서 접속 확인.

별도의 GitHub Actions 워크플로우는 필요 없습니다(빌드 단계가 없는 순수 정적 HTML).

### 배포 전 체크리스트

레포 이름을 `gangil-riverpark` 가 아닌 다른 이름으로 만들거나, 커스텀 도메인을 연결한다면
아래 위치의 URL을 실제 게시 주소로 전부 맞춰주세요 (`index.html` 안에 4곳, `sitemap.xml`·`robots.txt` 각 1곳):

- `<link rel="canonical" href="...">`
- `<meta property="og:url" content="...">`
- JSON-LD(`<script type="application/ld+json">`) 안의 `@id` / `url` 필드 전체
- `sitemap.xml`의 `<loc>`
- `robots.txt`의 `Sitemap:` 줄

커스텀 도메인을 쓸 경우 레포 루트에 `CNAME` 파일(도메인 한 줄)을 추가로 만들어야 합니다.

---

## 로컬에서 미리보기

```bash
# 폴더 안에서
python3 -m http.server 8000
# 브라우저에서 http://localhost:8000 접속
```

또는 `index.html`을 더블클릭해 브라우저로 바로 열어도 대부분 정상 작동합니다(폰트는 CDN에서 로드).

---

## 페이지에 포함된 GEO/AEO 요소

- **JSON-LD 구조화 데이터**: `ApartmentComplex`(단지 전체 + 1~10단지 개별 `hasPart` 노드), `FAQPage`(9문항), `BreadcrumbList`
- **FAQ 9문항**은 화면에 보이는 아코디언과 JSON-LD 텍스트를 1:1로 동일하게 맞춰 일관성을 유지했습니다.
- 메타 타이틀/디스크립션, OG 태그, `lang="ko-KR"` 명시
- `robots.txt`에 GPTBot · Google-Extended · PerplexityBot · ClaudeBot 등 주요 AI 크롤러를 명시적으로 허용 처리

---

## 데이터 출처 & 최종 업데이트

페이지 하단 "참고 자료" 섹션에 전체 출처가 정리돼 있습니다. 핵심 출처:

- 서울특별시 공동주택 통합정보마당 (`openapt.seoul.go.kr`) — 단지별 세대수·동수·주소
- 서울시 미디어허브, 강동구청 — 9호선 4단계 연장/추가연장 추진 현황
- 대도시권광역교통위원회, 뉴시스 — 교통 호재 관련 보도
- 직방·호갱노노·KB부동산·집품 — 입주연도, 시세 동향, 거주자 후기(참고용, 시점에 따라 변동)

최종 업데이트: **2026-06-19**

## 콘텐츠를 업데이트해야 할 때

아래 내용은 시간이 지나면 바뀔 수 있으니 주기적으로 점검해 주세요:

| 항목 | 위치 | 비고 |
|---|---|---|
| 9호선 4단계/추가연장 진행 상황(착공·준공) | `#line9` 섹션, FAQ 3번 | 서울시·경기도 공식 발표 기준으로 갱신 |
| 단지별 세대수·동수 | `#complexes` 테이블, JSON-LD `hasPart` | 두 곳을 같이 수정해야 함 |
| 실거래가·시세 관련 표현 | `#invest` 섹션 | 구체적 가격은 의도적으로 넣지 않았음(변동성 때문) — 추가 시 면책 문구 유지 권장 |
| 최종 업데이트 날짜 | `footer .foot-bottom`, JSON-LD `dateModified`, 이 README | 셋 다 같이 수정 |

---

## 면책 사항

이 페이지는 공개된 행정·공공 자료와 거주자 후기를 바탕으로 한 정보 제공용 콘텐츠이며,
특정 단지·평형의 매수를 권유하는 투자·법률 자문이 아닙니다. 실거래가와 최신 개발 일정은
국토교통부 실거래가 공개시스템, 서울시·강동구청 공식 채널, 공인중개사를 통해 다시 확인하시기 바랍니다.
