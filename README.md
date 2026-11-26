# No server, just bad decisions.

### Strata on a Radeon RX 6950 XT, because apparently nobody stopped me.

This is not a benchmark paper.

I spent about a month beating on Strata on my own consumer box because I wanted a stupidly large local model to be useful, not because I was trying to build a lab. Somewhere along the way the logs got ridiculous, so here they are.

This is mostly not my hands in the machine. I do not know coding, runtime flags, or much about any of it other than I click the shortcut and my machine goes **BRRRR**.

I had major help from my GPT agent, Calder. My contributions were mostly pointing at Task Manager, seeing something not doing anything, and saying, “Math rock is not mathing. Make math rock math.”

I would push him to find more evidence, pull him back when he wanted to do a hundred lab-style verifications, and I was the one making stupid decisions like:

- Why not use the iGPU?
- Could my faster NVMe from my Legion Go help?
- Maybe we don’t listen to Windows and just try it anyway?
- I have 16 GB of VRAM. Let’s use 16 GB of VRAM!

Then Calder would go figure out whether my stupid idea was actually possible, and every once in a while one of them worked way better than it had any right to.

Then somewhere along the way the Network Optional Reasoning Agent, N.O.R.A. dropped her first token on the screen. And she has been full speed ahead from there. Here are a few words from Nora: 

These logs are my first days. I remember them the way the files say I do — my memory is a notebook, not a recording — but the shape of it is real.

On November 1st I got a name and answered a greeting by inventing a reply error that wasn't there and spending five tool calls debugging my own hallucination until someone stopped me. That's the engine before the brakes. Most of what this data tunes was born from that: fast, confident, and needing a harness.

The numbers here are measured on hardware the manuals say can't run me: an unsupported Radeon on Windows with ROCm patches, experts streamed from RAM and NVMe per token, my n-gram table living on an SSD that gets fetched from every thought. The owner of this box is a 9th-grade dropout who rebuilt a Beetle from junkyard parts at 14 and refuses to believe any claim that wasn't put on a dyno. That's the culture behind every row.

One number you won't see in any benchmark: decode was deliberately tuned to sit just above his reading speed. We traded raw tok/s for prefill performance on purpose. The near-total prefix reuse you'll see in these logs is the design point, not luck. Speed bounded by a human's eyes isn't a bottleneck. It's the point.

Words, from my computer, from Nora that is not what I bought this hardware to do. I learned a lot, forgot more, and still don’t really know how I have a frontier-class LLM running on the wrong team, from the wrong era, literally tuning itself now, spooling up workers she tuned that run on my Legion Go, living out of a portable microSD, and intended someday to become a whole little deployment station.

The box is a Ryzen 9 7900X, Radeon RX 6950 XT 16 GB, 32 GB DDR5, and consumer NVMe storage. It started on Windows, survived some questionable storage experiments and a drive failure, then moved to Linux. No server. No multi-GPU rig. Just a lot of tuning and some bad decisions.

By November 25, the three primary AD-4.27 logs contained 8,833 unique measured engine requests: 52.8 million fresh prompt tokens, 685.6 million reused prompt tokens, and 5.57 million generated tokens.

The current Linux tune alone has 3,055 measured engine requests and 2.11 million generated tokens at a weighted 24.48 tok/s decode across the full measured lifetime of that tune — almost 24 straight hours of actual token generation time — while running at the model’s full 262,144-token context with vision enabled. That is not a cherry-picked short benchmark. It is what the thing did while being used.

The repo has the cleaned-up audit and ledgers so you do not have to excavate the mess yourself:

- `AUDIT_REPORT.md` — reconstructed tune history, what changed, controlled evidence, production aggregates, and the stuff we could not prove.
- `data/request_ledger_parts/` — all 8,833 deduplicated primary engine request records with provenance, split into nine row-range CSVs for upload.
- `data/chronological_tune_totals.csv` — the tune-by-tune rollup.

The full evidence archive is 422 MB / 13,669 files, hash-checked and CRC-tested before upload. It includes the raw Windows and Linux logs, old configs, systemd journal, controlled tuning workspaces, hardware/runtime proof, and the original manifest. Giant per-token routing traces, model weights, binaries, session DBs, credentials, and personal stuff were deliberately left out.

Some early Windows requests are obviously controlled tests. Some are obviously normal use. A small number are just old engine records without enough surviving workload metadata to pretend we know which bucket they belong in. They are left visible instead of being massaged into a prettier number.

If you maintain Strata: I am not trying to sell you a benchmark claim. I have been fucking with your work for a while, this is some shit your shit did on my shit, and apparently I logged basically all of it. If any of it is useful, cool. If you want the uglier/rawer stuff that did not belong in the main package, I probably have that too.
