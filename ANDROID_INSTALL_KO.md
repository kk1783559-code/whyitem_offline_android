# WHYITEM Android APK 만들기 및 스마트폰 설치

현재 제공되는 파일은 Android 앱 소스입니다. 이 작업공간에는 Android SDK/Gradle 빌드 환경이 없어 APK 바이너리를 직접 컴파일하지 못합니다. 대신 GitHub Actions가 APK를 자동 빌드하도록 설정했습니다.

## APK를 받는 순서

1. ZIP을 압축 해제합니다.
2. 프로젝트 파일 전체를 새 GitHub 저장소에 업로드합니다. `.github/workflows/build-apk.yml` 파일이 저장소 안에 포함되어야 합니다.
3. GitHub 저장소의 **Actions** 탭을 엽니다.
4. **Build WHYITEM Android APK** 워크플로를 선택하고 **Run workflow**를 누릅니다. `main` 또는 `master` 브랜치에 업로드하면 자동 실행될 수도 있습니다.
5. 작업이 초록색 체크로 완료되면 실행 기록 하단의 **Artifacts**에서 `WHYITEM-Android-APK`를 다운로드합니다.
6. 내려받은 ZIP을 풀어 `app-debug.apk`를 Android 스마트폰으로 옮기거나, 스마트폰에서 직접 다운로드합니다.
7. APK를 탭해 설치합니다. Android가 안내하면 해당 파일 관리 앱/브라우저의 **알 수 없는 앱 설치 허용**을 일시적으로 켭니다. 설치 후에는 이 권한을 다시 끌 수 있습니다.
8. 앱은 일반 앱처럼 실행·삭제할 수 있습니다. 앱 삭제 시 백업하지 않은 로컬 월드와 이미지도 삭제될 수 있습니다.

## 주의

- 이 APK는 개인 기기 테스트용 **debug APK**입니다. Google Play에 게시하기 위한 정식 서명 APK/AAB가 아닙니다.
- 앱을 재빌드하면 서명키가 달라질 수 있어 기존 앱 위에 업데이트 설치가 안 될 수 있습니다. 이 경우 기존 앱을 삭제한 후 새 APK를 설치해야 하며, 먼저 월드 데이터를 백업하세요.
- GitHub Actions를 실행하려면 GitHub 계정과 저장소 업로드가 필요합니다. 이 프로젝트는 인터넷 없이 게임을 실행하도록 설계됐지만, APK를 빌드하는 과정에는 GitHub Actions와 패키지 다운로드를 위한 인터넷 연결이 필요합니다.
- 정식 Google Play 배포 전에는 release 서명키, 개인정보 처리방침 필요 여부, 앱 콘텐츠 및 데이터 안전성 항목, 실제 기기 테스트 등을 별도로 확인해야 합니다.
