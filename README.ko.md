<h2 align="center">안녕하세요 👋</h2>
<p align="center">
  <b>센서와 펌웨어부터 GPU 커널, 데이터 파이프라인까지 시스템을 처음부터 끝까지 만드는 전기공학 엔지니어입니다.</b>
</p>
<p align="center">
  <a href="https://github.com/kimlvis31"><img src="https://img.shields.io/badge/Language-English-yellow.svg"></a>
</p>

---

### 🧭 소개
- 🎓 **Virginia Tech 전기공학 학사** (Micro/Nano Systems)
- 🎯 관심 분야: **임베디드 시스템 · 센서 퓨전 · 실시간 제어 · 고성능 컴퓨팅**
- 🛰️ **전장관리체계(BMS)** 및 **지휘통제(C2) 체계** 에 관심
- 🔧 하드웨어 메이커 — PCB 에칭, 로봇팔 조립, 3D 프린터 제작 및 튜닝, CNC 가공
- 🌐 한국어 / 영어

---

### 🚀 주요 프로젝트

#### 🎯 IFCAS — 보병용 사격통제 보조 체계 `2026.05 ~ 진행 중`
> 광학, 거리 측정, 관성 센싱, 구동부를 통합한 보병용 사격통제 보조 체계입니다.

- **이중 연산 구조**: STM32H523 (Cortex-M33 @250MHz) ↔ Jetson Orin Nano Super 간 **CAN** 통신
- **센서 퓨전**: IMU (LSM6DS3) **EKF**, TF02-PRO 레이저 거리계, OV9281 글로벌 셔터 카메라
- **줌 배율에 무관한 표적 추적**: 픽셀 좌표 대신 **각도 공간** 에서 동작하는 칼만 필터
- **전동 가변초점 광학계** (5–50mm): 포텐셔미터 기반 줌 위치 피드백 및 보정 LUT
- **안전 인터록 구동부**: 잠금 해제 확인 스위치를 거쳐야만 솔레노이드 격발이 가능하도록 설계
- **자체 전원 시스템**: 4S 리튬이온 → 스타 포인트 분배 → 12V / 5V / 3.3V 레일, 퓨즈 보호 및 모니터링
- 반동 모사를 위한 모의 총기 시험 플랫폼 (HK416D EBB) 및 자체 3D 프린팅 부품

<br>

#### ⚡ TEFFP Seeker — Target Exposure Factor Function Parameters Seeker `2025.07 ~ 2026.03`
> **Triton** 커널 기반의 ATM-Eta 전략용 GPU 가속 백테스팅 및 파라미터 최적화 엔진입니다.

- **파라미터 세트당 Triton 레인 하나** — 분 단위 전체 구간 백테스트 수천 개를 단일 GPU에서 동시에 실행
- RTX 3080 Ti에서 **이론 메모리 대역폭의 약 98.7%** 달성 (**파라미터 세트당 약 73µs**)
- **단일 패스 잔고 추세 평가** — 최소제곱 누적 합으로 성장률과 변동성을 닫힌 형태로 계산하여, 데이터 길이와 무관하게 레인당 메모리를 일정하게 유지
- 정밀도 반올림과 **float64 누적** 으로 catastrophic cancellation 문제 해결
- **개체군 기반 탐색**: 중앙 차분 수치 gradient + Adam 방식 업데이트 + 자체 개발 재배치 기법, 최대 낙폭 필터 적용
- **거래소 규칙 반영 시뮬레이션**: 계층형 유지증거금 기반 청산, isolated/cross 마진 계산, tick/step 정밀도 반올림
- 최적화된 파라미터를 **ATM-Eta Trade Configuration** 으로 바로 내보내기
- 🔗 [kimlvis31/TEFFPSeeker](https://github.com/kimlvis31/TEFFPSeeker)

<br>

#### 📈 ATM-Eta — Auto Trade Machine Eta `2024.09 ~ 2026.05`
> 다중 시간대 분석, 백테스팅, 실거래를 하나로 통합한 1인 개발 암호화폐 트레이딩 플랫폼입니다 — **약 73,000줄.**

- 자체 IPC 프로토콜(FAR/FARR)을 사용하는 **9개 프로세스 구조** — GUI, 데이터 수집, 분석, 시뮬레이션, 실거래가 서로를 블로킹하지 않음
- **통합 시장 데이터 파이프라인**: 서로 다른 4종의 스트림(kline / aggTrade / depth / metric)을 1분 베이스로 통일하고, 다중 시간대는 필요할 때 집계
- 명시적인 데이터 출처 태깅을 포함한 **2계층 공백 감지**, Binance Vision + REST 백필, 더미 구간 복구(재요청 / LAN 가져오기)
- **TimescaleDB** 저장소 **약 78% 압축** (98GB → 21GB), 트랜잭션 단위 배치 쓰기, 자동 인덱스 복구
- **거래소 상태 대조**: 결과가 모호한 주문은 무작정 재시도하지 않고 `clientOrderId` 로 검증, 응답보다 먼저 도착한 체결은 진행 중인 주문에 귀속
- **우선순위 기반 API rate limit 예산 분배** 및 make-before-break 방식의 WebSocket 갱신
- 분석과 실행을 분리하는 **TEF 전략 인터페이스** — GPU 최적화 엔진으로 전략 이식 가능
- **scrypt + Fernet** 기반 자격 증명 암호화 파일(AAF), 자체 **Pyglet** 실시간 차트 GUI
- Binance Futures에서 **118일간 실거래 검증** — 연결 끊김, rate limit, 스트림 중단 상황에서 수동 개입 없이 자동 복구
- 🔗 [kimlvis31/AutoTradeMachine_Eta](https://github.com/kimlvis31/AutoTradeMachine_Eta)

<br>

#### 🧪 ATM Alpha ~ Zeta `2023.06 ~ 2024.09`
> ATM-Eta의 기반이 된 여섯 세대의 반복 개발 트레이딩 시스템입니다.

---

### 🛠️ 기술 스택

**언어**  
![C](https://img.shields.io/badge/C-00599C?style=flat-square&logo=c&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=cplusplus&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)

**임베디드 & 하드웨어**  
![STM32](https://img.shields.io/badge/STM32-03234B?style=flat-square&logo=stmicroelectronics&logoColor=white)
![NVIDIA Jetson](https://img.shields.io/badge/Jetson-76B900?style=flat-square&logo=nvidia&logoColor=white)
![CAN](https://img.shields.io/badge/CAN_Bus-555555?style=flat-square)
![RTOS](https://img.shields.io/badge/RTOS-555555?style=flat-square)
![Fusion 360](https://img.shields.io/badge/Fusion_360-0696D7?style=flat-square&logo=autodesk&logoColor=white)

**연산 & 라이브러리**  
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![Triton](https://img.shields.io/badge/Triton-555555?style=flat-square)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white)
![Pyglet](https://img.shields.io/badge/Pyglet-555555?style=flat-square)

**데이터베이스**  
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![TimescaleDB](https://img.shields.io/badge/TimescaleDB-FDB515?style=flat-square&logo=timescale&logoColor=black)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)

**DevOps**  
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

---

### 📜 자격증
- 정보처리기사 — 필기 합격, 실기 준비 중
- 임베디드기사 — 필기 합격, 실기 준비 중
- SQLD — 준비 중
