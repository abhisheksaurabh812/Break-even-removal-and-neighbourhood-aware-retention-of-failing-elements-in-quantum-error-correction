# Round 16 — final archive (13 Nov 2026)

**Three parts, each under 25 MB.** `round16_part1_of_3_main.zip` (everything except round 15's runs),
`round16_part2_of_3_round15_runs_d9.zip` and `round16_part3_of_3_round15_runs_d7.zip` (round 15's 70 main runs, read
only by `analyse16_I10.py` and `gen_cfg16M.py`). Extract all three into the same folder: they fill one `round16/`
folder. Part 1 alone checks and re-runs everything else.

**Confidential.** Unpublished results behind the Indian provisional application of 8 November 2026 and its cognate.
Share only under confidentiality until the material is filed or published.

**Status.** Complete: 327 jobs in parts A–H, J, K and M, 62 CPU-hours on two cores, all finished (one erasure job
re-run from scratch after the 2-hour limit on background commands; the last three BP-OSD levels finished point by
point after a container restart; see *Record*). The rules of every simulation part (A–H, J, K, M) were written and
hashed before its first run; part I's items follow the design (1–9), rules hashed before computing (3b, 10, 11),
or were computed after the tests without a bar (12, 13).
**34 of 36 pre-registered checks passed**; E1 (couplers) failed with both decoders. Verification by separately written
scripts: 313 thresholds in 122 files recomputed without mismatch; part M recomputed with round 15's own statistics
functions without mismatch; frozen files unchanged (227 of 227 in round 16's lists, part M's 178 among them; 89 of 89
of round 15's). Write-up: `qec2/dev16/RESULTS_round16.md` (corrected and extended on 13 November; its last section
says what changed). Design: `qec2/dev16/ROUND16_DESIGN.md`. Working notes: `qec2/dev16/NOTES16.md`.

**This archive was checked from a fresh copy** (13 Nov 2026; `tools/check_round16.sh`, `tools/spotcheck16.py`):
unpacked into an empty folder, `tools/check_round16.sh` passed every check: the manifest; all nine hash lists;
`verify16.py` and `verify16_M.py`, whose output was identical to the stored output; and every part-I and part-M
analysis, whose output files were identical apart from item 9's milliseconds per decision period. `tools/spotcheck16.py`
then re-ran one job of each of parts H, C, G, F and M from the fresh copy (`H_d7_edge-data-x_plain_L8`,
`C_d7_xbias10_zanc_plain_L1`, `G_bb_unchanged_L1`, `F_targeted_m100` and `M_pairs_s18401`, the last rebuilding part
M's model caches from scratch): every count and every stored array was identical to the original run's.

## Parts

| Part | Question | Code (in `qec2/dev16/`) | Rules | Jobs | Results (`out16/`) |
|---|---|---|---|---|---|
| A | Ways of keeping a failing qubit (true rate, tracked, unchanged or no weights) | `ideal16.py`, `deform16.py` | `PREREG_16T.md` | `jobs16T.txt` | `A/` |
| B | Break-even tables at distances 5, 11 and 13 | `ideal16.py` | `PREREG_16B.md` | `jobs16B.txt` | `B/` |
| C | SI1000 and X-biased noise | `ideal16.py` | `PREREG_16T.md` | `jobs16T.txt` | `C/` |
| D | X-type measure qubits (X basis) | `ideal16.py` | `PREREG_16T.md` | `jobs16T.txt` | `D/` |
| E | Failing couplers | `ideal16.py` | `PREREG_16T.md` | `jobs16T.txt` | `E/` |
| F | Layout chosen at calibration time (40 random and 40 targeted maps, d = 9) | `f16.py` | `PREREG_16F.md` | `jobs16F.txt` | `F/` |
| G | qLDPC [[72,12,6]]: keeping versus erasing, BP-OSD | `bb16.py`, `bposd16.py` | `PREREG_16GJ.md` | `jobs16GJ.txt` | `G/` |
| H | Boundary and corner qubits | `ideal16.py`, `hdist16.py` | `PREREG_16H.md` | `jobs16H.txt` | `H/` |
| I | Analyses of the stored tables and runs (items 1–11; 12–13 computed afterwards, no bar) | `analyse16_I*.py` | `ROUND16_DESIGN.md`, `PREREG_16I3b.md`, `PREREG_16I11.md` | none | `I/` |
| J | BP-OSD on the surface code, d = 5 | `j16.py`, `j16pt.py`, `j16drive.py` | `PREREG_16GJ.md` | `jobs16GJ.txt` | `J/` |
| K | Decoder-only erasure | `ideal16.py` | `PREREG_16T.md` | `jobs16T.txt` | `K/` |
| M | Online, only the switch-out decision changed (30 runs) | `run16m.py` → `../dev15/m15/run15.py`; `gen_cfg16M.py` | `PREREG_16M.md` | `jobs16_M.txt` | `M/` |

Seeds (fixed in the rules): Stim seeds from 1600001 (B), 1610001 (A), 1620001 (C), 1630001 (D), 1640001 (E),
1650001 (H), 1660001 (K), 1670001 (J); numpy seeds from 1680001 (G); maps 1690001 + m and Stim 1691000 + 10 m + chunk
(F); part M seeds 18001–18010 (realistic), 18401–18410 (neighbouring failures), 18701–18710 (hardware-like). Spent
on development: part M seed 18999; part F dev maps 7000000 + m; the decoder checks listed in `PREREG_16GJ.md`.

## Contents

The folders mirror the workspace the runs used, so every relative path in the code works unchanged.

- `qec2/dev16/` — round 16: the code above; `check16.py` (circuit checks of `deform16.py`), `queue16.py` (job queue),
  `verify16.py` and `verify16_M.py` (verification, written separately from the run scripts); the rules, design,
  notes and write-up; job lists (`jobs16*.txt`; `jobs16_all.txt` to `jobs16_all5.txt` are the combined queue as it
  grew, the last with part M first, as run); `cfgM/` (part M configurations); `out16/` with every result,
  `done/` (seconds per job), `logs/` (each job's output), `queue.log`, the hash lists (`*hashes_at_start*.txt`,
  each with its time of recording), `verify16.txt` and `M/verify16_M.txt`; development checks in `repro/`, `probe/`,
  `dev_j/` and `out16/M/dev_repro*`, `out16/M/devM*`. Left out: part M's model caches (`cacheM/`, 977 MB, rebuilt on
  first use), byte-code, and three scratch folders left by interrupted `ideal16.py` jobs.
- `qec2/` — the shared code as frozen (every file named in a hash list) and the other top-level scripts; the CUSUM
  kernel (`kernel.c`, `libkernel.so`); round 15's configurations (`cfg14/`, `cfg15/`); the crossover tables read by
  parts F and I (`out9/`, `out10/`, `dev15/m15/tables/`); round 15's runner and helpers (`dev15/m15/`, code only);
  round 15's 70 main runs (`out15/`, read by `analyse16_I10.py` and `gen_cfg16M.py`) with its hash list and summaries.
- `bin/stim` — the Stim command-line tool of the earlier rounds (unchanged; in round 15's hash list).
- `tools/PyMatching/src/pymatching/` — PyMatching 2.4.0 built from source; parts A–K (`--pymatching` in the jobs).
- `pylib/pymatching/` — PyMatching 2.4.0, the build used by round 15; part M and `analyse16_I11.py`.
- `tools/stimpy/stim/` — Stim 1.15.0 Python module built from source; `check16.py` and `hdist16.py` only.
- `tools/PyMatching/LICENSE`, `tools/Stim/LICENSE` — both Apache 2.0.
- `ENVIRONMENT.txt` — machine, versions and checksums of the compiled files. `MANIFEST.sha256` — every file.
- `tools/check_round16.sh`, `tools/spotcheck16.py`, `tools/localise_jobs.py` — added for this archive.

## Requirements

Linux x86-64 and Python 3.13 with numpy and scipy (versions in `ENVIRONMENT.txt`). The compiled modules are for CPython 3.13
on x86-64 Linux. Elsewhere, install `stim==1.15.0` and `pymatching==2.4.0` and pass their paths (the pip `stim`
package also provides the `stim` command). Rebuild the kernel off Linux x86-64 with
`gcc -O2 -shared -fPIC -o libkernel.so kernel.c` in `qec2/`.

**Exact counts.** Stim's seeded sampling is the same only with the same Stim version and the same machine type: its
own help says results "will not" match across versions and "may not" across machines with different SIMD widths.
With the bundled `bin/stim` on x86-64 the stored counts are reproduced exactly (see the check above); elsewhere expect
statistically equivalent counts, not identical ones.

## Checking the archive (a few minutes; nothing in the archive is changed)

    tools/check_round16.sh

It checks `MANIFEST.sha256`; every hash list of rounds 15 and 16; re-runs `verify16.py` and `verify16_M.py` in a
temporary copy and compares their output with the stored output; and re-runs every part-I and part-M analysis there
and compares each output file with the stored one (only item 9's milliseconds per decision period may differ).
With part 1 alone it skips what needs round 15's runs and says so.

## Re-running jobs

Single jobs, into a temporary folder, compared with the stored counts (timing fields ignored):

    python3 tools/spotcheck16.py --list
    python3 tools/spotcheck16.py H_d7_edge-data-x_plain_L8 C_d7_xbias10_zanc_plain_L1 G_bb_unchanged_L1

Whole parts: job lines are `name est_seconds requires command`, run from `qec2/dev16/` by `queue16.py`. The commands
carry the original workspace path (`/tmp/claude-0/-home-claude/3dcb49be-a1d8-5021-976d-e9463a8ac650/scratchpad`);
`tools/localise_jobs.py` writes copies with this archive's path (the hashed originals stay as they are). The queue
skips a job marked in `out16/done/`, and the run scripts resume from their output files (a level, map or run already
stored is skipped), so work in a copy of the archive and delete there the results to be regenerated, keeping the
`hashes_at_start.txt` files. For part B, for example:

    cp -a round16 /scratch/r16 && cd /scratch/r16/qec2/dev16
    rm out16/B/d*.json out16/done/B_*
    python3 ../../tools/localise_jobs.py jobs16_all5.txt        # -> jobs16_all5_local.txt
    python3 queue16.py jobs16_all5_local.txt 95 2                # minutes per batch, jobs at a time; repeat until done

Then the analyses and the verification, from `qec2/dev16/`:

    python3 analyse16_I.py > out16/I/I_results.txt
    python3 analyse16_I3b.py; python3 analyse16_I10.py; python3 analyse16_I12_13.py; python3 analyse16_M.py
    PYTHONPATH=../../pylib python3 analyse16_I11.py
    python3 verify16.py > out16/verify16.txt; python3 verify16_M.py > out16/M/verify16_M.txt

Part M can also be regenerated from round 15's stored configurations with `python3 gen_cfg16M.py` (writes `cfgM/` and
`jobs16_M.txt`). A part-M run takes 10–50 minutes plus the model caches on first use; a full re-run takes about
62 CPU-hours.

## Record

- Part M was added on 9 November after an outside review, with its own rules and hashes, and moved ahead of the
  remaining parts before any part-M run (`jobs16_all5.txt`; noted in `out16/M/hashes_at_start.txt`). Before its first
  run a stored round-15 run was reproduced through `run16m.py` with every array identical (`out16/M/dev_repro*`).
- Part F's bar was changed from the approved design before any part-F simulation (stated in `PREREG_16F.md`).
- One erasure job hit the 2-hour limit on background commands and was re-run from scratch; batches then used a
  95-minute start window (`queue.log`).
- A container restart on 10 November stopped one BP-OSD job. The three remaining levels were run point by point with
  `j16pt.py` (checked first to reproduce two counts of `j16.py` exactly, 271 and 438) driven by `j16drive.py`; points
  already printed by the interrupted run were taken from its log (`out16/J/pts/`, `out16/J/pointwise_hashes.txt`).
- Items 12 and 13 of part I were computed on 13 November, after the pre-registered tests, from stored counts only
  (`analyse16_I12_13.py`). `out16/I/I12_bposd_with_matching_thresholds.json` is item 12 computed inline on 10 November
  while drafting; it is identical to the scripted `I12_results.json`. `out16/I/I_results_before_full_B.json` is part I
  run before every part-B table had finished (superseded by `I_results.json`).
- `RESULTS_round16.md` was corrected on 13 November: two online comparisons stated as differences now carry their
  intervals, which include zero; the BP-OSD ratios are stated exactly; the role-check line gives the 33.6× case with
  200 blocks separately (83–86% caught, the rest undecided); items 12 and 13 were added. No result changed.
