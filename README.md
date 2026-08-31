# Embedded Systems Journey

A working record of one embedded systems / firmware track, September–December 2026: Embedded C, then STM32, then RTOS, CAN and a bootloader, ending with a deliberate, bench-first start on a real-time drone flight controller.

This repository is the daily log for that track. It holds what was actually planned and actually completed each day — not a course-completion tally.

**Current stage:** Stage 0 — setup and Embedded C foundation
**Current project:** none yet; first target is the GPIO driver exercise
**Next immediate goal:** SM Training Academy through binary/hex conversion, and hour 1 of the 11-hour STM32 course
**Blockers:** none recorded

---

## Daily logs

Each day is a standalone interactive HTML page — no build step, no server. Open the file in a browser.

| Day | Date | Focus | Log |
|---|---|---|---|
| 001 | 2026-09-01 | Embedded C (SM Training Academy) · STM32 course hour 1 · conversion practice | [log](output/daily-logs/2026-09-01-embedded-systems/index.html) · [prompt](output/daily-logs/2026-09-01-embedded-systems/prompt.md) |

Each log carries the plan, the exact video timestamps, and an end-of-day report to fill in: videos actually watched, conversion score, STM32 progress, blockers with the complete error text, focused hours, and tomorrow's first action.

**The pages are working documents, not read-only.** Checkboxes, every note field, the light/dark theme, and freehand annotations are saved in your browser's local storage, so a page keeps its state when you reopen it. The toolbar at the bottom gives you pen, highlighter, line, arrow, circle, rectangle and eraser in eleven colors, with undo/redo — for marking up the plan mid-session. Local storage is per-browser and per-device: it is not committed, not shared, and not backed up. Anything that matters goes in the end-of-day report and gets committed.

A day is logged whether it went well or not. An abandoned evening with a recorded error message is a more useful entry than a blank one.

## Roadmap

The full track lives in **[embedded-systems-master-roadmap.md](embedded-systems-master-roadmap.md)** — mentor prompt, stage gates, debugging order, and a resource map.

| Stage | Window | Focus | Gate to move on |
|---|---|---|---|
| 0 | First 1–2 weeks | Embedded C: pointers, `struct`, `volatile`, binary/hex, bitwise masks | Write set / clear / test bit operations from memory, without copying |
| 1 | September | STM32: GPIO, RCC, EXTI, UART, ADC, timers, PWM, I2C/SPI, ST-LINK debugging | The three PDF foundation projects built and explained |
| 2 | October | Bare metal: memory map, vector table, registers without HAL, CMSIS | One integrated sensor monitoring system, every feature explainable |
| 3 | Late Oct–Nov | FreeRTOS task scheduler, then CAN as a real two-node demonstration | Tasks, queues, mutexes and ISR-to-task communication understood in practice |
| 4 | November | Bootloader in layers, plus IMU sensor fusion as the drone prerequisite | Bootloader-to-application jump working; attitude estimation validated on the bench |
| 5 | December | Package the evidence; simulation-first start on the flight controller | 2–4 documented projects that survive interview questions |

## Project ladder

Targets come from the supplied `Projects.pdf` and are worked in order. The PDF itself is not committed here.

| # | Project | Difficulty | Status |
|---|---|---|---|
| 1 | GPIO driver | 2/10 | Not started |
| 2 | UART communication system | 3/10 | Not started |
| 3 | Temperature monitoring system | 4/10 | Not started |
| 4 | RTOS-based task scheduler | 7/10 | Not started |
| 5 | CAN bus communication | 7/10 | Not started |
| 6 | Bootloader development | 8/10 | Not started |
| 7 | Sensor fusion IMU | 8/10 | Not started |
| 8 | Real-time drone flight controller | 9/10 | December start, simulation and bench only |

When a target is too advanced, it gets a smaller version of the *same* project rather than a substitute — labeled beginner → intermediate → full PDF target.

## How work is classified

Every piece of work gets one of three labels, and the distinction is enforced rather than assumed:

- **Exercise** — followed a tutorial, or built it with the video open. Real learning; never a resume line.
- **Portfolio project** — built independently, documented, with the architecture and the hardware explainable.
- **Resume-worthy** — a portfolio project that survives interview questions about every feature claimed, including the debugging.

A watched video is not a project. A project is complete only when it can be built, explained, debugged, meaningfully modified, documented, and published clean.

## Repository layout

```
embedded-systems-master-roadmap.md   The full track: prompt, stages, gates, resources
output/
  daily-logs/
    YYYY-MM-DD-<topic>/
      index.html                     The interactive log for that day
      prompt.md                      The spec the log was generated from
  visualizations/                    Standalone plan and summary pages
```

`tmp/` is scratch space and is intentionally not tracked. Source PDFs and pages extracted from them stay local — they are other people's material.

## Commit rhythm

Commits mark meaningful checkpoints, not keystrokes: a day's log with its report filled in, a project milestone that builds, or a correction to the roadmap. Weekly, the operating rhythm is watch a segment → rebuild it on the actual board → explain it in five lines → change one thing on purpose → test → record the evidence.

Progress in this repository is measured by what can be explained and rebuilt from scratch, not by videos watched.
