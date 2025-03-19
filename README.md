# System-SW-Working

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

