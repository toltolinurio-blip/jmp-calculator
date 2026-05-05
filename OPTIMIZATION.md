# OPTIMIZATION.md — 토큰 절약 원칙

## 핵심 원칙 5가지

### 1. 모델 계층화
- **Haiku** (기본): 웹서치, 요약, 매크로 간단 조회
- **Sonnet** (에이전트 자동): 심층 분석, 코딩 수정, 리밸런싱
- 세션 기본값을 Haiku로 설정 → 분석 에이전트가 Sonnet으로 자동 업그레이드

### 2. 지연 실행 (Lazy Execution)
- `/analyze`: 웹서치 먼저 → 심층 분석은 `y/n` 확인 후 실행
- `/dev`: 수정 범위 먼저 파악 → 필요 섹션만 Read (전체 60KB 파일 지양)
- 불필요한 Vault 탐색 금지 — Phase 2 심층 분석 시에만 실행

### 3. 컨텍스트 최소화
- CLAUDE.md: 핵심 규칙만 유지 (123줄 → 27줄, 78% 감소)
- 상세 문서 분리: `docs/ARCHITECTURE.md`, `docs/OBSIDIAN_TAGS.md`
- 에이전트별 전용 지시 → 중복 컨텍스트 제거

### 4. 캐시 활용
- 여러 종목 분석 시 동일 세션에서 연속 실행 (5분 내 캐시 유효)
- 반복 패턴 작업은 한 번에 배치 처리

### 5. Vault 저장 조건화
- Phase 2 심층 분석 완료 시에만 저장
- Phase 1 (웹서치 요약)은 저장하지 않음 → 불필요한 Write 토큰 절약

## 금지 패턴
| 패턴 | 이유 | 대안 |
|------|------|------|
| `nexus_analyst.html` 전체 Read | 60KB 소비 | 필요 섹션만 Read (line range 지정) |
| 모든 /analyze에서 Vault 탐색 | Glob + Read 오버헤드 | Phase 2 확인 후만 탐색 |
| 동일 종목 재검색 | 중복 토큰 낭비 | 컨텍스트 내 기존 데이터 활용 |
| Sonnet으로 단순 요약 | 비용 대비 과잉 | Haiku로 충분 |

## 작업별 권장 흐름
```
/analyze → Phase 1 (Haiku 웹서치) → 필요시 y → Phase 2 (Sonnet 심층)
/rebalance → Sonnet 직접 (복잡도 높음, 절충 불가)
/macro → Haiku 웹서치 + 요약 (충분)
/dev → Sonnet (필요 섹션만 Read 후 수정)
```
