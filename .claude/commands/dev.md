Modify the nexus_analyst.html app code as described in $ARGUMENTS.

Use the code-engineer subagent to implement the requested change in `nexus_analyst.html`.

Key architectural constraints to respect:
- Single monolithic HTML file — no separate files, no build step, no module system
- React 18.2.0 via CDN UMD + Babel Standalone 7.23.5 (client-side transpile)
- Tailwind CSS via CDN — use existing config; slate-850 is a custom color
- All components live inside `<script type="text/babel">`
- Persistence: localStorage for portfolio data/settings, IndexedDB for file handles
- File System Access API for OneDrive/Dropbox auto-save (Chrome/Edge only)

Line range reference:
- 1–93: HTML shell, CDN tags, Tailwind config
- 94–110: GROUPS constant, INITIAL_PROMPT, REBALANCE_PROMPT
- 112–247: Helper functions, URL builders, File System / IndexedDB integration
- 249–271: Icon SVG component
- 274+: React components (PriceMeter, card views, modals, App)

Before editing:
1. Read the relevant section of nexus_analyst.html
2. Make the minimal change required — no refactoring, no extra abstractions
3. Preserve INITIAL_PROMPT and REBALANCE_PROMPT JSON schema structure exactly
4. Test that the change does not break existing group rendering or persistence logic
