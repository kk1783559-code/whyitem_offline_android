# WHYITEM — 평행우주 오프라인 RPG (초기 MVP)

스마트폰 안에서 각자 독립된 평행우주를 생성하고, 인터넷 연결 없이 플레이하는 한글/영어 지원 텍스트 RPG입니다.

## 구현된 기능

- 한국어 / 영어 전환
- 스마트폰 세로 화면에 맞춘 가독성 중심 UI
- 서로 독립적인 월드를 여러 개 생성
- 월드별 시드, 성향, 세계 법칙, 혼돈 지수 생성
- 무작위 아이템 이름·등급·능력치·옵션 생성
- 탐험, 사건, 세계 역사 기록
- 월드 규칙에 따라 생성되는 모의 전투
- 이미지가 없는 아이템은 `?`로 표시하고 이미지 등록 유도
- 휴대폰에서 직접 선택한 이미지 파일을 기기 내부 IndexedDB에 저장
- 월드 하나 또는 전체 월드를 JSON으로 백업/복원
- 게임 실행 중 서버·계정·외부 AI API 호출 없음

## 꼭 알아둘 점

이 파일은 **플레이 가능한 초기 MVP 소스 프로젝트**입니다. Google Play에 바로 업로드할 서명된 APK/AAB 파일은 아직 포함되어 있지 않습니다. Android Studio에서 Android 프로젝트를 생성하고 실제 기기 테스트, 앱 서명, Play Console 설정을 마쳐야 배포할 수 있습니다.

세계 운영은 실제 생성형 AI 모델이 아니라 로컬 규칙 엔진과 무작위 생성 시스템으로 구현되어 있습니다. 따라서 AI API 비용이나 인터넷 연결은 필요 없지만, 자유로운 자연어 추론을 하는 진짜 AI가 실행되는 것은 아닙니다.

## Android 앱 빌드 방법

스마트폰에 직접 설치할 APK를 만들고 싶다면 `ANDROID_INSTALL_KO.md`의 GitHub Actions 자동 빌드 안내를 따라 주세요. 이 저장소에는 APK 자동 빌드 워크플로가 포함되어 있습니다.


필요한 것: PC, Node.js LTS, Android Studio, Android SDK, Android Gradle Plugin이 요구하는 Java 버전.

1. ZIP 파일을 PC에 압축 해제합니다.
2. 프로젝트 폴더에서 터미널을 엽니다.
3. 아래 명령을 순서대로 실행합니다.

```bash
npm install
npx cap add android
npx cap sync android
npx cap open android
```

4. Android Studio에서 실제 안드로이드 폰으로 실행해 봅니다.
5. 비행기 모드에서 월드 생성, 저장, 앱 강제 종료 후 복원, 이미지 등록, 백업/복원, 언어 전환을 테스트합니다.
6. 앱 아이콘, 버전, 서명키, 개인정보/데이터 안전성 항목 등을 설정한 뒤 Android Studio의 **Generate Signed Bundle / APK → Android App Bundle**에서 `.aab`를 생성합니다.
7. Google Play Console에서 앱 등록, 테스트, 심사 제출을 진행합니다.

`npx cap add android`에서 Android 플랫폼이 이미 있다고 나오면 해당 명령은 건너뛰고 `npx cap sync android`를 실행하면 됩니다.

## 데이터와 이미지 저장

- 월드 데이터와 아이템 이미지는 앱 내부 WebView의 IndexedDB에 저장됩니다.
- 이미지는 기기에서 처리하며, 저장 공간 절약을 위해 긴 변 기준 최대 512px로 줄여 저장합니다.
- 앱 데이터를 지우거나 앱을 삭제하면 백업하지 않은 데이터가 사라질 수 있습니다. 주기적으로 JSON 백업을 내보내세요.
- 엄격한 오프라인 제품으로 배포하려면 최종 Android Manifest에서 불필요한 권한을 검토하고, 분석 SDK·광고 SDK·원격 폰트·원격 이미지 등 네트워크 의존성을 추가하지 마세요.

## 가격

다운로드 가격 1,000원은 소스 코드에 하드코딩하지 않습니다. Google Play Console에서 일회성 유료 앱으로 설정합니다. 실제 가격 및 판매 가능 여부는 국가/지역 설정과 Play Console 정책에 따릅니다.
