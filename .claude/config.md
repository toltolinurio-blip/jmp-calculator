# Claude Code 모델 전략

## 기본 설정
- **기본 모델**: `claude-haiku-4-5-20251001` (settings.local.json에 설정)
- 빠른 조회, 웹서치 요약, 간단한 파일 작업에 사용

## 에이전트별 모델 자동 전환
| 에이전트 | 모델 | 이유 |
|---------|------|------|
| stock-analyst | Sonnet 4.6 | 심층 분석, 귀납적 추론 |
| rebalancer | Sonnet 4.6 | 복잡한 포트폴리오 계산 |
| code-engineer | Sonnet 4.6 | 코딩 정확도 |
| macro-updater | Haiku 4.5 | 웹서치 + 요약으로 충분 |

## 수동 모델 전환
- 세션 내 Sonnet 필요 시: `/model claude-sonnet-4-6`
- 세션 내 Haiku 복귀: `/model claude-haiku-4-5-20251001`

## 토큰 예산 기준
- 단순 질문/조회: Haiku (기본값 적용)
- /analyze Phase 1: Haiku (기본값)
- /analyze Phase 2 + 심층 분석: Sonnet (stock-analyst 에이전트 자동 적용)
- /rebalance, /dev: Sonnet (에이전트 자동 적용)
