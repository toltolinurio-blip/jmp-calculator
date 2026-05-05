Run a portfolio rebalancing simulation using the Titanium Protocol v4.9.

Use the rebalancer subagent to:
1. Read current portfolio data from nexus_analyst.html (GROUPS constant: buyStrong, buyAccum, buyAccum2, hold, sellProfit, sellStop, watchlist)
2. Fetch latest prices and macro context via web search
3. Apply the REBALANCE_PROMPT schema embedded in the app
4. Simulate weight adjustments based on:
   - Current bodyLocation of each position (sole→knee→waist→chest→shoulder→head/injured)
   - Perfect Storm macro framework risk scores
   - Group-level allocation targets

Output:
- 현재 포트폴리오 스냅샷 (Current snapshot by group)
- 리밸런싱 제안 (Suggested moves: buy more / trim / exit / watch)
- 매크로 리스크 맵 (Macro risk exposure per position)
- 실행 우선순위 (Execution priority order)

Do NOT output probability numbers or price targets. Follow Nexus Analyst v3.0 절대 금지 rules.
