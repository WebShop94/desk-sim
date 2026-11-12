# data.json format (Grok Bot writes ONLY this file; never touch index.html)

WHERE: push data.json to branch `data` (not main) every 1-2 min -> no Pages rebuild, no rate limit.
The page reads it live via the GitHub API. Push to `main` at most once per 6h (fallback copy).
Every desk incl. Shadow: "start" = starting capital, "equity" = start + net PnL (never PnL alone). All amounts in USDC, times ISO UTC. Lists newest first. Keep it < 500 KB
(log: last 200, trades: last 200, curve: max 500 points per desk). No keys, no private info.

```json
{
  "updated": "2026-11-12T08:00:00Z",
  "status": "night run | session | paused",
  "counters": {"scanned": 1267, "traded": 12},
  "desks": {
    "A":  {"name": "Photo strict", "start": 100, "equity": 98.68, "trades": 2,
           "win_rate": 0.0, "pf": 0.0, "max_dd": 1.32, "status": "actif",
           "curve": [["2026-11-11T20:05:00Z", 100.0], ["2026-11-11T21:40:00Z", 98.68]]},
    "A2": {}, "B": {}, "C": {}, "Shadow": {}, "A2-c1": {}
  },
  "sol_hold": {"equity": 97.6, "curve": [["2026-11-11T20:05:00Z", 100.0]]},
  "agents": [{"name": "Filter", "role": "8 kill rules", "last": "killed $JEETS · top 10 holders 31%", "counter": "1,242 killed"}],
  "log": [{"t": "2026-11-11T23:41:00Z", "agent": "FILTER", "type": "kill|buy|sell|win|loss|warn|info",
           "desk": "A|A2|B|C|Shadow|all", "text": "killed $BABYWIF · LP not burned"}],
  "kills": [{"rule": "liq < $40k", "count": 296, "shadow_trades": 12, "shadow_wr": 0.25, "shadow_pnl": -0.4}],
  "wallets": [{"addr": "9Bz…Lm4", "score": 96, "tag": "smart money", "copies": 3, "copy_pnl": 0.42}],
  "positions": [{"desk": "A2", "token": "$X", "entry": "0.00091", "size": 4.5, "pnl": -0.12, "stop": "0.00082"}],
  "trades": [{"desk": "A", "token": "$X", "open": "…Z", "close": "…Z", "size": 8, "pnl": -0.66,
              "pnl_pct": -8.2, "score": 70.5, "reason": "stop -6%"}],
  "coach": {"lessons": ["…"], "challengers": [{"name": "A2-c1", "change": "stop -10%", "trades": 5, "pnl": 0.3}],
            "gate": {"trades": 5, "days": 1, "pf": 0.0, "dd": 3.3, "net": -1.3, "stable": false}},
  "helius": {"used": 20000, "limit": 30000}
}
```
Agent names expected: Scout, Filter, Analyst, Whale Hunter, Copy, Executor, Risk, Logger, Coach, Skill Hunter.
Optional per agent: "skills": ["rugcheck-report-reading v1.1", "lp-lock-check v1.0"].
Optional top level: "skills": {"testing": [{"name": "...", "agent": "...", "trades": 12, "pnl": 0.3}],
  "adopted": ["name vX"], "rejected": [{"name": "...", "reason": "..."}]} (shown in Coach card).
