# 실행중인 Batch스크립트의 디렉토리 위치로 이동하기 `cd \d %~dp0`

## 관리자 권한으로 batch 스크립트를 실행시
cmd.exe의 설치 경로로부터 실행된다. (보통 `C:\WINDOWS\system32\`)  
따라서 스크립트 내에서 상대경로를 사용하고 싶은 경우에는 현재 batch 스크립트의 실행 경로를 가져와야 한다.

- ex. 다음 파일을 관리자 권한으로 실행시 

	C:\Users\foo\bar\test.bat

	```batch
	echo %0
	:: output: C:\WINDOWS\system32>echo C:\Users\foo\bar\test.bat
	```

## Batch parameters
MS에서는 `일괄 처리 매개 변수`라는 뭔가 무서워보이는 이름으로 번역해 두었다.. batch 스크립트를 실행하면서 전달한 인수를 스크립트 내에서 사용할 수 있도록 하는 특별한 변수를 말한다.   
예를 들어 `%1`은 첫번째 인수의 값을 가지고 있다. 

- ex. `foo@bar> .\some.bat some_arg`

	some.bat
	``` batch
	echo %1
	:: output: some_arg
	```

그리고 여기서 `%0`은 스크립트 자기 자신을 가리킨다. 따라서 다음과 같은 결과가 인출된다. 

- ex. `foo@bar> .\some2.bat some_arg`

	some2.bat
	``` batch
	echo %0
	echo %1
	:: output:
	:: C:\Users\foo\bar\some2.bat
	:: some_arg
	```
## Batch parameter의 값을 편집하기

위의 등장한 Batch parameter(일괄처리매개변수)에 대해서는 다음과 같은 구문을 사용해 편집된 값을 가져올 수 있다. 가장 간단한 예시로 다음의 구문을 보자.

- ex. `%~1`: `%1`을 확장하고 주변 따옴표를 제거합니다.

	`foo@bar> .\substitutions_1.bat "hello, substitutions!"` 
	```batch
	echo %~1
	:: output: hello, substitutions!
	```
- Batch parameter에서 사용 할 수 있는 구문들 [^1]

  | 일괄 매개 변수 | 	Description |
  | --- | --- |
  | %~1	| %1을(를) 확장하고 주변 따옴표를 제거합니다.|
  | % ~ f1 | 	확장 %1 정규화 된 경로에 있습니다. |
  | % ~ d 1 | 	확장 %1 드라이브 문자로 합니다. |
  | % ~ p1 | 	확장 %1 만 경로에 있습니다. |
  | % ~ n1 | 	확장 %1 만 파일 이름으로 저장 합니다. |
  | % ~ x1 | 	확장 %1 파일 이름 확장명으로 합니다. |
  | % ~ s1 | 	확장 %1 짧은 이름만 포함 하는 정규화 된 경로입니다. |
  | % ~ a1 | 	확장 %1 파일 특성에 있습니다. |
  | % ~ t1 | 	확장 %1 파일의 시간과 날짜를 합니다. |
  | % ~ z1 | 	확장 %1 파일의 크기입니다. |
  | % ~ $PATH: 1 | 	PATH 환경 변수에 나열 된 디렉터리를 검색 하 고 확장 %1 찾을 첫 번째 디렉터리의 정규화 된 이름에 있습니다. 환경 변수 이름이 정의 되지 않은 경우 파일은 검색에서 찾을 수 없습니다이 한정자는 빈 문자열로 확장 됩니다 |

## `cd \d %~dp0` 해석하기

지금까지의 정보를 바탕으로 `cd \d %~dp0`가 어떤 내용인지 해석하면 다음과 같다. 

- `cd`: 디렉토리를 이동함
- `\d`: 디렉토리를 변경하면서 드라이브도 함께 변경함 (cd 명령의 옵션)
- `%~dp0`: 실행중인 스크립트의 현재 드라이브+경로를  표시함

그래서 다음과 같은 batch 파일을 실행함으로써 스크립트의 위치로 이동이 가능하다.

- ex. 다음 파일을 관리자 권한으로 실행시 

	C:\Users\foo\bar\test2.bat

	```batch
	echo %cd%
	:: output: C:\WINDOWS\system32
	
	cd /d %~dp0
	echo %cd%
	:: output: C:\Users\foo\bar
	```
[^1]: https://learn.microsoft.com/ko-kr/windows-server/administration/windows-commands/call
