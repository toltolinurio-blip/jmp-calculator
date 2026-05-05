# Architecture — Nexus Analyst v25.80 Titanium

단일 파일 (`nexus_analyst.html`, ~60 KB). 빌드 없음, 모듈 없음.

## HTML 구조

| Lines | Content |
|-------|---------|
| 1–93 | HTML shell, CDN tags, Tailwind config |
| 94–110 | `GROUPS` constant, `INITIAL_PROMPT`, `REBALANCE_PROMPT` |
| 112–247 | Helper functions, URL builders (TradingView/Yahoo/Naver), File System / IndexedDB |
| 249–271 | `Icon` SVG component |
| 274+ | React components: `PriceMeter`, card views, modals, `App` |

## 스택
- React 18.2.0 (CDN UMD) + Babel Standalone 7.23.5 (클라이언트 트랜스파일)
- Tailwind CSS (CDN) — `slate-850` 커스텀 컬러 포함
- File System Access API (OneDrive/Dropbox 자동저장, Chrome/Edge 전용)
- IndexedDB (파일 핸들 영속), localStorage (포트폴리오 데이터·설정)

## 데이터 모델

```js
const GROUPS = {
  buyStrong,   // 💎 Strong Buy
  buyAccum,    // 🌱 Accumulation Buy – Recommended
  buyAccum2,   // 🌿 Accumulation Buy – Waiting
  hold,        // ⏳ Hold/Monitor
  sellProfit,  // 💰 Take Profit
  sellStop,    // 🛡️ Stop Loss
  watchlist,   // 👀 Watchlist
}
```

종목 필드: `name`, `ticker`, `country` (KR/US), `currentPrice`, `entryPrice`, `targetPrice`, `stopLoss`, `strategy`, `action`, `probability`, `opm`, `roe3y`, `beta`, `yieldGap`, `brokerage`, `purchasePrice`, `quantity`, `bodyLocation`

`bodyLocation` 은유: sole → knee → waist → chest → shoulder → head / injured (밸류에이션 위치)

## AI 프롬프트
- `INITIAL_PROMPT` — 신규 종목 분석, JSON 스키마 응답 필수
- `REBALANCE_PROMPT` — Titanium Protocol v4.9, JSON 스키마 응답 필수
- **주의**: 두 프롬프트의 JSON 스키마 구조는 앱이 직접 파싱하므로 절대 변경 금지

## 멀티마켓
- 한국주식: 6자리 KRX 코드, KRW, 9개 증권사 (키움/토스/삼성/미래에셋/NH나무/한국투자/KB/신한/대신)
- 미국주식: 심볼 기반, USD
- 차트 링크: ticker → name 폴백 (TradingView/Yahoo/Naver)
