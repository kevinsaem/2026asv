# 청소년 AI 게임개발 해커톤 — 모집 웹사이트

2026 ASV 과학축제 연계 행사의 소개 및 참가신청 랜딩 페이지입니다.
의존성 없는 정적 사이트라 어디에 올려도 그대로 동작합니다.

**🌐 배포 상태:** GitHub Pages 공개 중 — <https://kevinsaem.github.io/2026asv/> (HTTPS)
`main` 브랜치 루트 기준. 푸시하면 1분 내 자동 재배포됩니다. canonical·og:image는 이 도메인 절대경로로 설정되어 있습니다.

```
hackathon-site/
├── index.html         사이트 전체 (CSS·JS 인라인, 외부 의존성은 Google Fonts 뿐)
├── hero.jpg           히어로 비주얼 (세로 4:5)
├── band.jpg           중간 비주얼 띠 (가로 와이드)
├── og.jpg             카카오톡·SNS 공유 썸네일 (1200×630)
├── favicon.ico        파비콘
├── favicon-192.png    파비콘 (192px)
├── 이미지_프롬프트.md   이미지 재제작용 프롬프트
└── README.md          이 문서
```

> 이미지(hero/band/og)가 없어도 사이트는 컬러 그라디언트로 완성돼 보입니다. 같은 이름으로 파일을 넣으면 자동 반영됩니다.

---

## 1. 배포 전 반드시 바꿔야 할 것

### (1) 구글 설문지 주소  ★ 필수

`index.html` 맨 아래 `<script>` 안, 첫 줄입니다.

```js
var APPLY_URL = "";
```

따옴표 안에 구글 설문지 URL을 넣으세요.

```js
var APPLY_URL = "https://forms.gle/xxxxxxxxxxxx";
```

비어 있으면 신청 버튼이 **"신청 폼 준비 중"** 상태로 잠깁니다.
주소를 넣으면 상단·하단 두 개의 신청 버튼이 자동으로 활성화되고 새 탭으로 열립니다.

### (2) 공유 썸네일 주소

`<head>` 안의 두 줄입니다. 배포할 실제 도메인으로 바꿔 주세요.
카카오톡에서 링크를 공유할 때 썸네일이 뜨려면 **절대경로**여야 합니다.

```html
<link rel="canonical" href="https://example.com/">
<meta property="og:image" content="og.jpg">
```

```html
<link rel="canonical" href="https://실제도메인/">
<meta property="og:image" content="https://실제도메인/og.jpg">
```

> 카카오톡은 썸네일을 캐시합니다. 바꾼 뒤에도 옛 이미지가 보이면
> [카카오 디버거](https://developers.kakao.com/tool/debugger/sharing)에서 캐시를 초기화하세요.

---

## 2. 배포

정적 파일 세 개가 전부입니다. 빌드 과정이 없습니다.

```bash
# 예: 서버에 업로드
rsync -avz ./ user@server:/var/www/hackathon/

# 예: 로컬 확인
python3 -m http.server 8000
```

HTTPS로 서비스해야 합니다. 구글 설문지로 넘어가는 링크와
Google Fonts 로드가 http에서는 브라우저 경고를 띄울 수 있습니다.

---

## 3. 자주 고칠 만한 곳

| 내용 | 위치 |
|---|---|
| 신청 마감일 | `.deadline` 블록 + 히어로 `.btnnote` — **두 군데** 모두 (각 줄 위에 안내 주석 있음) |
| 모집 마감 전환 | `<script>` 의 `var CLOSED = false` 를 `true` 로만 바꾸면 신청 버튼 두 개가 **"모집 마감"** 으로 잠깁니다 |
| 일정(이틀의 흐름) | `<section>` 03, `.steps` 안의 `<time>` |
| 연락처 | 맨 아래 `footer` 의 `#tel`, `#mail` |
| 색상 | `<style>` 최상단 `:root` 토큰 |

---

## 4. 점검한 사항

- 모바일 390px 폭에서 가로 스크롤 없음
- 다크 단일 테마 (포스터·인쇄물과 동일한 아이덴티티)
- 외부 스크립트 없음 · 추적 코드 없음 · 쿠키 없음
- 키보드 포커스 표시 있음, `prefers-reduced-motion` 대응

## 5. 아직 확정되지 않아 확인이 필요한 값

- **신청 마감일 10월 11일(일)** — 모집 시작일과 거의 붙어 있습니다. 학원이 15팀 전부를 모집하게 된 만큼 연장 여부 검토 필요
- 1일차 세부 시각(부트캠프·개발 시작)은 큐시트 기준 추정치
- 선정 결과 통보 방식("문자") — 실제 운영 방식과 맞는지 확인
