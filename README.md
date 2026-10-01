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
- **패키지**: VQFN-32 또는 TSSOP-28
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

## 필요한 도구 및 장비

## 문서

- [개발계획서](개발계획서.md) - 목표, 설계, 할 일 목록, 일정
- [개발로그](개발로그.md) - 분석 결과, 발견사항, 변경 이력

---

**라이센스**: [라이센스 정보 추가 예정]  
**기여**: 이슈와 풀 리퀘스트를 환영합니다!
