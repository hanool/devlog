# PowerShell에서 Symbolic Link를 만드는 방법

윈도우에서는 주로 `바로가기(Shortcut)`을 이용해 왔었지만 리눅스(혹은 macos등 유닉스계열)을 사용하다보면 `symbolic link`를 자주 사용하게 된다. `바로가기`에 비해 훨씬 더 유용하고 편리하기 때문에 윈도우에서도 `symbolic link`를 만들 수 없는지 찾아보던 중 PowerShell을 이용하는 방법을 찾았다.

## Symbolic Link란?

간단히 말해 `바로가기`와 매우 비슷한 개념이다. 다른 파일이나 디렉터리에 대한 참조를 포함하고 있는 특별한 종류의 `파일`이 바로 `Symbolic Link`다. `바로가기`와의 가장 큰 차이점은 `바로가기`는 파일에 대한 참조만 가능한데 비해, `Symbolic Link`는 디렉터리에 대한 참조도 가능하다. 
또 `바로가기` (혹은 `Hard Link`)는 다른 볼륨이나 파일 시스템 상의 경로에는 접근 할 수 없지만, Symbolic Link는 이 또한 참조 할 수 있다.

## PowerShell에서 Symblic Link 작성

```powershell
	New-Item -ItemType SymbolicLink -Path ".\Some\Place" -Target "C:\Some\Target"
```
