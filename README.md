# System-SW-Working(수정 날짜: 25.03.26)

## Shebang (쉘 인터프리터 지정)

### Bash 쉘 사용
```sh
#! /bin/bash
```

### 기본 Bourne Shell 사용 (보통 /bin/bash와 동일)
```sh
#! /bin/sh
```

## Bash 스크립트 실행 예제
```sh
#! /bin/bash
echo "Hello, World!"
```

### 실행 방법
```sh
chmod +x script.sh  # 실행 권한 부여
./script.sh         # 실행
```
- `#! /bin/bash`를 사용하면 자동으로 Bash 환경에서 실행됨.

---

# BASH SHELL PROGRAMMING

## Input (입력)
- `read` 명령어를 사용하여 사용자 입력을 받을 수 있음.
- 명령줄 인수(Command Line Arguments)를 통해 실행 시 값을 전달할 수도 있음.

## Decision (조건문)
- `if-then-else` 문을 사용하여 조건을 평가하고 특정 동작을 수행.
- `case` 문을 사용하면 여러 가지 옵션을 간결하게 처리 가능.

## Repetition (반복문)
- `while`, `for`, `until`, `select` 문을 사용하여 반복 실행 가능.

## Functions (함수)
- 특정 작업을 수행하는 코드 블록으로, 호출 시 필요한 값을 전달할 수도 있음.

## Traps (트랩)
- `trap` 명령어를 사용하여 특정 신호(Ctrl+C 등) 입력 시 원하는 동작을 지정할 수 있음.

---

# USER INPUT

## Syntax:
```sh
read varname [more vars]
read -p "prompt" varname [more vars]
```
- `-p` 옵션을 사용하면 입력 요청 메시지를 표시할 수 있음.

### USER INPUT EXAMPLE
```sh
#! /bin/sh
read -p "enter your name: " first last
echo "First name: $first"
echo "Last name: $last"
```

---

# SPECIAL SHELL VARIABLES (특수 쉘 변수)

| 변수 | 의미 |
|-----------|--------------------------------|
| `$0` | 현재 실행 중인 쉘 스크립트의 이름 |
| `$1-$9` | 첫 번째부터 아홉 번째까지의 위치 매개변수 |
| `$#` | 전달된 위치 매개변수의 개수 |
| `$*` | 모든 위치 매개변수 (하나의 문자열로 처리) |
| `$@` | 모든 위치 매개변수 (각각 별개의 문자열로 처리) |
| `$?` | 가장 최근 실행한 명령어의 종료 상태 (0: 성공, 1 이상: 오류) |
| `$$` | 현재 실행 중인 프로세스의 ID (PID) |

---

# EXAMPLES: COMMAND LINE ARGUMENTS

```sh
% set tim bill ann fred  # 위치 매개변수 할당
% echo $*  # 모든 위치 매개변수 출력
tim bill ann fred
% echo $#  # 위치 매개변수 개수 출력
4
% echo $1  # 첫 번째 위치 매개변수 출력
tim
% echo $3 $4  # 세 번째와 네 번째 위치 매개변수 출력
ann fred
```

---

# IF STATEMENT (if 문)

## 기본 구조
```sh
if command
then
    statements
fi
```
- `command`가 성공(리턴 상태 `0`)하면 `then` 블록 실행.
- 실패(리턴 상태 `0`이 아님)하면 블록을 건너뜀.

---

# TEST COMMAND

### 설명
- `test` 명령어나 `[ expression ]`을 사용하여 조건을 평가하고, 참(true) 또는 거짓(false)을 반환한다.
- `[ expression ]` 형식은 `test expression`과 동일하게 동작하며, 조건을 판별하는 데 사용된다.
- 조건이 참이면 `0`(성공), 거짓이면 `1`(실패) 상태를 반환한다.

### Syntax:
```sh
test expression
[ expression ]
```
- `test` 또는 `[]`을 사용하여 특정 조건을 평가할 수 있다.

### Example:
```sh
if test -w "$1"
then
    echo "file $1 is write-able"
else
    echo "file $1 is not write-able or does not exist"
fi
```
- `$1` 파일이 쓰기 가능하면 `"file $1 is write-able"`을 출력한다.
- 파일이 없거나 쓰기 불가능하면 `"file $1 is not write-able or does not exist"`를 출력한다.

### 실행 방법
1. 스크립트 파일 생성
   ```sh
   nano test_script.sh
   ```
2. 위 코드 입력 후 저장 (Ctrl + X → Y → Enter)
3. 실행 권한 부여
   ```sh
   chmod +x test_script.sh
   ```
4. 실행
   ```sh
   ./test_script.sh filename.txt
   ```
   (여기서 `filename.txt`는 확인할 파일 이름)

### 결과 예시
- `filename.txt` 파일이 쓰기 가능하면:
  ```sh
  file filename.txt is write-able
  ```
- 파일이 없거나 쓰기 불가능하면:
  ```sh
  file filename.txt is not write-able or does not exist
  ```


---

## RELATIONAL OPERATORS

### 연산자 목록
| 의미 | 숫자 비교 | 문자열 비교 |
|------|---------|------------|
| 크다 | `-gt` | `str1 > str2` |
| 크거나 같다 | `-ge` | 없음 |
| 작다 | `-lt` | `str1 < str2` |
| 작거나 같다 | `-le` | 없음 |
| 같다 | `-eq` | `=` 또는 `==` |
| 다르다 | `-ne` | `!=` |
| 문자열 길이가 0보다 큼 | 없음 | `-n str` |
| 문자열 길이가 0임 | 없음 | `-z str` |

---

## EXAMPLE: USING THE `!` OPERATOR

```sh
#!/bin/bash
read -p "Enter years of work: " Years
if [ ! "$Years" -lt 20 ]; then
    echo "You can retire now."
else
    echo "You need 20+ years to retire"
fi
```
- `!` (논리 부정 연산자)를 사용하여 조건을 반대로 평가.
- `Years` 값이 20 미만이면 `"You need 20+ years to retire"` 출력.
- 20 이상이면 `"You can retire now."` 출력.

---

## EXAMPLE: USING THE `&&` OPERATOR

```sh
#!/bin/bash
Bonus=500
read -p "Enter Status: " Status
read -p "Enter Shift: " Shift
if [[ "$Status" = "H" && "$Shift" = 3 ]]
then
    echo "shift $Shift gets \$$Bonus bonus"
else
    echo "only hourly workers in"
    echo "shift 3 get a bonus"
fi
```
- `&&` (논리곱) 연산자를 사용하여 두 조건이 모두 참일 때 실행.
- `Status`가 `"H"`이고 `Shift`가 `3`이면 보너스를 지급.

---

## EXAMPLE: USING THE `||` OPERATOR

```sh
#!/bin/bash
read -p "Enter calls handled: " CHandle
read -p "Enter calls closed: " CClose
if [[ "$CHandle" -gt 150 || "$CClose" -gt 50 ]]
then
    echo "You are entitled to a bonus"
else
    echo "You get a bonus if the calls"
    echo "handled exceeds 150 or"
    echo "calls closed exceeds 50"
fi
```
- `||` (논리합) 연산자를 사용하여 두 조건 중 하나라도 참이면 실행.
- `CHandle`이 150보다 크거나 `CClose`가 50보다 크면 보너스를 지급.

---

## FILE TESTING

### 파일 상태를 확인하는 연산자 목록
| 연산자 | 의미 |
|--------|------------------------------|
| `-d file` | 파일이 디렉토리이면 참 |
| `-f file` | 파일이 일반 파일이면 참 |
| `-r file` | 파일이 읽기 가능하면 참 |
| `-w file` | 파일이 쓰기 가능하면 참 |
| `-x file` | 파일이 실행 가능하면 참 |
| `-s file` | 파일 크기가 0보다 크면 참 |

---

## EXAMPLE: FILE TESTING

```sh
#!/bin/bash
echo "Enter a filename: "
read filename
if [ ! -r "$filename" ]
then
    echo "File is not readable"
    exit 1
fi
```
- 입력한 파일이 읽기 불가능하면 `"File is not readable"` 출력 후 종료.

```sh
#!/bin/bash
if [ $# -lt 1 ]; then
    echo "Usage: filetest filename"
    exit 1
fi
if [[ ! -f "$1" || ! -r "$1" || ! -w "$1" ]]
then
    echo "File $1 is not accessible"
    exit 1
fi
```
- 실행 시 인수를 제공하지 않으면 사용법을 출력하고 종료.
- 파일이 일반 파일이 아니거나 읽기/쓰기 불가능하면 `"File $1 is not accessible"` 출력 후 종료.

---

## EXAMPLE: IF… STATEMENT

### 세 가지 방법으로 동일한 결과를 얻을 수 있음
```sh
# DOUBLE SQUARE BRACKETS
read -p "Do you want to continue? " reply
if [[ $reply = "y" ]]; then
    echo "You entered $reply"
fi

# SINGLE SQUARE BRACKETS
read -p "Do you want to continue? " reply
if [ $reply = "y" ]; then
    echo "You entered $reply"
fi

# "TEST" COMMAND
read -p "Do you want to continue? " reply
if test $reply = "y"; then
    echo "You entered $reply"
fi
```
- `[[ ... ]]`, `[ ... ]`, `test` 명령어를 사용하여 같은 결과를 얻을 수 있음.
- 사용자가 `"y"`를 입력하면 `"You entered y"` 출력.

---

## EXAMPLE: IF..ELIF... STATEMENT

```sh
#!/bin/bash
read -p "Enter Income Amount: " Income
read -p "Enter Expenses Amount: " Expense
let Net=$Income-$Expense
if [ "$Net" -eq "0" ]; then
    echo "Income and Expenses are equal - breakeven."
elif [ "$Net" -gt "0" ]; then
    echo "Profit of: $Net"
else
    echo "Loss of: $Net"
fi
```
- `Income`과 `Expense`를 입력받아 순이익(`Net`)을 계산.
- `Net` 값에 따라 손익 상태를 출력.
- `"0"`이면 손익분기, 양수이면 이익, 음수이면 손실을 나타냄.

---

# THE CASE STATEMENT

### 설명
- `case` 문은 여러 선택지를 기반으로 결정을 내릴 때 사용된다.
- `if-elif-else` 문보다 간결하고 가독성이 좋다.

### Syntax:
```sh
case word in
    pattern1) command-list1 ;;
    pattern2) command-list2 ;;
    patternN) command-listN ;;
esac
```
- `word` 값이 패턴(`pattern1`, `pattern2` 등)과 일치하면 해당 명령 목록(`command-list`)을 실행한다.
- `esac` 키워드를 사용하여 `case` 문을 종료한다.

---

## CASE PATTERN
- `word`와 `pattern`을 비교하여 일치하는 패턴이 있는 경우 해당 명령을 실행한다.
- 패턴에는 다음과 같은 특수 문자를 사용할 수 있다:
  - `*` : 모든 문자열과 일치
  - `?` : 단일 문자와 일치
  - `[ … ]` : 대괄호 안의 문자 중 하나와 일치
  - `[:class:]` : 특정 문자 클래스와 일치 (예: `[:digit:]` → 숫자와 일치)
- 여러 개의 패턴을 `|` 기호를 사용하여 한 줄에 나열할 수 있다.

---

## EXAMPLE 1: THE CASE STATEMENT
```sh
#!/bin/bash
echo "Enter Y to see all files including hidden files"
echo "Enter N to see all non-hidden files"
echo "Enter Q to quit"
read -p "Enter your choice: " reply

case $reply in
    Y|YES) echo "Displaying all (really…) files"
           ls -a ;;
    N|NO)  echo "Displaying all non-hidden files..."
           ls ;;
    Q)     exit 0 ;;
    *)     echo "Invalid choice!"; exit 1 ;;
esac
```

### 동작 방식
1. 사용자에게 입력값을 받는다.
2. 입력값이 `Y` 또는 `YES`이면 숨김 파일을 포함한 모든 파일을 출력한다 (`ls -a`).
3. 입력값이 `N` 또는 `NO`이면 숨김 파일을 제외한 파일만 출력한다 (`ls`).
4. 입력값이 `Q`이면 스크립트가 종료된다.
5. 위의 조건과 일치하지 않으면 `"Invalid choice!"` 메시지를 출력하고 종료한다.

### 실행 방법
1. 스크립트 파일 생성
   ```sh
   nano case_script.sh
   ```
2. 위 코드 입력 후 저장 (Ctrl + X → Y → Enter)
3. 실행 권한 부여
   ```sh
   chmod +x case_script.sh
   ```
4. 실행
   ```sh
   ./case_script.sh
   ```

### 예제 실행 결과
#### 입력값이 `Y`
```sh
Displaying all (really…) files
.  ..  file1  .hiddenfile
```

#### 입력값이 `N`
```sh
Displaying all non-hidden files...
file1
```

#### 입력값이 `Q`
```sh
(스크립트 종료)
```

#### 잘못된 입력값 (`X` 등)
```sh
Invalid choice!
```

---

# EXAMPLE 2: THE CASE STATEMENT

### 설명
- `case` 문을 사용하여 입력된 연령대에 따라 요금을 결정하는 스크립트.
- 연령대를 구분하여 `ChildRate`, `AdultRate`, `SeniorRate`에 따라 요금을 출력.

```sh
#!/bin/bash
ChildRate=3
AdultRate=10
SeniorRate=7

read -p "Enter your age: " age

case $age in
    [1-9]|[1][0-2])   # 어린이 요금 (1~12세)
        echo "Your rate is $""$ChildRate.00" ;;
    [1][3-9]|[2-5][0-9]) # 성인 요금 (13~59세)
        echo "Your rate is $""$AdultRate.00" ;;
    [6-9][0-9])       # 노인 요금 (60세 이상)
        echo "Your rate is $""$SeniorRate.00" ;;
esac
```

### 동작 방식
1. 사용자가 나이를 입력.
2. `case` 문을 통해 나이 범위를 패턴과 비교:
   - `[1-9]|[1][0-2]` → 1~12세: 어린이 요금 적용 (`$ChildRate`)
   - `[1][3-9]|[2-5][0-9]` → 13~59세: 성인 요금 적용 (`$AdultRate`)
   - `[6-9][0-9]` → 60세 이상: 노인 요금 적용 (`$SeniorRate`)
3. 해당하는 요금을 출력.

### 실행 방법
1. 스크립트 파일 생성
   ```sh
   nano case_rate.sh
   ```
2. 위 코드 입력 후 저장 (Ctrl + X → Y → Enter)
3. 실행 권한 부여
   ```sh
   chmod +x case_rate.sh
   ```
4. 실행
   ```sh
   ./case_rate.sh
   ```

### 예제 실행 결과
#### 입력값: `10`
```sh
Your rate is $3.00
```
#### 입력값: `25`
```sh
Your rate is $10.00
```
#### 입력값: `65`
```sh
Your rate is $7.00
```

---

# BASH PROGRAMMING: SO FAR

### 데이터 구조
- 변수 (Variables)
- 숫자 변수 (Numeric variables)
- 배열 (Arrays)

### 사용자 입력
- `read` 명령어를 사용하여 사용자 입력을 받을 수 있음.

### 제어 구조 (Control structures)
- `if-then-else` 문
- `case` 문

---

# BASH PROGRAMMING: STILL TO COME

### 추가 학습할 제어 구조
- 반복문 (Repetition)
  - `do-while`
  - `repeat-until`
  - `for`
  - `select`

### 기타 학습 내용
- 함수 (Functions)
- 신호 트래핑 (Trapping signals)

---

# THE WHILE LOOP

### 목적
- `while` 루프는 `expression`이 참(`true`)인 동안 `command-list`를 반복 실행한다.

### Syntax:
```sh
while [ expression ]
do
    command-list
done
```
- `[ expression ]`이 참일 때 `command-list` 실행.
- 표현식이 거짓이 되면 루프 종료.

---

## EXAMPLE: USING THE WHILE LOOP

### 예제 1: 기본적인 카운터 증가
```sh
#!/bin/bash
COUNTER=0
while [ $COUNTER -lt 10 ]
do
    echo "The counter is $COUNTER"
    let COUNTER=$COUNTER+1
done
```
- `COUNTER` 값이 10 미만인 동안 증가하면서 출력.
- `let COUNTER=$COUNTER+1` 을 통해 카운터 증가.

---

### 예제 2: 사용자 입력을 통한 반복 제어
```sh
#!/bin/bash
Cont="Y"
while [ $Cont = "Y" ]; do
    ps -A
    read -p "Want to continue? (Y/N)" reply
    Cont=`echo $reply | tr [:lower:] [:upper:]`
done
echo "Done"
```
- 프로세스 목록(`ps -A`)을 출력한 후, 계속 실행할지 여부를 물어봄.
- 입력값을 대문자로 변환하여 비교 (`tr [:lower:] [:upper:]`).
- `Y`가 입력되면 계속 실행, 그렇지 않으면 종료.

---

### 예제 3: 특정 디렉토리에 파일을 시간별로 이동
```sh
#!/bin/bash
# 홈 디렉토리에서 웹 서버 디렉토리로 파일을 복사하는 스크립트
# 새로운 디렉토리를 매 시간 생성
PICSDIR=/home/carol/pics
WEBDIR=/var/www/carol/webcam
while true; do
    DATE=`date +%Y%m%d`
    HOUR=`date +%H`
    mkdir $WEBDIR/"$DATE"
    while [ $HOUR -ne "00" ]; do
        DESTDIR=$WEBDIR/"$DATE"/"$HOUR"
        mkdir "$DESTDIR"
        mv $PICSDIR/*.jpg "$DESTDIR"/
        sleep 3600
        HOUR=`date +%H`
    done
done
```
- `PICSDIR`에서 `WEBDIR`로 `.jpg` 파일을 이동하는 스크립트.
- 매시간 새로운 디렉토리를 생성하고 이미지를 이동시킴.
- `sleep 3600`을 사용하여 매시간 파일을 이동함.
- `while true`는 무한 루프를 수행함.

---

# THE UNTIL LOOP

### 설명
- `until` 루프는 `expression`이 거짓(`false`)인 동안 `command-list`를 실행한다.

### Syntax:
```sh
until [ expression ]
do
    command-list
done
```
- `[ expression ]`이 거짓일 때 `command-list` 실행.
- 표현식이 참이 되면 루프 종료.

---

## EXAMPLE: USING THE UNTIL LOOP

### 예제 1: 카운터 감소
```sh
#!/bin/bash
COUNTER=20
until [ $COUNTER -lt 10 ]
do
    echo $COUNTER
    let COUNTER-=1
done
```
- `COUNTER` 값이 10 미만이 될 때까지 감소하면서 출력.
- `let COUNTER-=1` 을 통해 카운터 감소.

---

### 예제 2: 사용자 입력을 통한 반복 제어
```sh
#!/bin/bash
Stop="N"
until [ $Stop = "Y" ]; do
    ps -A
    read -p "Want to stop? (Y/N)" reply
    Stop=`echo $reply | tr [:lower:] [:upper:]`
done
echo "Done"
```
- 프로세스 목록(`ps -A`)을 출력한 후, 실행을 중지할지 여부를 물어봄.
- 입력값을 대문자로 변환하여 비교 (`tr [:lower:] [:upper:]`).
- `Y`가 입력되면 루프 종료, 그렇지 않으면 계속 실행.

---

# THE FOR LOOP

### 설명
- `for` 루프는 `argument-list`에 포함된 각 요소에 대해 `command-list`를 실행한다.

### Syntax:
```sh
for variable in argument-list
do
    commands
done
```
- `argument-list`의 각 요소가 `variable`에 저장되며, 해당 값을 이용해 `commands` 실행.

---

## EXAMPLE 1: THE FOR LOOP

```sh
#!/bin/bash
for i in 7 9 2 3 4 5
do
    echo $i
done
```
- `7 9 2 3 4 5` 값들을 `i`에 할당하며 반복 실행.
- 각 값이 차례로 출력됨.

---

## EXAMPLE 2: USING THE FOR LOOP

```sh
#!/bin/bash
# Compute the average weekly temperature
for num in 1 2 3 4 5 6 7
do
    read -p "Enter temp for day $num: " Temp
    let TempTotal=$TempTotal+$Temp
done
let AvgTemp=$TempTotal/7
echo "Average temperature: $AvgTemp"
```
- 사용자에게 7일간의 온도를 입력받아 합산.
- 7로 나누어 평균 온도를 계산 후 출력.

---

# LOOPING OVER ARGUMENTS

### 설명
- 가장 간단한 형태의 `for` 루프는 커맨드 라인에서 전달된 모든 인수를 반복 실행한다.

```sh
#!/bin/bash
for parm
do
    echo $parm
done
```
- 실행 시 전달된 인수들을 하나씩 출력함.
- 예를 들어, `./script.sh arg1 arg2 arg3`를 실행하면 `arg1`, `arg2`, `arg3`가 차례로 출력됨.



---

# SELECT COMMAND

### 설명
- `select` 문은 간단한 메뉴를 만들기 위해 사용되며, 사용자로부터 번호 입력을 받는다.
- 각 번호는 리스트 내 단어의 인덱스(1부터 시작)를 나타낸다.
- 루프는 사용자가 `Ctrl+D` 또는 `Ctrl+C`를 누를 때까지 계속된다.

### Syntax
```sh
select WORD in LIST
do
    RESPECTIVE-COMMANDS
done
```

### 예제
```sh
#!/bin/bash
select var in alpha beta gamma
do
    echo $var
done
```
- 출력 예시:
```
1) alpha
2) beta
3) gamma
#? 2
beta
#? 1
alpha
```

---

### 상세 기능
- `PS3` 변수는 사용자에게 표시되는 프롬프트 메시지를 설정한다.
- `$REPLY`는 사용자가 입력한 번호를 저장한다.

```sh
#!/bin/bash
PS3="select entry or ^D: "
select var in alpha beta
do
    echo "$REPLY = $var"
done
```

---

### 실용 예제: 파일 보호 스크립트
```sh
#!/bin/bash
echo "script to make files private"
echo "Select file to protect:"
select FILENAME in *
do
    echo "You picked $FILENAME ($REPLY)"
    chmod go-rwx "$FILENAME"
    echo "it is now private"
done
```

---

# BREAK AND CONTINUE

### BREAK
- 루프를 즉시 종료하고 루프 다음 문장으로 이동한다.

```sh
while [ condition ]
do
    cmd-1
    break
    cmd-n
 done
echo "done"
```

### CONTINUE
- 현재 반복을 건너뛰고 다음 반복으로 이동한다.

```sh
while [ condition ]
do
    cmd-1
    continue
    cmd-n
done
echo "done"
```

---

### 예제: break & continue <mark> 중요! </mark>
```sh
for index in 1 2 3 4 5 6 7 8 9 10
do
    if [ $index -le 3 ]; then
        echo "continue"
        continue
    fi
    echo $index
    if [ $index -ge 8 ]; then
        echo "break"
        break
    fi
done
```

---

# SHELL FUNCTIONS

### 설명
- 함수는 나중에 실행하기 위해 명령어 시퀀스를 저장할 수 있는 블록이다.
- 함수는 호출한 동일한 셸 내에서 실행되며, `.profile`, 스크립트 또는 커맨드라인에서 정의 가능하다.
- 함수 제거는 `unset` 사용.

### Syntax
```sh
function_name () {
    statements
}
```

---

### 예제: 간단한 함수
```sh
#!/bin/bash
funky () {
    echo "This is a funky function."
    echo "Now exiting funky function."
}
funky
```

---

### 예제: 반복 함수
```sh
#!/bin/bash
fun () {
    JUST_A_SECOND=1
    let i=0
    REPEATS=30
    echo "And now the fun really begins."
    while [ $i -lt $REPEATS ]
    do
        echo "-------FUNCTIONS are fun-------->"
        sleep $JUST_A_SECOND
        let i+=1
    done
}
fun
```

---

### 함수 인자
- `$1`, `$2`, ..., `$#`로 접근 가능
- `$0`은 여전히 스크립트 이름

### 예제: 매개변수가 있는 함수
```sh
#!/bin/sh
#!/bin/bash # 이거를 적어야함.
testfile() {
    if [ $# -gt 0 ]; then
        if [[ -f $1 && -r $1 ]]; then //bash 지원
            echo "$1 is a readable file"
        else
            echo "$1 is not a readable file"
        fi
    fi
}
testfile .
testfile funtest
```

---

### 예제: 여러 인자 처리
```sh
#!/bin/bash
checkfile() {
    for file
do
    if [ -f "$file" ]; then
        echo "$file is a file"
    elif [ -d "$file" ]; then
        echo "$file is a directory"
    fi
done
}
checkfile . funtest
```

---

### 지역 변수 (local)
- 함수 내의 변수는 기본적으로 **전역**이다.
- `local` 키워드를 사용하면 함수 내부에 **지역 변수**를 만들 수 있다.

```sh
#!/bin/bash
global="pretty good variable"
foo () {
    local inside="not so good variable"
    echo $global
    echo $inside
    global="better variable"
}
echo $global
foo
echo $global
echo $inside  # 출력되지 않음
```

---
