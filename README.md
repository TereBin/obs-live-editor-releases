# Live Editor for OBS 다운로드

OBS Studio에서 치지직 방송 제목, 카테고리, 태그를 수정할 수 있는 Windows용 플러그인입니다.

## 최신 버전

현재 버전은 `0.2.0`입니다.

[Windows x64 설치 파일 다운로드](https://github.com/TereBin/obs-live-editor-releases/releases/download/v0.2.0/obs-live-editor-0.2.0-windows-x64-setup.exe)

요구 사항:

- Windows 10 또는 Windows 11 64비트
- OBS Studio 64비트
- 치지직 스트리머 계정

## 설치

1. OBS Studio를 종료합니다.
2. 위의 설치 파일을 내려받아 실행합니다.
3. 관리자 권한 요청을 승인하고 설치를 완료합니다.
4. OBS Studio를 다시 실행합니다.
5. OBS의 `도크` 메뉴에서 `라이브 정보 편집`을 엽니다.

현재 설치 파일은 코드 서명이 되어 있지 않아 Windows SmartScreen 경고가 나타날 수 있습니다. `추가 정보`를 선택한 뒤 게시자와 파일을 확인하고 실행하세요. 무결성을 확인하려면 아래 명령의 결과를 [SHA256SUMS.txt](./SHA256SUMS.txt)와 비교합니다.

```powershell
Get-FileHash .\obs-live-editor-0.2.0-windows-x64-setup.exe -Algorithm SHA256
```

## 사용

1. `로그인`을 누르고 브라우저에서 치지직 로그인을 완료합니다.
2. 방송 제목을 입력합니다.
3. 카테고리 이름을 두 글자 이상 입력하고 검색 결과에서 선택합니다.
4. 태그는 쉼표로 구분해 입력합니다.
5. `적용`을 눌러 변경 내용을 저장합니다.

`새로고침`은 현재 방송 정보를 다시 불러옵니다. 카테고리 오른쪽의 초기화 버튼을 누른 뒤 적용하면 카테고리가 제거됩니다.

플러그인은 하루에 한 번 새 버전을 확인합니다. 일반 업데이트는 도크 상단에 표시되며, 현재 버전이 최소 지원 버전보다 낮거나 긴급 보안 업데이트가 필요한 경우 필수 업데이트 경고가 표시되고 방송 정보 변경 기능이 비활성화됩니다.

## 삭제

Windows의 `설정 > 앱 > 설치된 앱`에서 `Live Editor for OBS`를 제거합니다.

## 보안과 소스 코드

로그인 토큰은 Windows DPAPI로 암호화되어 현재 Windows 사용자만 읽을 수 있는 로컬 파일에 저장됩니다. Client Secret과 실제 사용자 토큰은 이 저장소에 포함되지 않습니다.

소스 코드, 빌드 방법, Worker 구성은 [obs-live-editor 소스 저장소](https://github.com/TereBin/obs-live-editor)에서 확인할 수 있습니다. 이 프로그램은 GPL-2.0 라이선스로 배포됩니다.

## 문제 보고

오류를 보고할 때는 소스 저장소의 Issues를 이용해 주세요. Access Token, Refresh Token, Client Secret 또는 `credentials.bin` 파일을 첨부하지 마세요.

---

[개발자 후원하기](https://ko-fi.com/terebin)
