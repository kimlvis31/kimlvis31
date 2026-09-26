<h2 align="center">Hi there 👋</h2>
<p align="center">
  <b>Electrical Engineer building systems end-to-end — from sensors and firmware to GPU kernels and data pipelines.</b>
</p>
<p align="center">
  <a href="./README.ko.md"><img src="https://img.shields.io/badge/Language-한국어-blue.svg"></a>
</p>
---

### 🧭 About Me
- 🎓 **B.S. in Electrical Engineering** (Micro/Nano Systems), Virginia Tech
- 🎯 Focus: **Embedded systems · Sensor fusion · Real-time control · High-performance computing**
- 🛰️ Interested in **Battle Management Systems (BMS)** and **Command & Control (C2)** systems
- 🔧 Hardware maker — PCB etching, robot arm assembly, 3D printer builds & tuning, CNC machining
- 🌐 Bilingual: Korean / English

---

### 🚀 Featured Projects

#### 🎯 IFCAS — Infantry Fire Control Assistance System `2026.05 ~ Present`
> Infantry-level fire-control assistance system integrating optics, ranging, inertial sensing, and actuation.

- **Dual-compute architecture**: STM32H523 (Cortex-M33 @250MHz) ↔ Jetson Orin Nano Super over **CAN**
- **Sensor fusion**: IMU (LSM6DS3) **EKF**, TF02-PRO laser rangefinder, OV9281 global-shutter camera
- **Zoom-invariant target tracking**: Kalman filter operating in **angle space** instead of pixel coordinates
- **Motorized varifocal optics** (5–50mm) with potentiometer-based zoom position feedback & calibration LUT
- **Safety-interlocked actuation**: solenoid release gated by a lock-retraction confirmation switch
- **Custom power system**: 4S Li-ion → star-point distribution → 12V / 5V / 3.3V rails, fused & monitored
- Mock-firearm test platform (HK416D EBB) for recoil simulation, with custom 3D-printed parts

<br>

#### ⚡ TEFFP Seeker — Target Exposure Factor Function Parameters Seeker `2025.07 ~ 2026.03`
> GPU-accelerated backtesting & parameter optimization engine for ATM-Eta strategies, built on **Triton** kernels.

- **One Triton lane per parameter set** — thousands of full-length, minute-level backtests run concurrently on a single GPU
- Achieves **~98.7% of theoretical memory bandwidth** on RTX 3080 Ti (**~73µs per parameter set**)
- **Single-pass balance trend evaluation** — growth rate & volatility solved in closed form from running least-squares sums, keeping per-lane memory constant regardless of data length
- Resolved catastrophic cancellation via precision rounding and **float64 accumulation**
- **Population-based search**: central-difference numerical gradients + Adam-style updates + self-developed repopulation, with a max-drawdown filter
- **Exchange-faithful simulation**: tiered maintenance margin liquidation, isolated/cross margin accounting, tick/step precision rounding
- Exports optimized parameters directly as **ATM-Eta Trade Configurations**
- 🔗 [kimlvis31/TEFFPSeeker](https://github.com/kimlvis31/TEFFPSeeker)

<br>
  
#### 📈 ATM-Eta — Auto Trade Machine Eta `2024.09 ~ 2026.05`
> Solo-developed end-to-end crypto trading platform unifying multi-timeframe analysis, backtesting, and live execution — **~73,000 lines.**

- **9-process architecture** with a custom IPC protocol (FAR/FARR) — GUI, ingestion, analysis, simulation, and execution never block each other
- **Unified market data pipeline**: 4 heterogeneous streams (kline / aggTrade / depth / metric) normalized into a 1m base with on-demand multi-timeframe aggregation
- **Two-layer gap detection** with explicit data provenance tagging, Binance Vision + REST backfill, and dummy-range recovery (refetch / LAN import)
- **TimescaleDB** storage with **~78% compression** (98GB → 21GB), transactional batch writes, and automatic index repair
- **Exchange state reconciliation**: ambiguous orders verified by `clientOrderId` instead of blind retries, early fills attributed to in-flight orders
- **Priority-based API rate-limit budgeting** and make-before-break WebSocket renewal
- **TEF strategy interface** decoupling analysis from execution — strategies portable to the GPU optimizer
- **scrypt + Fernet** encrypted credential files (AAF), custom **Pyglet** real-time chart GUI
- Validated by a **118-day live run** on Binance Futures with automatic recovery from disconnects, rate limits, and stream interruptions
- 🔗 [kimlvis31/AutoTradeMachine_Eta](https://github.com/kimlvis31/AutoTradeMachine_Eta)

<br>

#### 🧪 ATM Alpha ~ Zeta `2023.06 ~ 2024.09`
> Six iterative generations of the trading system that laid the groundwork for ATM-Eta.

---

### 🛠️ Tech Stack

**Languages**  
![C](https://img.shields.io/badge/C-00599C?style=flat-square&logo=c&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=cplusplus&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)

**Embedded & Hardware**  
![STM32](https://img.shields.io/badge/STM32-03234B?style=flat-square&logo=stmicroelectronics&logoColor=white)
![NVIDIA Jetson](https://img.shields.io/badge/Jetson-76B900?style=flat-square&logo=nvidia&logoColor=white)
![CAN](https://img.shields.io/badge/CAN_Bus-555555?style=flat-square)
![RTOS](https://img.shields.io/badge/RTOS-555555?style=flat-square)
![Fusion 360](https://img.shields.io/badge/Fusion_360-0696D7?style=flat-square&logo=autodesk&logoColor=white)

**Compute & Libraries**  
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![Triton](https://img.shields.io/badge/Triton-555555?style=flat-square)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white)
![Pyglet](https://img.shields.io/badge/Pyglet-555555?style=flat-square)

**Database**  
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![TimescaleDB](https://img.shields.io/badge/TimescaleDB-FDB515?style=flat-square&logo=timescale&logoColor=black)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)

**DevOps**  
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

---

### 📜 Certifications
- 정보처리기사 (Engineer Information Processing) — Written exam passed, practical in progress
- 임베디드기사 (Engineer Embedded Systems) — Written exam passed, practical in progress
- SQLD — In preparation
