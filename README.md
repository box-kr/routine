# Routine (macOS Automation)

<div align="center">

**🚀 macOS 사용자 패턴 기반 자동화 시스템**

시간, Wi-Fi, 배터리, 시스템 상태 등의 트리거를 감지하여 볼륨 조절, 앱 실행, 시스템 설정 변경 등을 자동으로 수행하는 유틸리티 앱입니다.

![macOS](https://img.shields.io/badge/macOS-13.0+-blue)
![Swift](https://img.shields.io/badge/Swift-5.9+-orange)

</div>

## 📦 설치 방법 (Installation)

Homebrew를 사용하여 터미널에서 간편하게 설치하고 업데이트할 수 있습니다.

```bash
# 1. 저장소 Tap 추가
brew tap box-kr/homebrew-routine

# 2. Routine 앱 설치
brew install --cask box-kr/routine/routine
```

### 업데이트 방법 (Update)

```bash
brew upgrade --cask box-kr/routine/routine
```


## ✨ 주요 기능

Routine은 다양한 **트리거(Triggers)**와 **액션(Actions)**을 조합하여 나만의 자동화 파이프라인을 구축할 수 있습니다.

### 🎯 지원 트리거 (8종)
- **시간/요일**: 특정 시간에 반복되거나 일회성 자동화 실행.
- **Wi-Fi 연결/해제**: 특정 SSID 연결 시(`*` 와일드카드 지원) 작업 수행.
- **LAN 연결/해제**: 유선 네트워크(LAN)의 연결 및 해제 상태 감지.
- **배터리 임계치**: 배터리 잔량이 설정한 % 이하/이상이 될 때 실행.
- **전원 상태**: 충전 시작, 충전 중, 배터리 사용 시점 감지.
- **화면 잠금/해제**: 맥북 덮개를 닫거나 화면이 잠길 때의 동작 정의.
- **키보드 조합키**: 특정 단축키(Hotkeys) 입력 시 액션 트리거.

### ⚡ 지원 액션 (10종)
- **볼륨/밝기**: 스피커 볼륨 및 화면 밝기 자동 조절.
- **Wi-Fi/Bluetooth**: 통신 모드를 즉시 켜거나 끄기.
- **일시적 Wi-Fi**: 지정된 시간 동안 Wi-Fi 상태를 변경하고, 이더넷 감지 등 조건에 따라 복구.
- **다크 모드**: 시스템 테마를 다크/라이트 모드로 전환.
- **방해 금지**: 집중 모드(Do Not Disturb) 활성화 및 해제.
- **앱 실행**: 필요한 작업용 앱(VSCode, Chrome 등) 자동 실행.
- **알림 시스템**: 루틴 실행 결과를 macOS 기본 알림으로 전송.
- **키보드 차단**: 내장 키보드 입력을 의도적으로 제한(먼지 청소 모드 등).

---

## 🔒 필수 권한 설정 (중요)

Routine 앱은 시스템 제어 특성상 다음과 같은 macOS 권한이 필요합니다. 앱 최초 실행 시 또는 기능 사용 전 설정이 필요할 수 있습니다.

1. **위치 서비스 (Location Services)**: 
   - 연결된 Wi-Fi의 이름(SSID)을 조회하기 위해 필요합니다.
2. **접근성 (Accessibility)**: 
   - 키보드 조합키 트리거 및 내장 키보드 차단 기능을 위해 필수적입니다.
3. **알림 (Notifications)**: 
   - 자동화 실행 성공 여부를 사용자에게 알리기 위해 사용됩니다.
4. **Apple Events**: 
   - 일부 시스템 설정 조절 및 앱 실행 제어를 위해 권한 승인이 필요합니다.

---

## 🛠️ 기술 사양

- **언어 및 프레임워크**: Swift 5.9, SwiftUI
- **시스템 인터페이스**: AppKit (NSStatusItem, NSPopover), CoreWLAN (Networking)
- **하드웨어 제어**: IOKit (Battery, Display Brightness)
- **이벤트 핸들링**: CoreGraphics (Event Tap for Keyboard)
- **데이터 관리**: UserDefaults 기반 `RoutineStore`

---

## 📝 릴리즈 노트

**v1.0.2 (최신 업데이트)**
- **앱 내 자동 업데이트**: Homebrew를 이용한 앱 내 업데이트 확인 및 원클릭 설치 기능 추가.
- **신규 트리거**: 유선 LAN 연결/해제 감지 트리거 추가.
- **신규 액션**: 설정한 시간 동안 동작 후 복구되는 일시적 Wi-Fi(Temporary Wi-Fi) 제어 액션 추가.
- **루틴 논리 옵션**: 여러 개의 트리거가 등록된 경우, 실행 조건을 `Any(하나라도 만족)` 또는 `All(모두 만족)`로 설정할 수 있는 기능 추가.
- **다국어 업데이트**: 신규 기능에 대한 한국어, 영어 로케일 문자열 추가 반영.

**v1.0.0 (Initial Public Release)**
- **다국어 지원(i18n)**: 영어, 한국어, 일본어, 중국어(간체) 완벽 지원.
- **엔진 안정화**: 루틴 생성/수정/삭제 및 복제 기능 안정화.
- **시스템 통합**: 7종 트리거(시간, Wi-Fi, 배터리 등) 및 9종 액션 통합 시스템 구축.
- 메뉴바(StatusBar) 전용 팝오버 UI 구현.

---

## ❗️ 문제 해결

**"개발자를 확인할 수 없습니다" 메시지가 나타날 때:**
빌드된 앱은 Ad-hoc 서명으로 구성되어 macOS Gatekeeper가 차단할 수 있습니다. 터미널에서 다음 명령어를 실행하여 격리 속성을 해제하세요:
```bash
xattr -cr /Applications/Routine.app
# 또는 dist 폴더에 있는 경우
xattr -cr dist/Routine.app
```

---

## 🔗 링크
- [Routine 공식 프로젝트 리포지토리](https://github.com/box-kr/routine)
- 기능 제안 및 버그 제보는 GitHub 이슈를 통해 남겨주세요!
