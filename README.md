# One2Touch Keyboard Hack

![One2Touch Keyboard Module](images/20250720_211616%20(2).jpg)

## 프로젝트 개요

이 프로젝트는 타오바오에서 구입한 One2Touch 터치 키보드 모듈을 분석하고 역공학을 통해 설계를 이해하며, 커스터마이징 및 해킹을 목적으로 하는 프로젝트입니다.

## 목표

- 🔍 One2Touch 터치 키보드 모듈의 하드웨어 분석
- 🛠️ 펌웨어 역공학 및 분석
- 📋 회로도 및 PCB 설계 복원
- 🔧 커스텀 펌웨어 개발
- 📚 완전한 기술 문서화

## 프로젝트 구조

```
One2Touch_Keyboard_hack/
├── docs/                   # 문서 및 분석 자료
│   ├── hardware/          # 하드웨어 분석 자료
│   └── datasheets/        # 데이터시트 모음
├── sch
│   
│   └ easyEDA
└── images/               # 사진 및 이미지 자료
    ├── teardown/         # 분해 과정 사진
    └── pcb_analysis/     # PCB 분석 이미지
```

## 하드웨어 정보

### One2Touch 키보드 모듈 사양
- **구입처**: 타오바오 (Taobao)
- **구매링크**: [One2Touch Touch Keyboard Module](https://item.taobao.com/item.htm?&id=659293613694)
- **타입**: 용량성 터치 키보드
- **인터페이스**: [분석 중]
- **메인 MCU**: MSP430FR2633 (Texas Instruments)
- **RFID 칩**: NT3H2111W0FTTJ (NXP Semiconductors)

## 주요 IC 정보

### MSP430FR2633 (메인 컨트롤러)
- **제조사**: Texas Instruments
- **타입**: 16-bit Ultra-Low-Power Microcontroller
- **메모리**: 16KB FRAM, 4KB SRAM
- **패키지**: VQFN-32 (RHB)
- **주요 특징**: 
  - CapTIvate™ 터치 기술 지원
  - 초저전력 설계
  - 내장 12-bit ADC
  - 다중 커뮤니케이션 인터페이스 (UART, SPI, I2C)

### NT3H2111W0FTTJ (RFID/NFC 칩)
- **제조사**: NXP Semiconductors
- **타입**: NFC Forum Type 2 Tag with I2C Interface
- **메모리**: 924 bytes EEPROM
- **인터페이스**: I2C (Fast mode up to 1 Mbit/s)
- **주요 특징**:
  - ISO14443 Type A 호환
  - Energy Harvesting 지원
  - Pass-through mode
  - Field Detection 핀

## 핀맵 및 연결

> 핀 번호는 MSP430FR2633 **VQFN-32 (RHB)**, NT3H2111 **TSSOP8** 기준이에요.

### MSP430FR2633 핀맵 (보드에서의 용도)

| 핀 | 기능 | 보드 연결 |
|---|---|---|
| 1 | RST/NMI/SBWTDIO | SBW 프로그래밍 |
| 2 | TEST/SBWTCK | SBW 프로그래밍 |
| 3 | P1.4/UCA0TXD | 미확인 |
| 4 | P1.5/UCA0RXD | 미확인 |
| 5 | P1.6 | 미확인 |
| 6 | P1.7 | 미확인 |
| 7 | P1.0 | 미확인 |
| 8 | P1.1 | 미확인 |
| 9 | P1.2/UCB0SDA | I2C SDA → NT3H2111 5번 |
| 10 | P1.3/UCB0SCL | I2C SCL → NT3H2111 3번 |
| 11 | P2.2 | NT3H2111 4번 (FD) |
| 12 | P3.0/CAP0.0 | 터치 5행 |
| 13 | CAP0.1 | 터치 4행 |
| 14 | P2.3/CAP0.2 | 터치 5열 |
| 15 | CAP0.3 | 터치 9열 |
| 16 | P3.1/CAP1.0 | 터치 3행 |
| 17 | P2.4/CAP1.1 | 터치 11열 |
| 18 | P2.5/CAP1.2 | 터치 7열 |
| 19 | P2.6/CAP1.3 | 터치 3열 |
| 20 | VREG | 내부 레귤레이터 (커패시터) |
| 21 | CAP2.0 | 터치 2행 |
| 22 | CAP2.1 | 터치 1열 |
| 23 | CAP2.2 | 터치 4열 |
| 24 | CAP2.3 | 터치 8열 |
| 25 | P2.7/CAP3.0 | 터치 10열 |
| 26 | CAP3.1 | 터치 6열 |
| 27 | P3.2/CAP3.2 | 터치 2열 |
| 28 | CAP3.3 | 터치 1행 |
| 29 | P2.0/XOUT | 미확인 |
| 30 | P2.1/XIN | 미확인 |
| 31 | DVSS | GND |
| 32 | DVCC | NT3H2111 6번 (VCC), 7번 (VOUT) |

### NT3H2111 핀맵

| 핀 | 기능 | 보드 연결 |
|---|---|---|
| 1 | LA | 안테나 |
| 2 | VSS | GND |
| 3 | SCL | MSP430 10번 |
| 4 | FD (필드 감지) | MSP430 11번 (P2.2) |
| 5 | SDA | MSP430 9번 |
| 6 | VCC | MSP430 32번 (DVCC) |
| 7 | VOUT (에너지 하베스팅) | MSP430 32번 (DVCC) |
| 8 | LB | 안테나 |

### MSP430 ↔ NT3H2111 연결 요약

| MSP430 | NT3H2111 | 용도 |
|---|---|---|
| 9 (SDA) | 5 (SDA) | I2C |
| 10 (SCL) | 3 (SCL) | I2C |
| 11 (P2.2) | 4 (FD) | NFC 필드 감지 (MCU 깨우기용으로 추정) |
| 32 (DVCC) | 6 (VCC), 7 (VOUT) | 에너지 하베스팅 전원 |

- 보드 전체 전원을 NT3H2111 에너지 하베스팅으로 공급해요 (최대 약 15mW).
  - → NFC 필드가 없으면 보드가 꺼져 있어요.
- NT3H2111 I2C 주소: `0x55`

### 터치 키 매트릭스

- PCB 터치 풋프린트 5행 × 11열, 1행 1열은 없음 → **총 54키**
- MSP430 CapTIvate 핀 16개를 모두 사용 (상호용량 방식으로 추정)

| | 1열<br>22 | 2열<br>27 | 3열<br>19 | 4열<br>23 | 5열<br>14 | 6열<br>26 | 7열<br>18 | 8열<br>24 | 9열<br>15 | 10열<br>25 | 11열<br>17 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **1행 (28)** | ✗ | ● | ● | ● | ● | ● | ● | ● | ● | ● | ● |
| **2행 (21)** | ● | ● | ● | ● | ● | ● | ● | ● | ● | ● | ● |
| **3행 (16)** | ● | ● | ● | ● | ● | ● | ● | ● | ● | ● | ● |
| **4행 (13)** | ● | ● | ● | ● | ● | ● | ● | ● | ● | ● | ● |
| **5행 (12)** | ● | ● | ● | ● | ● | ● | ● | ● | ● | ● | ● |

(괄호 안 숫자 = MSP430 핀 번호, ✗ = 풋프린트 없음)

## 필요한 도구 및 장비

## 문서

- [개발계획서](개발계획서.md) - 목표, 설계, 할 일 목록, 일정
- [개발로그](개발로그.md) - 분석 결과, 발견사항, 변경 이력

---

**라이센스**: [라이센스 정보 추가 예정]  
**기여**: 이슈와 풀 리퀘스트를 환영합니다!
