# Live Editor for OBS 다운로드

OBS Studio에서 치지직 방송 제목, 카테고리, 태그를 수정할 수 있는 Windows용 플러그인입니다.

## 최신 버전

현재 버전은 `0.2.0`입니다.

[Windows x64 무설치 ZIP 다운로드 (권장)](https://github.com/TereBin/obs-live-editor-releases/releases/download/v0.2.0/obs-live-editor-0.2.0-windows-x64-portable.zip)

[Windows x64 설치 파일 다운로드](https://github.com/TereBin/obs-live-editor-releases/releases/download/v0.2.0/obs-live-editor-0.2.0-windows-x64-setup.exe)

> **Defender 오탐 안내:** 현재 설치 파일이 일부 PC에서 `Trojan:Win32/Wacatac.C!ml`로 탐지되는 사례가 있어 Microsoft에 오탐 분석을 요청했습니다. 분석이 완료될 때까지는 위의 무설치 ZIP 사용을 권장합니다. Windows 보안 기능을 끄거나 백신 예외를 추가하지 마세요. ZIP 내부 파일도 탐지될 경우 설치를 중단하고 [Issues](https://github.com/TereBin/obs-live-editor/issues)에 알려주세요.

## 주요 기능

- OBS Studio 도크에서 치지직 방송 제목 조회 및 변경
- 카테고리 검색, 선택 및 제거
- 방송 태그 조회, 변경 및 전체 제거
- 브라우저를 이용한 치지직 OAuth 로그인
- Access Token 자동 갱신
- Windows DPAPI를 이용한 로그인 토큰 암호화 저장
- 새 버전 자동 확인 및 중요도별 업데이트 알림
- 최소 지원 버전 미만 또는 긴급 보안 업데이트 시 필수 업데이트 안내

## 요구 사항

- Windows 10 또는 Windows 11 64비트
- OBS Studio 32.2.2 이상 64비트
- 치지직 스트리머 계정
- 인터넷 연결

## 무설치 ZIP 설치 (권장)

1. OBS Studio를 종료합니다.
2. 무설치 ZIP을 내려받아 압축을 풉니다.
3. 압축 안의 `bin`, `data`, `obs-plugins` 폴더를 OBS 설치 폴더(기본값: `C:\Program Files\obs-studio`)에 복사합니다.
4. 파일 복사 중 관리자 권한 요청이 나타나면 승인합니다.
5. OBS Studio를 다시 실행하고 `도크` 메뉴에서 `라이브 정보 편집`을 엽니다.

<details>
<summary><strong>폴더 복사 위치 자세히 보기</strong></summary>

압축을 풀면 다음 세 폴더가 보입니다.

```text
bin
data
obs-plugins
```

개별 DLL만 꺼내지 말고 **세 폴더를 폴더째 모두 선택**하여 OBS 설치 폴더 안에 복사하세요. 기본 설치 위치는 다음과 같습니다.

```text
C:\Program Files\obs-studio
```

Windows에서 같은 이름의 폴더가 있다는 메시지가 나타나면 폴더 병합과 파일 덮어쓰기를 허용합니다. 복사가 끝난 뒤 파일 위치는 정확히 다음과 같아야 합니다.

```text
C:\Program Files\obs-studio\bin\64bit\tls\qschannelbackend.dll
C:\Program Files\obs-studio\obs-plugins\64bit\obs-live-editor.dll
C:\Program Files\obs-studio\data\obs-plugins\obs-live-editor\locale\ko-KR.ini
C:\Program Files\obs-studio\data\obs-plugins\obs-live-editor\locale\en-US.ini
```

특히 `qschannelbackend.dll`은 `tls` 폴더 밖으로 따로 옮기면 안 됩니다. 위치가 잘못되면 로그인할 때 `TLS initialization failed` 오류가 발생합니다.

다음과 같이 폴더가 한 번 더 중복된 경로도 잘못된 설치입니다.

```text
C:\Program Files\obs-studio\bin\bin\64bit\tls\qschannelbackend.dll
C:\Program Files\obs-studio\obs-plugins\obs-plugins\64bit\obs-live-editor.dll
```

문제가 계속되면 OBS에서 `도움말 > 로그 파일 > 현재 로그 보기`를 열고 아래 문구가 있는지 확인하세요.

```text
[obs-live-editor] plugin loaded (version 0.2.0)
```

</details>

## EXE 설치

Microsoft의 오탐 분석이 끝난 뒤에는 설치 파일을 이용할 수 있습니다.

1. OBS Studio를 종료합니다.
2. 설치 파일을 내려받아 실행합니다.
3. 관리자 권한 요청을 승인하고 설치를 완료합니다.
4. OBS Studio를 다시 실행합니다.
5. OBS의 `도크` 메뉴에서 `라이브 정보 편집`을 엽니다.

현재 배포 파일은 코드 서명이 되어 있지 않습니다. 무결성을 확인하려면 아래 명령의 결과를 [SHA256SUMS.txt](./SHA256SUMS.txt)와 비교합니다.

```powershell
Get-FileHash .\obs-live-editor-0.2.0-windows-x64-portable.zip -Algorithm SHA256
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

EXE로 설치했다면 Windows의 `설정 > 앱 > 설치된 앱`에서 `Live Editor for OBS`를 제거합니다.

무설치 ZIP으로 설치했다면 OBS를 종료한 뒤 다음 파일을 직접 삭제합니다.

```text
C:\Program Files\obs-studio\obs-plugins\64bit\obs-live-editor.dll
C:\Program Files\obs-studio\bin\64bit\tls\qschannelbackend.dll
C:\Program Files\obs-studio\data\obs-plugins\obs-live-editor\
```

## 보안과 소스 코드

로그인 토큰은 Windows DPAPI로 암호화되어 현재 Windows 사용자만 읽을 수 있는 로컬 파일에 저장됩니다. Client Secret과 실제 사용자 토큰은 이 저장소에 포함되지 않습니다.

소스 코드, 빌드 방법, Worker 구성은 [obs-live-editor 소스 저장소](https://github.com/TereBin/obs-live-editor)에서 확인할 수 있습니다. 이 프로그램은 GPL-2.0 라이선스로 배포됩니다.

## 문제 보고

오류를 보고할 때는 소스 저장소의 Issues를 이용해 주세요. Access Token, Refresh Token, Client Secret 또는 `credentials.bin` 파일을 첨부하지 마세요.

## 후원

Live Editor for OBS가 도움이 되었다면 [Ko-fi에서 TereBin 후원하기](https://ko-fi.com/terebin)를
통해 개발을 응원할 수 있습니다.
