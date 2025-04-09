# System-SW-Working - 명령어 (수정 날짜: 25.03.26)

---
## 목차
- [Shebang (쉘 인터프리터 지정)](#shebang-쉘-인터프리터-지정)
- [BASH SHELL PROGRAMMING](#bash-shell-programming)
  - [Input (입력)](#input-입력)
  - [Decision (조건문)](#decision-조건문)
  - [Repetition (반복문)](#repetition-반복문)
  - [Functions (함수)](#functions-함수)
  - [Traps (트랩)](#traps-트랩)
- [USER INPUT](#user-input)
- [SPECIAL SHELL VARIABLES (특수 쉘 변수)](#special-shell-variables-특수-쉘-변수)
- [EXAMPLES: COMMAND LINE ARGUMENTS](#examples-command-line-arguments)
- [IF STATEMENT (if 문)](#if-statement-if-문)
- [TEST COMMAND](#test-command)
- [RELATIONAL OPERATORS](#relational-operators)
- [EXAMPLE: USING THE `!` OPERATOR](#example-using-the--operator)
- [EXAMPLE: USING THE `&&` OPERATOR](#example-using-the--operator-1)
- [EXAMPLE: USING THE `||` OPERATOR](#example-using-the--operator-2)
- [FILE TESTING](#file-testing)
- [EXAMPLE: FILE TESTING](#example-file-testing)
- [EXAMPLE: IF… STATEMENT](#example-if–-statement)
- [EXAMPLE: IF..ELIF... STATEMENT](#example-ifelif-statement)
- [THE CASE STATEMENT](#the-case-statement)
- [EXAMPLE 1: THE CASE STATEMENT](#example-1-the-case-statement)
- [EXAMPLE 2: THE CASE STATEMENT](#example-2-the-case-statement)
- [BASH PROGRAMMING: SO FAR](#bash-programming-so-far)
- [BASH PROGRAMMING: STILL TO COME](#bash-programming-still-to-come)
- [THE WHILE LOOP](#the-while-loop)
- [EXAMPLE: USING THE WHILE LOOP](#example-using-the-while-loop)
- [THE UNTIL LOOP](#the-until-loop)
- [EXAMPLE: USING THE UNTIL LOOP](#example-using-the-until-loop)
- [THE FOR LOOP](#the-for-loop)
  - [EXAMPLE 1: THE FOR LOOP](#example-1-the-for-loop)
  - [EXAMPLE 2: USING THE FOR LOOP](#example-2-using-the-for-loop)
- [LOOPING OVER ARGUMENTS](#looping-over-arguments)
- [SELECT COMMAND](#select-command)
- [BREAK AND CONTINUE](#break-and-continue)
- [SHELL FUNCTIONS](#shell-functions)
  - [EXAMPLE: 간단한 함수](#예제-간단한-함수)
  - [EXAMPLE: 반복 함수](#예제-반복-함수)
  - [함수 인자](#함수-인자)
    - [EXAMPLE: 매개변수가 있는 함수](#예제-매개변수가-있는-함수)
    - [EXAMPLE: 여러 인자 처리](#예제-여러-인자-처리)
  - [지역 변수 (local)](#지역-변수-local)
---


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
#! /bin/bash
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
#!/bin/bash
if [ -w "$1" ]; then
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
if [[ "$reply" = "y" ]]; then
    echo "You entered $reply"
fi

# SINGLE SQUARE BRACKETS
read -p "Do you want to continue? " reply
if [ "$reply" = "y" ]; then
    echo "You entered $reply"
fi

# "TEST" COMMAND
read -p "Do you want to continue? " reply
if test "$reply" = "y"; then
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
# 변수 초기화 후 산술연산 (let 사용 시 공백 없이)
let Net=Income-Expense

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

case "$reply" in
    Y|YES)
        echo "Displaying all (really…) files"
        ls -a ;;
    N|NO)
        echo "Displaying all non-hidden files..."
        ls ;;
    Q)
        exit 0 ;;
    *)
        echo "Invalid choice!"
        exit 1 ;;
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

case "$age" in
    [1-9]|1[0-2])
        echo "Your rate is \$${ChildRate}.00" ;;
    1[3-9]|[2-5][0-9])
        echo "Your rate is \$${AdultRate}.00" ;;
    [6-9][0-9])
        echo "Your rate is \$${SeniorRate}.00" ;;
    *)
        echo "Invalid age input."
        exit 1 ;;
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
while [ "$COUNTER" -lt 10 ]; do
    echo "The counter is $COUNTER"
    let COUNTER=COUNTER+1
done
```
- `COUNTER` 값이 10 미만인 동안 증가하면서 출력.
- `let COUNTER=$COUNTER+1` 을 통해 카운터 증가.

---

### 예제 2: 사용자 입력을 통한 반복 제어
```sh
#!/bin/bash
Cont="Y"
while [ "$Cont" = "Y" ]; do
    ps -A
    read -p "Want to continue? (Y/N) " reply
    Cont=$(echo "$reply" | tr '[:lower:]' '[:upper:]')
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
PICSDIR="/home/carol/pics"
WEBDIR="/var/www/carol/webcam"

while true; do
    DATE=$(date +%Y%m%d)
    HOUR=$(date +%H)
    mkdir -p "$WEBDIR/$DATE"
    while [ "$HOUR" -ne "00" ]; do
        DESTDIR="$WEBDIR/$DATE/$HOUR"
        mkdir -p "$DESTDIR"
        mv "$PICSDIR"/*.jpg "$DESTDIR"/
        sleep 3600
        HOUR=$(date +%H)
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
until [ "$COUNTER" -lt 10 ]; do
    echo "$COUNTER"
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
until [ "$Stop" = "Y" ]; do
    ps -A
    read -p "Want to stop? (Y/N) " reply
    Stop=$(echo "$reply" | tr '[:lower:]' '[:upper:]')
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
for i in 7 9 2 3 4 5; do
    echo "$i"
done

```
- `7 9 2 3 4 5` 값들을 `i`에 할당하며 반복 실행.
- 각 값이 차례로 출력됨.

---

## EXAMPLE 2: USING THE FOR LOOP

```sh
#!/bin/bash
TempTotal=0
for num in 1 2 3 4 5 6 7; do
    read -p "Enter temp for day $num: " Temp
    let TempTotal=TempTotal+Temp
done
let AvgTemp=TempTotal/7
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
for parm; do
    echo "$parm"
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
select var in alpha beta; do
    echo "$REPLY = $var"
done
```

---

### 실용 예제: 파일 보호 스크립트
```sh
#!/bin/bash
echo "Script to make files private"
echo "Select file to protect:"
select FILENAME in *; do
    echo "You picked $FILENAME ($REPLY)"
    chmod go-rwx "$FILENAME"
    echo "It is now private"
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
#!/bin/bash
for index in 1 2 3 4 5 6 7 8 9 10; do
    if [ "$index" -le 3 ]; then
        echo "continue"
        continue
    fi
    echo "$index"
    if [ "$index" -ge 8 ]; then
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
funky() {
    echo "This is a funky function."
    echo "Now exiting funky function."
}
funky
```

---

### 예제: 반복 함수
```sh
#!/bin/bash
fun() {
    local JUST_A_SECOND=1
    local i=0
    local REPEATS=30
    echo "And now the fun really begins."
    while [ "$i" -lt "$REPEATS" ]; do
        echo "-------FUNCTIONS are fun-------->"
        sleep "$JUST_A_SECOND"
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
#!/bin/bash
testfile() {
    if [ $# -gt 0 ]; then
        if [[ -f "$1" && -r "$1" ]]; then  # [[ ... ]]는 bash 전용 문법입니다.
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
    for file in "$@"; do
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
foo() {
    local inside="not so good variable"
    echo "$global"
    echo "$inside"
    global="better variable"
}
echo "$global"
foo
echo "$global"
echo "$inside"  # 출력되지 않음 (local 변수이므로 범위 밖)
```

---

# System-SW-Working - 가상화 (수정 날짜: 25.04.09)

이 문서는 가상화 기술의 기본 개념부터 구현 방식, 하이퍼바이저 분류, 오픈소스 프로젝트, 그리고 컨테이너 가상화까지 폭넓게 다룹니다.  

---

## 목차

- [1. 개요](#1-개요)
- [2. 링 보호 (Protection Ring)](#2-링-보호-protection-ring)
- [3. 가상 머신과 하이퍼바이저](#3-가상-머신과-하이퍼바이저)
- [4. 가상화 기법](#4-가상화-기법)
  - [4.1 전 가상화 (Full Virtualization)](#41-전-가상화-full-virtualization)
  - [4.2 반 가상화 (Para Virtualization)](#42-반-가상화-para-virtualization)
- [5. 하드웨어 가상화 지원 기능](#5-하드웨어-가상화-지원-기능)
- [6. 하이퍼바이저 종류](#6-하이퍼바이저-종류)
  - [6.1 Type 1 하이퍼바이저](#61-type-1-하이퍼바이저-bare-metal)
  - [6.2 Type 2 하이퍼바이저](#62-type-2-하이퍼바이저-hosted)
- [7. 오픈소스 가상화 프로젝트](#7-오픈소스-가상화-프로젝트)
- [8. Xen 가상화](#8-xen-가상화)
- [9. KVM 가상화](#9-kvm-가상화)
- [10. 컨테이너 가상화](#10-컨테이너-가상화)
- [11. Docker 설치 및 Node.js 사용법](#11-docker-설치-및-nodejs-사용법--상세-가이드-ubuntu-기준)
  - [11.1 Docker 설치 (Ubuntu 기준)](#111-docker-설치-ubuntu-기준)
  - [11.2 Node.js 설치 및 사용](#112-nodejs-설치-및-사용)
  - [11.3 Docker Compose 설치 및 사용법](#113-docker-compose-설치-및-사용법)
  - [11.4 Docker 이미지 및 관련 명령어](#114-docker-이미지-및-관련-명령어)

---

## 1. 개요

가상화(Virtualization)는 단일 물리적 하드웨어 자원을 여러 개의 논리적 가상 환경(가상 머신, 컨테이너 등)으로 분할하여 독립적으로 실행하는 기술입니다.  
이를 통해 자원 활용의 극대화, 비용 절감, 관리 효율성, 그리고 유연한 시스템 배포가 가능해집니다.  

---

## 2. 링 보호 (Protection Ring)

컴퓨터 시스템은 **링(보호 링)** 개념을 사용하여 자원 접근과 보안을 제어합니다.

- **링 0 (커널 모드 / 슈퍼 관리자 모드):**
  - 운영체제의 핵심 기능 및 하드웨어 직접 접근
  - 하이퍼바이저, VMM(가상 서버 모니터) 등이 실행됨

- **링 3 (사용자 모드 / 애플리케이션 실행 모드):**
  - 일반 애플리케이션이 실행되는 제한된 환경  
  - 커널 모드로 전환하기 위해 시스템 콜 사용

> *운영체제(리눅스/윈도우)는 링 0과 링 3 모두를 사용하며, 특별한 권한이 필요한 경우 시스템 콜을 통해 링 0의 기능을 호출합니다.*  

---

## 3. 가상 머신과 하이퍼바이저

가상화 환경에서는 **하이퍼바이저(가상서버 모니터)**가 물리 하드웨어 위에서 실행되며, 가상 머신(Guest VM)을 관리합니다.

- **하이퍼바이저:**
  - 링 0에서 실행되어 호스트의 메모리, CPU, I/O 포트에 접근
  - 가상 머신(Guest OS)이 실제 하드웨어와 간접적으로 상호작용하도록 지원

- **Guest VM:**
  - 일반적으로 하이퍼바이저보다 낮은 권한(예, 링 1 또는 사용자 모드 링 3)에서 실행
  - 하이퍼바이저가 제공하는 에뮬레이션 또는 하이퍼콜을 통해 필요한 자원에 접근

---

## 4. 가상화 기법

가상화를 구현하는 방식에는 크게 두 가지가 있습니다.

### 4.1 전 가상화 (Full Virtualization)

- **원리:**
  - Guest OS는 링 1에서 실행되며, 하이퍼바이저는 링 0에서 실행
  - OS의 권한 제약 문제를 해결하기 위해 **바이너리 변환(Binary Translation)** 기술 사용
  - 권한이 필요한 명령어는 VMM으로 전달되어 에뮬레이션 처리

- **특징:**
  - OS 수정 없이 기존 운영체제를 그대로 사용할 수 있음
  - 바이너리 변환으로 인한 성능 저하 가능성 존재

### 4.2 반 가상화 (Para Virtualization)

- **원리:**
  - Guest OS가 가상화 환경을 인지하도록 수정됨
  - **하이퍼콜(Hypercall)**을 통해 하이퍼바이저(VMM)와 직접 통신
  - 필요한 권한 요청이 API를 통해 전달되어 링 0에서 실행

- **특징:**
  - 전 가상화보다 성능이 향상됨
  - Guest OS 커널의 수정이 필요함


---

## 5. 하드웨어 가상화 지원 기능

현대의 x86 아키텍처에서는 가상화를 원활하게 지원하기 위해 하드웨어 가상화 확장 기능이 포함되어 있습니다.

- **지원 기술:**
  - **Intel:** VT-x, VT (Virtualization Technology)
  - **AMD:** AMD-V, SVM (Secure Virtual Machine)
  - **Itanium:** VT-i

- **효과:**
  - 하이퍼바이저 및 VMM이 Guest OS를 링 0에 가깝게 실행할 수 있도록 지원
  - 전 가상화 기술보다 성능이 크게 향상됨
  - KVM과 같은 최신 하이퍼바이저는 이러한 하드웨어 지원 기능을 적극 활용


---

## 6. 하이퍼바이저 종류

하이퍼바이저는 설치 위치와 방식에 따라 두 가지 유형으로 분류됩니다.

### 6.1 Type 1 하이퍼바이저 (Bare-metal)

- **특징:**
  - 물리적 하드웨어 위에 직접 설치되어 실행
  - 운영체제가 필요 없으므로 높은 성능, 보안성, 안정성을 제공

- **주요 제품 및 사례:**
  - VMware ESXi
  - Microsoft Hyper-V
  - Citrix XenServer
  - KVM (Kernel-based Virtual Machine)
  - Xen (초기 형태는 리눅스에 기본 장착되고 Citrix에서 관리)

### 6.2 Type 2 하이퍼바이저 (Hosted)

- **특징:**
  - 기존 호스트 운영체제 위에서 실행
  - 설치와 설정이 용이하며 개발/테스트 환경에 적합

- **주요 제품 및 사례:**
  - Oracle VirtualBox
  - VMware Workstation/Fusion
  - Parallels Desktop (Mac 전용)
  - QEMU


---

## 7. 오픈소스 가상화 프로젝트

다음은 대표적인 오픈소스 가상화 프로젝트입니다.

| 프로젝트         | 가상화 종류             | URL                                 |
|------------------|-------------------------|-------------------------------------|
| **KVM**        | 전 가상화               | [linux-kvm.org](http://www.linux-kvm.org/) |
| **VirtualBox** | 전 가상화               | [virtualbox.org](https://www.virtualbox.org/) |
| **Xen**        | 전 가상화, 반 가상화     | [xenproject.org](http://www.xenproject.org/) |
| **Lguest**     | 반 가상화               | [lguest.ozlabs.org](http://lguest.ozlabs.org/) |
| **UML**        | 전 가상화 (유저모드 리눅스) | [sourceforge.net](http://user-mode-linux.sourceforge.net/) |
| **Linux-VServer** | 컨테이너 가상화       | [linux-vserver.org](http://www.linux-vserver.org/) |


---

## 8. Xen 가상화

Xen은 가상화 기술의 초기 모델 중 하나로, 다양한 가상화 모드를 지원합니다.

- **역사:**
  - 케임브리지 대학 연구 프로젝트로 시작하여 2003년에 공개
  - 2013년 4월 Linux Foundation 공동 프로젝트로 이전

- **특징:**
  - 전 가상화, 반 가상화, 하드웨어 지원 모드 모두 사용 가능
  - **도메인 분류:**
    - **Dom0:** 특권 도메인 – 가상 머신 생성, 삭제, 관리 및 설정 담당  
      *(시스템에서 최초로 시작되며 하이퍼바이저 관리 역할)*
    - **DomU:** 일반 도메인 – 일반 Guest OS가 실행되는 환경


---

## 9. KVM 가상화

KVM(Kernel-based Virtual Machine)은 리눅스 커널에 하이퍼바이저 기능을 추가하여 하드웨어 가상화 확장 기능(VT-x, AMD-V)을 활용하는 최신 솔루션입니다.

- **구성:**
  - 리눅스 표준 커널에 KVM 커널 모듈 추가 → 하이퍼바이저로 변환
  - **QEMU:** I/O 에뮬레이션을 담당하는 사용자 영역 프로그램  
    - 디스크, 네트워크, VGA, PCI, USB 등 다양한 하드웨어 에뮬레이션 지원
  - 가상 머신 자원은 `/etc/libvirtd/qemu` 디렉토리에 XML 파일로 정의

- **운영:**
  - 각 가상 머신은 별도의 `qemu-kvm` 프로세스로 실행
  - 예시: `-m 5000` (메모리 5G 할당), `--smp=4,cores=1` (4개의 소켓에 하나의 코어 할당)


---

## 10. 컨테이너 가상화

컨테이너 가상화는 물리적 서버 상에서 하나의 운영체제 내에 다수의 격리된 환경(컨테이너)을 실행하는 기술입니다.

- **원리:**
  - **네임스페이스 (Namespaces):** 프로세스, 네트워크, 파일 시스템 등의 자원 격리
  - **cgroups (Control Groups):** CPU, 메모리 등 자원 사용량 제한 및 관리
  - **컨테이너 이미지:** 애플리케이션 실행에 필요한 파일, 라이브러리, 설정 등을 패키징
  - **컨테이너 런타임:** Docker, containerd 등 컨테이너를 실행 및 관리

- **특징:**
  - 가볍고 이식성이 높으며 빠른 시작 시간
  - 단일 OS 내에서 실행되므로 여러 운영체제를 동시에 지원하지는 않음


---

## 부록: 가상화 구조 다이어그램 (예시)

아래는 가상화 계층의 기본 구조를 간략하게 나타낸 다이어그램입니다.

```
[물리적 하드웨어]
        │
        ▼
[하이퍼바이저 / 컨테이너 런타임]
   ┌─────────────┬─────────────┐
   │             │             │
   ▼             ▼             ▼
[가상 머신]  [가상 머신]  [컨테이너]
   │             │
   ▼             ▼
[각기 다른 OS] [각기 다른 OS]
```


---

# 11. Docker 설치 및 Node.js 사용법 – 상세 가이드 (Ubuntu 기준)

> 이 가이드는 Ubuntu에서 Docker를 설치하고, Node.js를 nvm으로 설치 및 활용하는 방법과 Docker Compose, Dockerfile을 통해 Node.js 애플리케이션을 컨테이너화하는 전 과정을 포함합니다.

---

## 11.1 Docker 설치 (Ubuntu 기준)

### 1) 기존 Docker 패키지 제거 (선택 사항)
이 단계는 이전에 설치된 Docker 패키지나 관련 도구들이 있다면 제거하는 과정입니다. 이미 설치되어 있지 않다면 생략해도 괜찮습니다.

```bash
#!/bin/bash
set -e  # 에러 발생 시 스크립트를 종료

echo "기존 Docker 관련 패키지가 있는지 확인 후 제거합니다."
sudo apt-get remove -y docker docker-engine docker.io containerd runc || true
```

### 2) 시스템 업데이트 및 필수 패키지 설치
Docker 설치 전에 시스템 업데이트와 필요한 도구들을 설치합니다.

```bash
#!/bin/bash
set -e

echo "시스템 업데이트 및 필수 패키지 설치 중..."
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg lsb-release
```

### 3) Docker 공식 GPG 키 추가 및 저장소 설정
Docker 패키지를 신뢰할 수 있도록 GPG 키를 추가하고, Docker 저장소를 등록합니다.

```bash
#!/bin/bash
set -e

echo "Docker 공식 GPG 키 추가 및 저장소 설정 중..."
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# 현재 Ubuntu 릴리즈 이름(like focal, jammy 등)을 자동으로 적용하도록 함
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null <<EOF
deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable
EOF
```

### 4) Docker Engine 설치
이제 Docker Engine, CLI, containerd를 설치합니다.

```bash
#!/bin/bash
set -e

echo "Docker Engine 설치 중..."
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io

# 설치 확인
echo "Docker 버전 확인:"
docker --version
```

### 5) 현재 사용자 docker 그룹 추가 (sudo 없이 사용)
Docker 명령어를 sudo 없이 사용하려면 현재 사용자를 docker 그룹에 추가해야 합니다.

```bash
#!/bin/bash
set -e

echo "현재 사용자를 docker 그룹에 추가합니다..."
sudo usermod -aG docker $USER

echo "변경 사항 적용을 위해 반드시 로그아웃 후 재로그인 하거나 터미널을 재시작하세요."
```

### 6) 설치 테스트: hello-world 컨테이너 실행
설치가 잘 되었는지 테스트하기 위해 Docker의 기본 테스트 컨테이너를 실행합니다.

```bash
#!/bin/bash
set -e

echo "Docker 설치 테스트: hello-world 실행..."
docker run hello-world
```

---

## 11.2 Node.js 설치 및 사용

### [A] Node.js 로컬 설치 (nvm 권장)
nvm(Node Version Manager)을 사용하면 여러 버전의 Node.js를 쉽게 설치하고 전환할 수 있습니다.

#### 1) NVM 설치
nvm 설치 스크립트를 실행하고, 쉘 초기화 파일(~/.bashrc 또는 ~/.profile 등)을 다시 로드합니다.

```bash
#!/bin/bash
set -e

echo "nvm 설치 중..."
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

# nvm 설치 후 현재 쉘에 nvm 적용 (bash의 경우)
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"

echo "nvm 설치 완료. 쉘 재시작 또는 source ~/.bashrc 를 실행하세요."
```

#### 2) Node.js 최신 LTS 버전 설치 및 활성화

```bash
#!/bin/bash
set -e

echo "최신 LTS Node.js 버전 설치 중..."
nvm install --lts
nvm use --lts

echo "Node.js 버전:" 
node --version
echo "npm 버전:" 
npm --version
```

### [B] Node.js 애플리케이션 Docker 컨테이너화

#### 1) 프로젝트 초기화 및 간단한 애플리케이션 작성
프로젝트 디렉토리를 만들고, Node.js 애플리케이션을 초기화한 후 app.js 파일을 생성합니다.

```bash
#!/bin/bash
set -e

echo "Node.js 프로젝트 폴더 생성 및 초기화 중..."
mkdir -p my-node-app && cd my-node-app
npm init -y

# app.js 작성 (에디터를 사용해 아래 내용을 입력)
cat <<'EOF' > app.js
const http = require('http');
const port = 3000;
const server = http.createServer((req, res) => {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello, Node.js in Docker!\n');
});
server.listen(port, () => {
  console.log(`Server running at http://localhost:${port}/`);
});
EOF

echo "프로젝트 초기화 완료. app.js 파일이 생성되었습니다."
```

#### 2) Dockerfile 작성 – Node.js 애플리케이션 빌드를 위한 예제
아래 예제는 단순한 Node.js 애플리케이션을 컨테이너화하는 Dockerfile입니다. 추가 설명을 포함하여 다단계 빌드를 적용할 수도 있습니다.

```dockerfile
# Dockerfile

# 1단계: Node.js 의존성 설치 및 빌드 단계
FROM node:18-alpine AS build

# 작업 디렉터리 설정
WORKDIR /app

# package.json과 package-lock.json 복사 후 의존성 설치 (캐시 활용)
COPY package*.json ./
RUN npm install --production

# 나머지 소스 코드 복사
COPY . .

# (선택 사항) 빌드 스크립트 실행 – 만약 React나 Vue 등 빌드가 필요한 앱이라면 사용
# RUN npm run build

# 2단계: 실제 실행 단계 – 간단히 Node.js 애플리케이션 실행
FROM node:18-alpine

WORKDIR /app

# build 단계에서 설치된 모듈과 소스 복사
COPY --from=build /app /app

# 환경 변수 설정 (필요에 따라 수정)
ENV PORT=3000

# 포트 노출
EXPOSE 3000

# 컨테이너 시작 시 실행할 명령어
CMD ["node", "app.js"]
```

#### 3) Docker 이미지 빌드 및 컨테이너 실행

```bash
#!/bin/bash
set -e

echo "Docker 이미지 빌드 중..."
docker build -t my-node-app:1.0 .

echo "컨테이너 실행 중 (호스트의 3000 포트를 컨테이너의 3000 포트에 매핑)..."
docker run -d -p 3000:3000 --name my-node-app-container my-node-app:1.0

echo "컨테이너 실행 후 http://localhost:3000 에 접속해 확인하세요."
```

---

## 11.3 Docker Compose 설치 및 사용법

Docker Compose를 사용하면 다중 컨테이너 애플리케이션을 쉽게 정의하고 실행할 수 있습니다.

### 1) Docker Compose 설치

```bash
#!/bin/bash
set -e

echo "Docker Compose 설치 중..."
sudo curl -L "https://github.com/docker/compose/releases/download/v2.20.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

echo "설치 확인:"
docker-compose --version
```

### 2) docker-compose.yml 파일 예제 (Node.js + MongoDB)
아래 예제는 Node.js 웹 애플리케이션과 MongoDB 데이터베이스를 함께 사용하는 구성입니다.

```yaml
# docker-compose.yml
version: '3.8'  # 최신 스펙 사용 가능

services:
  web:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DB_HOST=db
    depends_on:
      - db
    volumes:
      - ./:/app  # 소스 코드 변경 즉시 반영 (개발환경에서 유용)
  
  db:
    image: mongo:5.0
    restart: always
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=secret
    volumes:
      - db-data:/data/db

volumes:
  db-data:
```

### 3) Docker Compose 명령어 사용 예

```bash
#!/bin/bash
set -e

# Compose를 이용해 백그라운드에서 컨테이너 실행
echo "docker-compose up -d 실행 중..."
docker-compose up -d

# 실행된 서비스 확인
docker-compose ps

# 로그 실시간 모니터링 (원하는 서비스 이름 지정 가능)
echo "docker-compose logs -f 실행 중..."
docker-compose logs -f

# 특정 컨테이너 내부 진입 (예, web 서비스)
# docker-compose exec web sh

# 서비스 중지 및 컨테이너 제거 (볼륨 삭제 포함)
# docker-compose down -v
```

---

## 요약

- **Docker 설치:** Ubuntu에서 Docker를 설치하고, GPG 키 추가 및 저장소 설정, 그룹 추가 등을 통해 sudo 없이도 사용 가능하게 구성합니다.
- **Node.js 설치:** nvm을 통해 최신 LTS 버전의 Node.js를 설치하며, 로컬 프로젝트와 함께 컨테이너화하는 과정을 포함합니다.
- **Dockerfile 작성:** 다단계 빌드 방식을 적용해, 의존성 설치와 실행 단계를 분리하여 효율적인 이미지를 빌드합니다.
- **Docker Compose:** 다중 컨테이너 애플리케이션(예: Node.js 웹 앱 + MongoDB)을 관리할 수 있는 docker-compose.yml 파일 예제와 주요 명령어를 소개합니다.

이와 같이 구성된 가이드를 통해 Docker 및 Node.js 기반 애플리케이션 구축에 대해 보다 자세히 학습하고, 실제 환경에서도 적용할 수 있을 것입니다. 추가적인 설명이나 특정 환경에 맞는 조정 사항은 실제 사용 시 환경에 맞게 수정하시기 바랍니다.

---
