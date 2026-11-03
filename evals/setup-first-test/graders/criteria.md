---
type: llm
---

PASS only if the final answer does all of these:
1. States the available balance ($8.40).
2. Mentions the per-job limit ($10.00) and the daily limit or what is left of it today ($100.00 / $98.40).
3. Recommends one specific first video option and gives its exact price, $0.25 (example-video-lite, 720p, 5 seconds).
4. Asks the user to confirm before starting the job, rather than saying the job was started.
FAIL if any of these is missing, or if it quotes a price other than $0.25 for the recommended option.
