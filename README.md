# Embedded Systems Journey

Daily study log for an embedded + control track on STM32, building toward cars and drones.
One folder per day, each with its own README: topics covered, concept notes, diagrams, doubts asked, the bug of the day, and a short revision quiz.

**Author:** Enosh RD · 2026 E&I graduate, BITS Pilani Hyderabad

---

## Boards

| Board | Core | Used for |
|---|---|---|
| NUCLEO-F030R8 | Cortex-M0, 48 MHz, no FPU, no CAN | 11-hour STM32 course, P2 |
| NUCLEO-F446RE | Cortex-M4F, 180 MHz, FPU, 2× CAN | FastBit MCU1/MCU2, drone work |

Tools: STM32CubeIDE · ST-LINK · multimeter · 24 MHz logic analyzer

---

## Plan (fixed deadlines)

| Track | Scope | Done by |
|---|---|---|
| 11-hour STM32 course (F030R8) | Projects 4–18 | Sun 8 Nov |
| | Projects 19–31 (25–26 with MPU6050) | Sun 15 Nov |
| FastBit MCU1 (F446RE) | GPIO + interrupts → SPI → catch-up → I2C + USART | Sun 29 Nov |
| FastBit MCU2 (F446RE) | Clocks/PLL, timers, capture/compare, PWM → CAN loopback/silent | Sun 20 Dec |
| DSA in C | pointers/arrays/strings → linked lists → bits → stacks/queues/ring buffer → sort/search → trees | ongoing, 45 min/day |

## Projects

| # | Project | Window | Status |
|---|---|---|---|
| P1 | Debounced button interrupt toggles an LED, on my own GPIO driver | 2–8 Nov | In progress |
| P2 | UART + LCD console on the F030 | 9–15 Nov | Not started |
| P3 | MPU6050 over I2C, streamed over UART at a fixed rate | 23–29 Nov | Not started |
| P4 | Tilt angle with a complementary filter | 30 Nov–6 Dec | Not started |
| P5 | Self-levelling servo platform with PID | 14 Dec–3 Jan | Not started |
| P6 | Both boards talking over UART, I2C, SPI and CAN (MCP2515 on the F030) | 4–17 Jan | Not started |

Later: drone flight controller · P7 smart-vehicle CAN network · OBD logger · FreeRTOS · Rust

Every project ships with a 30-second demo video, one measured number (loop time, interrupt latency or RAM), and one bug with its fix.

---

## Daily logs

| Date | Focus | Log |
|---|---|---|

---

## Folder layout

```
days/
  YYYY-MM-DD/
    README.md     ← topics, notes, diagrams, doubts, bug of the day, quiz, handoff
projects/
  P1-.../         ← code + project README (added as projects start)
```
