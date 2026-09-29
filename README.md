<h2 align="center">Hi there 👋</h2>
<p align="center">
  <b>Systems developer with an EE background, learning by building — from embedded hardware to real-time data pipelines and GPU computation.</b>
</p>
<p align="center">
  <a href="./README.ko.md"><img src="https://img.shields.io/badge/Language-한국어-blue.svg"></a>
</p>

---

### 🧭 About Me
- 🎓 **B.S. in Electrical Engineering** (Micro/Nano Systems), Virginia Tech
- 🔬 **Research interest**: Currently exploring how multiple resource-constrained embedded devices can share data and computation over unreliable networks
- 🎯 Focus: **Embedded systems · Real-time data pipelines · Sensor fusion · High-performance computing**
- 🛰️ Long-term goal: small-unit networked systems for **Command & Control (C2)** and battle management
- 🔧 Hands-on hardware builder — circuit & power design, CAD-designed 3D-printed enclosures, PCB etching, 3D printer builds
- 🌐 Bilingual: Korean / English

---

### 🚀 Featured Projects

#### 🎯 IFCAS — Infantry Fire Control Assistance System `2026.06 ~ Present`
> Counter-drone fire-control assistance device integrating optics, ranging, inertial sensing, and actuation.
> **Status:** hardware complete · firmware & Jetson software in progress (LRF ingestion over UART done)

- **Dual-compute architecture**: STM32H523 (Cortex-M33, RTOS) ↔ Jetson Orin Nano over **CAN**
- **Sensor timing sync**: STM32 triggers the OV9281 global-shutter camera via GPIO to align frames with IMU / LRF samples
- **Custom power system**: 4S Li-ion with BMS & fuse → four isolated buck rails (12V ×2 / 5V / 3.3V)
- **EMI shielding** around buck converters and cooling fan to protect IMU / camera signals
- **Varifocal optics** (5–50mm) with potentiometer-based zoom position sensing
- **Safety-interlocked actuation**: single-lever solenoid trigger lock, gated by a lock-retraction confirmation switch
- *In development*: IMU (LSM6DS3) attitude estimation, drone detection on Jetson, and zoom-invariant target tracking with a Kalman filter in **angle space** fusing LRF range and camera bearing
- Mock-firearm test platform (HK416D EBB) for recoil simulation, with custom 3D-printed enclosures

<br>

#### ⚡ TEFFP Seeker — Target Exposure Factor Function Parameters Seeker `2025.07 ~ 2026.03`
> GPU-accelerated backtesting & parameter optimization engine for ATM-Eta strategies, built on **Triton** kernels.

- **One Triton lane per parameter set** — thousands of full-length, minute-level backtests run concurrently on a single GPU
- Achieves **~98.7% of theoretical memory bandwidth** on RTX 3080 Ti
- **Single-pass balance trend evaluation** — growth rate & volatility solved in closed form from running least-squares sums, keeping per-lane memory constant regardless of data length
- Resolved catastrophic cancellation via precision rounding and **float64 accumulation**; float64 mode matches the CPU reference simulator exactly
- **Population-based search**: central-difference numerical gradients + Adam-style updates + self-developed repopulation, with a max-drawdown filter
- **Exchange-faithful simulation**: tiered maintenance margin liquidation, isolated/cross margin accounting, tick/step precision rounding
- Exports optimized parameters directly as **ATM-Eta Trade Configurations**
- 🔗 [kimlvis31/TEFFPSeeker](https://github.com/kimlvis31/TEFFPSeeker)

<br>

#### 📈 ATM-Eta — Auto Trade Machine Eta `2024.09 ~ 2026.05`
> Solo-developed end-to-end platform for real-time time-series ingestion, analysis, backtesting, and live execution — **~73,000 lines.**

- **9-process architecture** with a custom IPC protocol (FAR/FARR) — GUI, ingestion, analysis, simulation, and execution never block each other
- **Unified market data pipeline**: 4 heterogeneous streams (kline / aggTrade / depth / metric) normalized into a 1m base with on-demand multi-timeframe aggregation
- **Two-layer gap detection** with explicit data provenance tagging, Binance Vision + REST backfill, and dummy-range recovery (refetch / LAN import)
- **Multi-node continuity**: during maintenance another machine on the LAN takes over collection, then databases are reconciled by range metadata to fill gaps
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
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![C](https://img.shields.io/badge/C-00599C?style=flat-square&logo=c&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=cplusplus&logoColor=white)

**Embedded & Hardware**  
![STM32](https://img.shields.io/badge/STM32-03234B?style=flat-square&logo=stmicroelectronics&logoColor=white)
![NVIDIA Jetson](https://img.shields.io/badge/Jetson-76B900?style=flat-square&logo=nvidia&logoColor=white)
![RTOS](https://img.shields.io/badge/RTOS-555555?style=flat-square)
![Fusion 360](https://img.shields.io/badge/Fusion_360-0696D7?style=flat-square&logo=autodesk&logoColor=white)
![LTspice](https://img.shields.io/badge/LTspice-555555?style=flat-square)

**Compute & Libraries**  
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![Triton](https://img.shields.io/badge/Triton-555555?style=flat-square)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white)
![Pyglet](https://img.shields.io/badge/Pyglet-555555?style=flat-square)

**Database**  
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![TimescaleDB](https://img.shields.io/badge/TimescaleDB-FDB515?style=flat-square&logo=timescale&logoColor=black)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)

**DevOps & OS**  
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=flat-square&logo=ubuntu&logoColor=white)

---

### 📜 Certifications & Languages
- 정보처리기사 (Engineer Information Processing) — Written exam passed, practical in progress
- 임베디드기사 (Engineer Embedded Systems) — Written exam passed, practical in progress
- English — OPIc AL, TOEIC 985
