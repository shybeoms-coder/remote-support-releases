# remote-support-releases

원격 지원 호스트 앱(**RemoteSupportHost**)의 설치파일 보관소입니다.
소스 코드는 들어있지 않고, 릴리스 자산(설치파일 + blockmap)만 보관합니다.

## 왜 여기에 두는가

호스트 앱의 자동업데이트 피드(`latest.yml`)는 시그널링 서버가 제공하지만,
설치파일 본체(약 86MB)를 서버 배포 이미지 안에 두면 서버를 재배포할 때마다
설치파일이 사라져 자동업데이트가 깨집니다. 그래서 피드는 서버에,
설치파일은 이 repo의 릴리스에 둡니다. electron-updater는 `latest.yml`의
`url`이 절대 URL이면 그 URL에서 바로 내려받습니다.

이 repo가 **공개(public)** 인 이유는 electron-updater가 토큰 없이 자산을
내려받기 때문입니다. 자산은 코드 서명된 설치파일뿐입니다.

## 자산 이름 규칙

```
RemoteSupportHost.Setup.<버전>.exe
RemoteSupportHost.Setup.<버전>.exe.blockmap
```

공백 대신 점을 씁니다. electron-updater가 blockmap 경로를 설치파일 URL에서
계산하기 때문에 이름이 어긋나면 차분(delta) 업데이트가 실패합니다.

## 주의

**기존 릴리스와 자산을 지우거나 이름을 바꾸지 마세요.** 이미 설치된 호스트가
이 URL을 직접 내려받습니다. 이전 버전 태그에 올려둔 blockmap도 차분 업데이트에
쓰이므로 그대로 두세요.

새 버전 릴리스 절차는 호스트 앱 저장소의 `remote-support/README.md`
"호스트 앱 릴리스 절차" 절을 참고하세요.
