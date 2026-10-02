# Live Editor for OBS

OBS Studio에서 치지직 방송 제목, 카테고리, 태그를 수정할 수 있는 Windows용 플러그인입니다.

## 다운로드

현재 버전은 `0.2.0`입니다.

[Windows x64 무설치 ZIP 다운로드 (권장)](https://github.com/TereBin/obs-live-editor-releases/releases/download/v0.2.0/obs-live-editor-0.2.0-windows-x64-portable.zip)

[Windows x64 설치 파일 다운로드](https://github.com/TereBin/obs-live-editor-releases/releases/download/v0.2.0/obs-live-editor-0.2.0-windows-x64-setup.exe)

> **Defender 안내:** EXE 설치 파일이 일부 PC에서 `Trojan:Win32/Wacatac.C!ml`로 오탐되는 사례가 있어 현재는 무설치 ZIP을 권장합니다. Windows 보안 기능을 끄거나 예외를 추가하지 마세요. 자세한 대응 방법은 [Defender 문제 해결](#다운로드-또는-검사-중-defender가-파일을-차단함)을 확인하세요.

다운로드한 파일의 무결성은 [SHA256SUMS.txt](./SHA256SUMS.txt)와 비교할 수 있습니다.

```powershell
Get-FileHash .\obs-live-editor-*-windows-x64-portable.zip -Algorithm SHA256
```

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

## 설치

### 무설치 ZIP (권장)

1. OBS Studio를 종료합니다.
2. 무설치 ZIP을 내려받아 압축을 풉니다.
3. 압축 안의 `bin`, `data`, `obs-plugins` 폴더를 OBS 설치 폴더(기본값: `C:\Program Files\obs-studio`)에 복사합니다.
4. 파일 복사 중 관리자 권한 요청이 나타나면 승인합니다.
5. OBS Studio를 다시 실행하고 `도크` 메뉴에서 `라이브 정보 편집`을 엽니다.

<a id="portable-paths"></a>
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

특히 `qschannelbackend.dll`은 `tls` 폴더 밖으로 따로 옮기면 안 됩니다. 관련 오류는 [`TLS initialization failed` 문제 해결](#로그인할-때-tls-initialization-failed가-표시됨)을 확인하세요.

다음과 같이 폴더가 한 번 더 중복된 경로도 잘못된 설치입니다.

```text
C:\Program Files\obs-studio\bin\bin\64bit\tls\qschannelbackend.dll
C:\Program Files\obs-studio\obs-plugins\obs-plugins\64bit\obs-live-editor.dll
```

문제가 계속되면 OBS에서 `도움말 > 로그 파일 > 현재 로그 보기`를 열고 아래와 같은 문구가 있는지 확인하세요.

```text
[obs-live-editor] plugin loaded (version ...)
```

</details>

### EXE 설치

현재 일부 PC에서 Defender 오탐 사례가 있으므로 가능하면 무설치 ZIP을 사용하세요. EXE가 차단되지 않는 환경에서는 다음 순서로 설치할 수 있습니다.

1. OBS Studio를 종료합니다.
2. 설치 파일을 내려받아 실행합니다.
3. 관리자 권한 요청을 승인하고 설치를 완료합니다.
4. OBS Studio를 다시 실행합니다.
5. OBS의 `도크` 메뉴에서 `라이브 정보 편집`을 엽니다.

## 사용

1. `로그인`을 누르고 브라우저에서 치지직 로그인을 완료합니다.
2. 방송 제목을 입력합니다.
3. 카테고리 이름을 두 글자 이상 입력하고 검색 결과에서 선택합니다.
4. 태그는 쉼표로 구분해 입력합니다.
5. `적용`을 눌러 변경 내용을 저장합니다.

`새로고침`은 현재 방송 정보를 다시 불러옵니다. 카테고리 오른쪽의 초기화 버튼을 누른 뒤 적용하면 카테고리가 제거됩니다.

### 업데이트 확인

플러그인은 OBS가 실행 중일 때만 업데이트를 확인합니다. 마지막 확인 후 24시간 이상 지났다면 다음 OBS 실행 시 한 번 확인하며, 자동으로 다운로드하거나 설치하지 않습니다. 일반 업데이트는 도크 상단에 표시됩니다. 현재 버전이 최소 지원 버전보다 낮거나 긴급 보안 업데이트가 필요한 경우 방송 정보 변경 기능이 비활성화되고 필수 업데이트가 안내됩니다.

## 삭제

EXE로 설치했다면 Windows의 `설정 > 앱 > 설치된 앱`에서 `Live Editor for OBS`를 제거합니다.

무설치 ZIP으로 설치했다면 OBS를 종료한 뒤 다음 파일을 직접 삭제합니다.

```text
C:\Program Files\obs-studio\obs-plugins\64bit\obs-live-editor.dll
C:\Program Files\obs-studio\bin\64bit\tls\qschannelbackend.dll
C:\Program Files\obs-studio\data\obs-plugins\obs-live-editor\
```

## 문제 해결

### `도크` 메뉴에 `라이브 정보 편집`이 없음

- **확인:** OBS에서 `도움말 > 로그 파일 > 현재 로그 보기`를 열고 `[obs-live-editor] plugin loaded`를 검색합니다.
- **해결:** 해당 문구가 없다면 OBS를 완전히 종료한 뒤 [폴더 복사 위치](#portable-paths)에 따라 ZIP의 세 폴더를 다시 복사하고 OBS를 실행합니다.

### 로그에 이전 플러그인 버전이 표시됨

- **확인:** 로그의 `[obs-live-editor] plugin loaded (version ...)`이 [다운로드](#다운로드)에 표시된 현재 버전과 같은지 확인합니다.
- **해결:** OBS를 완전히 종료하고 최신 ZIP을 다시 내려받은 뒤 [설치 안내](#설치)에 따라 세 폴더를 모두 덮어씁니다. OBS가 실행 중이면 기존 DLL이 교체되지 않을 수 있습니다.

### 로그인할 때 `TLS initialization failed`가 표시됨

- **확인:** 로그에 `No functional TLS backend was found` 또는 `No TLS backend is available`이 있는지 확인합니다. 다음 파일도 확인합니다.

  ```text
  C:\Program Files\obs-studio\bin\64bit\tls\qschannelbackend.dll
  ```

- **해결:** `qschannelbackend.dll`만 따로 옮기지 말고 [폴더 복사 위치](#portable-paths)에 따라 ZIP의 `bin` 폴더를 폴더째 다시 복사한 뒤 OBS를 실행합니다.

### 로그인 버튼을 눌러도 브라우저가 열리지 않음

- **확인:** 인터넷 연결과 Windows 기본 브라우저 설정을 확인하고, OBS 도크에 표시된 오류 문구를 확인합니다.
- **해결:** 기본 브라우저를 지정한 뒤 OBS를 다시 실행합니다. VPN, 프록시 또는 보안 프로그램이 연결을 차단하는 경우 일시적으로 다른 네트워크에서 다시 시도하되 Windows 보안 기능을 끄지는 마세요.

### 브라우저 로그인은 끝났지만 OBS가 로그인 상태로 바뀌지 않음

- **확인:** 브라우저의 로그인 완료 화면이 표시됐는지, OBS 도크에 로그인 검증 또는 토큰 발급 오류가 있는지 확인합니다.
- **해결:** OBS로 돌아와 잠시 기다린 뒤 다시 시도합니다. 계속 실패하면 OBS를 재실행하고 로그인 과정을 처음부터 진행합니다. 로그인 중에는 OBS를 종료하지 마세요.

### 카테고리 검색 결과가 나타나지 않음

- **확인:** 카테고리 이름을 두 글자 이상 입력했는지 확인합니다. 한글 입력은 조합 완료 후 약 350ms 뒤 검색됩니다.
- **해결:** 입력을 마친 뒤 잠시 기다리고, 나타난 검색 결과를 직접 선택합니다. 텍스트만 입력하고 결과를 선택하지 않으면 적용할 수 없습니다.

### 방송 정보가 적용되지 않음

- **확인:** 로그인 상태인지, 방송 제목이 비어 있지 않은지, 카테고리를 검색 결과에서 선택했는지 확인합니다. 태그에는 글자와 숫자만 사용할 수 있습니다.
- **해결:** `새로고침`으로 현재 방송 정보를 다시 불러온 뒤 값을 수정하고 `적용`을 누릅니다. 오류가 계속되면 로그와 도크의 오류 문구를 함께 확인합니다.

### 새 버전 알림이 표시되지 않음

- **확인:** [업데이트 확인 방식](#업데이트-확인)에 따라 마지막 확인 후 24시간이 지났는지 확인합니다.
- **해결:** 인터넷 연결을 확인하고 다음 확인 시점에 OBS를 실행합니다. 새 버전이 있으면 알림의 배포 페이지에서 직접 내려받아 설치합니다.

### 다운로드 또는 검사 중 Defender가 파일을 차단함

- **확인:** Windows 보안의 `바이러스 및 위협 방지 > 보호 기록`에서 탐지 이름과 영향을 받은 파일을 확인합니다.
- **해결:** 보안 기능을 끄거나 예외를 추가하지 마세요. EXE가 차단되면 [무설치 ZIP](#다운로드)을 사용하고 체크섬을 확인합니다. ZIP 내부 파일도 탐지되면 설치를 중단하고 탐지 이름을 포함해 문제를 보고해 주세요.

## 문제 보고

오류 보고와 기능 제안은 [Live Editor for OBS Issues](https://github.com/TereBin/obs-live-editor/issues)를 이용해 주세요. 공개 이슈 작성이 어렵거나 개별 문의가 필요하면 [Discord에서 TereBin에게 문의](https://discordapp.com/users/537256771501424640)할 수 있습니다.

OBS에서 `도움말 > 로그 파일 > 현재 로그 보기`를 선택하고 문제 발생 직후의 로그에서 `obs-live-editor`, `TLS`, `qschannelbackend`가 포함된 줄과 도크의 오류 문구를 함께 제공하면 원인 확인이 빠릅니다.

어느 경로로 문의하더라도 Access Token, Refresh Token, Client Secret 또는 `credentials.bin` 파일은 절대 첨부하거나 전송하지 마세요.

## 보안과 소스 코드

로그인 토큰은 Windows DPAPI로 암호화되어 현재 Windows 사용자만 읽을 수 있는 로컬 파일에 저장됩니다. Client Secret과 실제 사용자 토큰은 이 저장소에 포함되지 않습니다.

소스 코드, 빌드 방법, Worker 구성은 [obs-live-editor 소스 저장소](https://github.com/TereBin/obs-live-editor)에서 확인할 수 있습니다. 이 프로그램은 GPL-2.0 라이선스로 배포됩니다.

## 후원

Live Editor for OBS가 도움이 되었다면 [Ko-fi에서 TereBin 후원하기](https://ko-fi.com/terebin)를
통해 개발을 응원할 수 있습니다.
