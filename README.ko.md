<h2 align="center">안녕하세요 👋</h2>
<p align="center">
  <b>전기공학 배경의 시스템 개발자 — 임베디드 하드웨어부터 실시간 데이터 파이프라인, GPU 연산까지 직접 만들며 배우고 있습니다.</b>
</p>
<p align="center">
  <a href="./README.md"><img src="https://img.shields.io/badge/Language-English-blue.svg"></a>
</p>

---

### 🧭 소개
- 🎓 **Virginia Tech 전기공학 학사** (Micro/Nano Systems 트랙)
- 🔬 **연구 관심**: 제한된 연산 자원을 가진 여러 임베디드 장치가 불안정한 네트워크에서 데이터와 연산을 공유하는 방법을 탐구하고 있습니다
- 🎯 주요 분야: **임베디드 시스템 · 실시간 데이터 파이프라인 · 센서 융합 · 고성능 컴퓨팅**
- 🛰️ 장기 목표: 소규모 부대 단위 네트워크 기반의 **지휘통제(C2)** 및 전장 관리 시스템
- 🔧 하드웨어 직접 제작 — 회로·전원 설계, CAD 기반 3D 프린팅 하우징, PCB 에칭, 3D 프린터 제작
- 🌐 한국어 / 영어

---

### 🚀 주요 프로젝트

#### 🎯 IFCAS — 대드론 보병 사격 통제 보조 체계 `2026.06 ~ 진행 중`
> 광학, 거리 측정, 관성 센싱, 액추에이터를 하나로 통합한 대드론 사격 통제 보조 장치입니다.
> **진행 상황:** 하드웨어 제작 완료 · 펌웨어 및 Jetson 소프트웨어 개발 중 (UART 기반 LRF 데이터 수신 구현 완료)

- **이중 연산 구조**: STM32H523 (Cortex-M33, RTOS) ↔ Jetson Orin Nano를 **CAN**으로 연결
- **센서 타이밍 동기화**: STM32가 GPIO로 OV9281 글로벌 셔터 카메라의 촬영 시점을 트리거해, 영상 프레임과 IMU / LRF 데이터의 타이밍을 정렬
- **자체 설계 전원부**: BMS와 퓨즈를 적용한 4S Li-ion 배터리 → 독립된 4개 벅 컨버터 계통 (12V ×2 / 5V / 3.3V)
- **EMI 차폐**: 벅 컨버터와 냉각팬 주변을 차폐해 IMU / 카메라 신호 보호
- **가변 배율 광학계** (5–50mm): 포텐셔미터 기반 줌 배율 감지
- **안전 인터락 액추에이터**: 단일 레버 방식의 솔레노이드 방아쇠 잠금 장치, 잠금 후퇴 확인 스위치로 동작 제어
- *개발 중*: IMU (LSM6DS3) 자세 추정, Jetson 기반 드론 탐지, LRF 거리와 카메라 방향 정보를 **각도 공간**에서 칼만 필터로 융합하는 줌 배율 무관 표적 추적
- 반동 재현을 위한 모의 총기 테스트 플랫폼 (HK416D EBB)과 자체 설계 3D 프린팅 하우징

<br>

#### ⚡ TEFFP Seeker — Target Exposure Factor Function Parameters Seeker `2025.07 ~ 2026.03`
> ATM-Eta 전략의 파라미터를 탐색하는 GPU 가속 백테스팅·최적화 엔진으로, **Triton** 커널 기반으로 구현했습니다.

- **파라미터 세트당 하나의 Triton 레인** — 수천 개의 분봉 단위 전체 기간 백테스트를 단일 GPU에서 동시에 실행
- RTX 3080 Ti에서 **이론 메모리 대역폭의 약 98.7%** 달성
- **단일 패스 잔고 추세 평가** — 누적 최소제곱 합으로 성장률과 변동성을 닫힌 형태로 계산해, 데이터 길이와 무관하게 레인당 메모리를 일정하게 유지
- 정밀도 반올림과 **float64 누적**으로 catastrophic cancellation 문제 해결, float64 모드에서 CPU 레퍼런스 시뮬레이터와 완전 일치 검증
- **개체군 기반 탐색**: 중앙 차분 수치 그래디언트 + Adam 방식 업데이트 + 자체 개발 재생성 기법, 최대 낙폭(MDD) 필터 적용
- **실제 거래소와 동일한 시뮬레이션**: 구간별 유지 증거금 기반 청산, 격리/교차 마진 계산, 틱/스텝 단위 정밀도 처리
- 최적화된 파라미터를 **ATM-Eta 매매 설정**으로 바로 내보내기
- 🔗 [kimlvis31/TEFFPSeeker](https://github.com/kimlvis31/TEFFPSeeker)

<br>

#### 📈 ATM-Eta — Auto Trade Machine Eta `2024.09 ~ 2026.05`
> 실시간 시계열 데이터 수집, 분석, 백테스팅, 실매매 실행까지 단독으로 개발한 엔드투엔드 플랫폼입니다 — **약 73,000줄.**

- **9개 프로세스 구조**와 자체 IPC 프로토콜 (FAR/FARR) — GUI, 데이터 수집, 분석, 시뮬레이션, 매매 실행이 서로를 블로킹하지 않도록 설계
- **통합 시장 데이터 파이프라인**: 4종의 이기종 스트림 (kline / aggTrade / depth / metric)을 1분 기준으로 정규화하고, 필요 시 다중 타임프레임으로 집계
- **2단계 데이터 공백 탐지**와 명시적 데이터 출처 태깅, Binance Vision + REST 기반 보완 수집, 더미 구간 복구 (재수집 / LAN 가져오기)
- **다중 장비 연속성 확보**: 유지보수 중에는 LAN상의 다른 장비가 수집을 이어받고, 이후 구간 메타데이터 기반으로 DB 간 공백을 동기화
- **TimescaleDB** 저장 구조로 **약 78% 압축**, 트랜잭션 기반 배치 쓰기, 인덱스 자동 복구
- **거래소 상태 정합성 확보**: 불확실한 주문은 무작정 재시도하지 않고 `clientOrderId`로 검증, 선체결은 진행 중인 주문에 귀속
- **우선순위 기반 API 호출 한도 관리**와 make-before-break 방식의 WebSocket 갱신
- **TEF 전략 인터페이스**로 분석과 실행을 분리 — 전략을 GPU 최적화 엔진으로 그대로 이식 가능
- **scrypt + Fernet** 기반 암호화 계정 파일 (AAF), 자체 제작 **Pyglet** 실시간 차트 GUI
- Binance Futures에서 **118일간 실운용**으로 검증 — 연결 단절, 호출 한도, 스트림 끊김 상황에서 자동 복구
- 🔗 [kimlvis31/AutoTradeMachine_Eta](https://github.com/kimlvis31/AutoTradeMachine_Eta)

<br>

#### 🧪 ATM Alpha ~ Zeta `2023.06 ~ 2024.09`
> ATM-Eta의 기반을 다진 6세대에 걸친 반복 개발 버전입니다.

---

### 🛠️ 기술 스택

**언어**  
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![C](https://img.shields.io/badge/C-00599C?style=flat-square&logo=c&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=cplusplus&logoColor=white)

**임베디드 & 하드웨어**  
![STM32](https://img.shields.io/badge/STM32-03234B?style=flat-square&logo=stmicroelectronics&logoColor=white)
![NVIDIA Jetson](https://img.shields.io/badge/Jetson-76B900?style=flat-square&logo=nvidia&logoColor=white)
![RTOS](https://img.shields.io/badge/RTOS-555555?style=flat-square)
![Fusion 360](https://img.shields.io/badge/Fusion_360-0696D7?style=flat-square&logo=autodesk&logoColor=white)
![LTspice](https://img.shields.io/badge/LTspice-555555?style=flat-square)

**연산 & 라이브러리**  
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![Triton](https://img.shields.io/badge/Triton-555555?style=flat-square)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white)
![Pyglet](https://img.shields.io/badge/Pyglet-555555?style=flat-square)

**데이터베이스**  
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![TimescaleDB](https://img.shields.io/badge/TimescaleDB-FDB515?style=flat-square&logo=timescale&logoColor=black)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)

**DevOps & OS**  
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=flat-square&logo=ubuntu&logoColor=white)

---

### 📜 자격증 및 어학
- 정보처리기사 — 필기 합격, 실기 준비 중
- 임베디드기사 — 필기 합격, 실기 준비 중
- 영어 — OPIc AL, TOEIC 985
