Analyze the stock in $ARGUMENTS using a lean 2-phase approach.

## Phase 1 — Fast Scan (항상 실행, Haiku)
2-3개 WebSearch 쿼리 실행:
- "[종목명] 실적 뉴스 2026"
- "[종목명] PER PBR ROE 밸류에이션"
- (섹터 민감 종목만) "[종목명] 매크로 리스크"

결과를 5-7 bullet 요약으로 출력:
- 현재 주가 / 최근 시황
- 최근 실적 핵심
- 재무 지표 스냅샷 (PER, PBR, ROE)
- Perfect Storm 관련 리스크 (해당 시)

출력 후 반드시 질문: **"심층 분석을 진행할까요? Vault 저장 포함, Sonnet 사용 (~4,000 토큰 추가) [y/n]"**

## Phase 2 — Deep Report (사용자가 "y" 응답 시)
stock-analyst 서브에이전트를 호출해 전체 Nexus Analyst v3.0 리포트 실행:
- Obsidian Vault 기존 노트 참조
- Perfect Storm 4대 리스크 교차 검토
- Base / Bull / Bear 시나리오 서술 (수치 목표 없이)
- Vault 자동 저장 및 백링크 추가

## 항상 적용
- 절대 금지: 확률 수치, 가격 목표치, 감정적 언어, 결론 선행 분석
- Phase 1만 실행 시 Vault 저장 없음
