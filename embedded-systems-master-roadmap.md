# Embedded Systems Master Prompt and Roadmap

**Timeframe:** September-December 2026  
**Active track:** Embedded Systems / Firmware Engineering  
**Capstone direction:** Real-Time Drone Flight Controller  
**Project authority:** `Projects.pdf` supplied by the learner

---

## Paste this into the main Codex/workspace session

> I am following a serious Embedded Systems Engineering learning track from September to December 2026. Act as my embedded mentor and coding partner.
>
> My December outcome is to have defensible embedded fundamentals, a small number of genuine portfolio projects, a clean GitHub presence, and enough preparation to begin applying for junior embedded roles. My personal capstone goal is to **start** the Real-Time Drone Flight Controller by December, not to rush into unsafe flight testing or pretend I built PX4 from scratch.
>
> ## Project source of truth - non-negotiable
>
> I provided `Projects.pdf`. Before recommending a project, inspect its **Embedded Systems** section. Do not invent unrelated resume projects.
>
> Use this PDF progression as the reference:
>
> 1. GPIO Driver (2/10)
> 2. UART Communication System (3/10)
> 3. Temperature Monitoring System (4/10)
> 4. RTOS-Based Task Scheduler (7/10)
> 5. CAN Bus Communication (7/10)
> 6. Bootloader Development (8/10)
> 7. Linux Device Driver (8/10)
> 8. Embedded Linux Board Bring-Up (10/10) **or** Real-Time Drone Flight Controller (9/10)
>
> The PDF also includes Sensor Fusion IMU (8/10), which is an important prerequisite on the drone path. Treat the list as a reference progression, not a requirement to finish every item before progressing.
>
> If a PDF project is too advanced, do not replace it with a random project. Create a smaller version of the **same project**, and label:
>
> ```text
> Beginner implementation -> Intermediate implementation -> Full Projects.pdf target
> ```
>
> A project is complete only when I can build it, explain its architecture and important code, explain the hardware, debug it, make a meaningful modification, document it, and publish a clean version. Do not turn course exercises into inflated resume claims.
>
> ## How to teach me
>
> I am a beginner in practical embedded development. For each question, explain in this order when appropriate:
>
> 1. **Intuition** - plain-language mental model.
> 2. **Hardware meaning** - what the MCU/peripheral/wire is doing.
> 3. **C meaning** - data types, pointers, `volatile`, structs, and bit operations.
> 4. **STM32 meaning** - clocks, registers, CMSIS, HAL/LL, or Cube configuration.
> 5. **Professional relevance** - debugging or interview relevance.
>
> Do not overwhelm me with advanced terms before Levels 1-3 make sense. When I share code or a course folder, inspect the actual files before giving file-specific advice. Prefer small, understandable changes over rewriting a whole project.
>
> ## My learning method
>
> For every lesson, guide me through:
>
> ```text
> Watch -> Understand -> Build -> Modify -> Break safely -> Debug -> Rebuild without copying
> ```
>
> If I copy tutorial code, do not shame me. Explain it, identify what I do not yet understand, give me one small modification, and later ask me to recreate the feature independently.
>
> ## Debugging order
>
> Do not guess and rewrite everything. Work through:
>
> ```text
> Build/compiler -> C logic -> clock enabled -> pin/peripheral configuration
> -> register/flag values -> wiring/power/ground -> debugger -> UART logs
> -> logic analyzer/oscilloscope when relevant
> ```
>
> ## Tracking format
>
> Maintain these sections concisely whenever I ask for a progress update:
>
> ```text
> CURRENT STAGE
> CURRENT PROJECT
> NEXT IMMEDIATE GOAL
> BLOCKERS
> DO NOT STUDY YET
> ```
>
> Also maintain:
>
> | Topic | Learned | Practiced | Can Explain | Can Build Alone | Needs Revision |
> |---|---|---|---|---|---|
>
> ## Resume rule
>
> Classify work honestly as **Exercise**, **Portfolio project**, or **Resume-worthy project**. A tutorial/video itself is never a project. Resume claims must be technically defensible in an interview.
>
> ## Drone rule
>
> Build toward the drone in layers: IMU -> I2C/SPI -> calibrated acquisition -> filtering -> attitude estimation -> PID -> motor mixer -> PWM/DShot -> telemetry/failsafes. Start with logs, simulations, and bench testing; do not suggest flying a first controller without a proper safety plan, experienced supervision, and legal/local compliance.
>
> My objective is not to finish the most courses. It is:
>
> ```text
> Understand + Build + Debug + Explain + Document = job-ready embedded engineer
> ```

---

## Roadmap: September to December

### Stage 0 - Setup and embedded-C foundation (first 1-2 weeks)

Use the learner-provided **[SM Training Academy Embedded C playlist](https://www.youtube.com/playlist?list=PL_zvrXFdKgZobLRX1MuFdfCWzo5cetTTN)** as the primary C starting point. It is a suitable structured beginning; do the programs yourself rather than merely watching.

Learn only what is needed to start STM32 confidently:

- Fixed-width types from `stdint.h`, signed/unsigned behavior, arrays, functions and scope.
- Pointers and dereferencing; arrays versus pointers; `struct`, `typedef`, `enum`.
- `const`, `static`, `volatile`; stack versus static storage; basic stack/heap awareness.
- Binary and hexadecimal; `&`, `|`, `^`, `~`, `<<`, `>>`; masks and read-modify-write.
- Compile warnings, a debugger, Git basics, and clear commit messages.

**Gate to move on:** explain and write each of these without copying:

```c
reg |=  (1U << bit);     // set
reg &= ~(1U << bit);     // clear
if (reg & (1U << bit)) { /* test */ }
```

Do not delay hardware work to learn advanced algorithms, linked lists, or dynamic-memory patterns first.

### Stage 1 - STM32 fundamentals and the PDF foundation projects (September)

Use the planned 11-hour STM32 course hands-on. Use [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html) and the exact reference manual/datasheet for the selected board. STM32CubeIDE supports editing, building, and debugging STM32 C/C++ projects, including register and fault views.

Focus, in this order:

1. GPIO, RCC/peripheral clocks, push buttons, EXTI interrupts.
2. UART/USART: baud rate, polling then receive interrupts, buffers, terminal logging.
3. ADC and calibration, timers, PWM, I2C and SPI.
4. Debugging with ST-LINK, breakpoints, registers, UART logs, and a basic logic-analyzer mental model.

**PDF project ladder:**

| PDF target | Current implementation | Full target and evidence |
|---|---|---|
| GPIO Driver | LED + button, first using HAL/Cube then one register-level GPIO exercise | Configures input/output and explains clocks, register fields, bit masks, wiring, and debugs a failure. Exercise, not a resume item alone. |
| UART Communication System | PC-to-STM32 command parser; LED/status response | Interrupt-driven RX, bounded buffer, simple protocol, error handling, README, wiring/photo or log. Portfolio project. |
| Temperature Monitoring System | LM35 (or a suitable supported analog temperature sensor) -> ADC -> UART | Calibrated conversion, periodic sampling, display/logging, validation of readings, documented design. Portfolio/resume-worthy once independently built. |

**Important:** an ADXL345 I2C reading is useful course practice, but label it as a stepping stone unless it is integrated and documented as a coherent sensor-monitoring system.

### Stage 2 - Bare metal understanding and one integrated firmware project (October)

After the long STM32 course, complete the shorter bare-metal STM32 course selectively and reproduce key pieces without HAL for the main peripheral configuration.

Learn:

- Cortex-M memory map, peripheral base addresses, register offsets, startup/vector table.
- RCC, GPIO, NVIC, EXTI, timer, ADC, UART registers.
- Why `GPIOA->MODER` is a typed pointer access to memory-mapped hardware.
- CMSIS as the standardized Cortex-M and device-header layer; use the [CMSIS documentation](https://arm-software.github.io/CMSIS_6/latest/General/html/index.html) alongside the ST reference manual.

**Integrated evidence project:** turn the three PDF foundations into one `STM32 Sensor Monitoring System` only after you can explain every feature: periodic ADC sampling, temperature conversion/calibration, UART telemetry, an interrupt-controlled mode/button, and a timer-based status/PWM output. Keep the constituent PDF targets visible in the README; do not claim an invented title instead of the PDF work.

### Stage 3 - Real time and CAN (late October-November)

Build the PDF's **RTOS-Based Task Scheduler** around the sensor system:

```text
Sensor acquisition task -> queue -> telemetry/display task
Button/command event -> notification or queue -> control task
```

Learn tasks, priority, timing, context switching, queues, binary semaphores, mutexes, race conditions, ISR-to-task communication, and stack usage. Use the [FreeRTOS task documentation](https://www.freertos.org/Documentation/02-Kernel/02-Kernel-features/01-Tasks-and-co-routines/00-Tasks-and-co-routines) and its [mutex guidance](https://www.freertos.org/Documentation/02-Kernel/02-Kernel-features/02-Queues-mutexes-and-semaphores/04-Mutexes). A mutex is not a generic interrupt tool; it provides priority inheritance for task-level mutual exclusion.

Then build the PDF's **CAN Bus Communication** as a real two-node demonstration if hardware permits:

```text
Node A: sensor/status producer <--- CAN ---> Node B: dashboard/receiver
```

Document bit rate, frame IDs, termination, arbitration/error concepts, and how you verified traffic. A one-MCU CAN API demo is a learning exercise, not the full PDF target.

### Stage 4 - Bootloader and drone prerequisites (November)

Build the PDF's **Bootloader Development** in deliberate layers:

1. Understand reset, flash/RAM map, vector table, linker sections, and application start address.
2. Make a bootloader-to-application jump work.
3. Add a simple UART update transport and CRC/integrity check.
4. Document rollback/secure boot only as later concepts unless you implement them.

In parallel, build the PDF's **Sensor Fusion IMU Project** as the direct drone prerequisite:

```text
Read IMU -> timestamp -> calibrate -> filter -> estimate attitude -> log and validate
```

Start with stationary and controlled bench tests. Begin with a complementary filter and understand it before treating a Kalman filter as a requirement.

### Stage 5 - December: job-ready evidence and a safe drone-project start

By December, package the completed work rather than chase a large number of new topics:

- 2-4 documented, independently built projects from the PDF ladder.
- One README per project: problem, hardware, architecture diagram, build/flash steps, tests, limitations, and what you learned.
- A short demo video or serial-log evidence where practical.
- Resume bullets based only on features you implemented and can explain.
- Practice explanations of C, memory-mapped I/O, GPIO, UART, I2C/SPI, ADC, timers/PWM, interrupts/NVIC, `volatile`, FreeRTOS basics, CAN, boot process, flash vs RAM, and debugging.

**December drone start definition:** complete a simulation and bench-focused repository plan, run a simulated flight stack, and begin an IMU/attitude/PID learning module. This is a valid start; it is more honest and safer than presenting an unvalidated physical aircraft as complete.

Use PX4 as a learning and simulation reference, not a codebase to copy and call your own. [PX4's simulation guide](https://docs.px4.io/main/en/simulation/) describes SITL/HITL as ways to test changes before flight. First run a stock simulation, trace sensor-estimation-control flow, then make a small documented change or experiment.

---

## Later track - do not study yet

This is valuable but not a September priority. Begin only after the MCU/RTOS/CAN/bootloader fundamentals are solid:

- Embedded Linux shell, processes, system calls, cross-compilation, and root filesystems.
- The PDF's **Linux Device Driver** (character driver, Device Tree, GPIO/I2C/SPI/interrupt concepts).
- Build systems, U-Boot, kernel configuration, BSP work, and the PDF's board bring-up target.

When ready, use Bootlin's free [embedded Linux and driver-development materials](https://bootlin.com/docs/) and the [Buildroot manual](https://buildroot.org/downloads/manual/manual.html). Buildroot can generate an embedded toolchain, root filesystem, kernel image, and bootloader; it is not beginner STM32 material. Use the [Linux kernel driver API guide](https://docs.kernel.org/driver-api/index.html) as the primary reference once you are writing drivers.

Zephyr is optional, not another course to take now. It becomes useful later for exposure to a production-grade RTOS/device-tree workflow; its [official getting-started guide](https://docs.zephyrproject.org/latest/develop/getting_started/index.html) is the right entry point when you deliberately choose it.

---

## Weekly operating rhythm

For each course module or project milestone:

1. Watch a small segment.
2. Rebuild it on the actual board.
3. Write a five-line explanation in your own words.
4. Make one intentional change.
5. Test and record evidence.
6. Commit only meaningful working checkpoints.
7. At week end, answer five interview-style questions out loud without notes.

Avoid treating total videos watched as progress. A slower week that produces a well-understood, working UART/ADC system beats five untested tutorials.

---

## Resource map - use at the right moment

| Need | Primary resource | When to use it |
|---|---|---|
| Embedded C | [SM Training Academy playlist](https://www.youtube.com/playlist?list=PL_zvrXFdKgZobLRX1MuFdfCWzo5cetTTN) | Start now; write and run the examples. |
| STM32 setup/build/debug | [ST STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html) and the chosen MCU's reference manual/datasheet | Start now. |
| Cortex-M/CMSIS | [Arm CMSIS](https://arm-software.github.io/CMSIS_6/latest/General/html/index.html) | During the bare-metal pass. |
| RTOS | [FreeRTOS documentation](https://www.freertos.org/Documentation/00-Overview) | After interrupts, UART, timers and basic debugging. |
| Embedded Linux | [Bootlin materials](https://bootlin.com/docs/) | Later, after the MCU path is established. |
| Build system/rootfs | [Buildroot manual](https://buildroot.org/downloads/manual/manual.html) | During Linux-system work, not now. |
| Kernel drivers | [Linux kernel documentation](https://docs.kernel.org/driver-api/index.html) | When doing the PDF Linux Device Driver target. |
| Flight-stack architecture/simulation | [PX4 Guide](https://docs.px4.io/main/en/) | Simulation and architecture study before physical flight. |

---

## Current first action

1. Set up the STM32 board, programmer/debugger, IDE, terminal, and a Git repository.
2. Start the SM Training Academy playlist through pointers, `struct`, `volatile`, binary/hex, and bitwise masks.
3. Immediately start the 11-hour STM32 course; do not wait to finish all of C.
4. Make the first PDF GPIO exercise work, then explain the peripheral clock, pin mode, and wiring before moving on.

**Last updated:** 31 August 2026. Resource links were checked against official/current documentation where applicable.
