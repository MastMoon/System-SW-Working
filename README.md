# System-SW-Working

# Shebang (쉘 인터프리터 지정)

#! /bin/bash    
- Bash 쉘 사용

#! /bin/sh      
- 기본 Bourne Shell 사용 (보통 /bin/bash와 동일)

# Bash 스크립트에서 사용
#! /bin/bash

echo "Hello, World!"

# 실행 방법
chmod +x script.sh  
- 실행 권한 부여

./script.sh         
- 실행

#! /bin/bash'를 사용하면 자동으로 Bash 환경에서 실행됨


# BASH SHELL PROGRAMMING

## Input (입력)
- 사용자가 입력한 값을 받을 수 있으며, `read` 명령어를 사용해 입력을 변수에 저장할 수 있다.
- 명령줄 인수(Command Line Arguments)를 통해 스크립트 실행 시 값을 전달할 수도 있다.

## Decision (조건문)
- `if-then-else` 문을 사용해 조건을 평가하고 특정 동작을 수행할 수 있다.
- `case` 문을 사용하면 여러 가지 옵션을 처리하는 것이 더 간결해진다.

## Repetition (반복문)
- `while` 문은 조건이 참일 동안 반복 실행된다.
- `for` 문을 사용하면 지정된 범위 내에서 반복할 수 있다.
- `until` 문은 조건이 거짓일 때 반복 실행된다.
- `select` 문을 사용하면 사용자가 여러 옵션 중 하나를 선택하도록 할 수 있다.

## Functions (함수)
- 함수를 정의하면 같은 코드를 여러 번 사용해야 할 때 효율적으로 재사용할 수 있다.
- 함수는 특정 작업을 수행하는 코드 블록이며, 호출 시 필요한 값을 전달할 수도 있다.

## Traps (트랩)
- `trap` 명령어를 사용하면 특정 신호(예: Ctrl+C)가 입력될 때 원하는 동작을 지정할 수 있다.
- 이를 통해 스크립트가 강제 종료되는 것을 방지하거나, 종료 전에 특정 작업을 수행할 수 있다.


# USER INPUT

## Shell은 사용자 입력을 받을 수 있도록 `read` 명령어를 제공한다.

### Syntax:
- `read varname [more vars]`
- `read -p "prompt" varname [more vars]`
  - `-p` 옵션을 사용하면 입력을 요청하는 메시지를 표시할 수 있다.
  - 사용자가 입력한 단어들이 변수(`varname` 및 `more vars`)에 할당된다.
  - 마지막 변수는 남은 모든 입력을 받는다.

## USER INPUT EXAMPLE

### 예제 스크립트
- 쉘 스크립트에서 사용자에게 이름을 입력받아 출력하는 예제

### 코드:
```sh
#! /bin/sh
read -p "enter your name: " first last
echo "First name: $first"
echo "Last name: $last"
```

# SPECIAL SHELL VARIABLES (특수 쉘 변수)

| 변수      | 의미 |
|-----------|------------------------------------------------|
| `$0`      | 현재 실행 중인 쉘 스크립트의 이름 |
| `$1-$9`   | 첫 번째부터 아홉 번째까지의 위치 매개변수 |
| `$#`      | 전달된 위치 매개변수의 개수 |
| `$*`      | 모든 위치 매개변수 (하나의 문자열로 처리) |
| `$@`      | 모든 위치 매개변수 (각각 별개의 문자열로 처리) |
| `$?`      | 가장 최근 실행한 명령어의 종료 상태 (0: 성공, 1 이상: 오류) |
| `$$`      | 현재 실행 중인 프로세스의 ID (PID) |


# EXAMPLES: COMMAND LINE ARGUMENTS

1. `% set tim bill ann fred`
   - `set` 명령어를 사용하여 위치 매개변수 할당
   - `$1 = tim`, `$2 = bill`, `$3 = ann`, `$4 = fred`

2. `% echo $*`
   - 모든 위치 매개변수를 하나의 문자열로 출력
   - 출력: `tim bill ann fred`

3. `% echo $#`
   - 위치 매개변수의 개수 출력
   - 출력: `4`

4. `% echo $1`
   - 첫 번째 위치 매개변수 출력
   - 출력: `tim`

5. `% echo $3 $4`
   - 세 번째와 네 번째 위치 매개변수 출력
   - 출력: `ann fred`

📌 **설명**  
- `set` 명령어를 사용하면 위치 매개변수에 값을 할당할 수 있다.
- `$*` : 모든 인수를 하나의 문자열로 출력.
- `$#` : 인수 개수를 반환.
- `$1, $2, $3 ...` : 각각의 위치 매개변수를 참조.


# IF STATEMENT (if 문)

## 기본 구조
```sh
if command
then
    statements
fi
```

## 설명
- `command` 가 성공(리턴 상태 `0`)하면 `then` 블록 내의 `statements` 가 실행됨.  
- `command` 가 실패(리턴 상태 `0`이 아님)하면 `then` 블록을 건너뜀.  

## 동작 방식
1. `command` 실행 후 종료 상태 확인  
2. 종료 상태가 `0`이면 `then` 블록 실행  
3. 종료 상태가 `0`이 아니면 `then` 블록 건너뜀



# TEST COMMAND

### 설명
- `test` 명령어나 `[ expression ]`을 사용하여 조건을 평가하고, 참(true) 또는 거짓(false)을 반환한다.
- `[ expression ]` 형식은 `test expression`과 동일하게 동작하며, 조건을 판별하는 데 사용된다.

### Syntax:
```sh
test expression
[ expression ]
```
- `test` 또는 `[]`를 사용하여 특정 조건을 평가할 수 있다.
- 조건이 참이면 `0`(성공), 거짓이면 `1`(실패) 상태를 반환한다.

### Example:
```sh
if test -w "$1"
then
    echo "file $1 is write-able"
fi
```
- `$1` 파일이 쓰기 가능하면 `"file $1 is write-able"`을 출력한다.
- `-w` 옵션은 파일이 쓰기 가능한지 확인하는 조건이다.

---

## THE SIMPLE IF STATEMENT

### 설명
- `if` 문은 조건을 검사하고, 조건이 참(true)일 경우 특정 명령을 실행한다.
- 조건이 거짓(false)이면 `then` 블록 내의 명령어가 실행되지 않는다.

### 기본 구조
```sh
if [ condition ]; then
    statements
fi
```
- `[ condition ]`은 조건을 검사하며, 조건이 참이면 `then` 블록 내 명령어가 실행된다.
- `condition`은 파일 상태, 변수 값 비교, 문자열 비교 등에 사용할 수 있다.

### Example:
```sh
if [ -f "$1" ]; then
    echo "File $1 exists."
fi
```
- `$1` 파일이 존재하면 `"File $1 exists."` 출력한다.
- `-f` 옵션은 지정된 파일이 존재하는지 확인한다.

---

## THE IF-THEN-ELSE STATEMENT

### 설명
- `if` 문을 사용하여 조건이 참일 경우 `statements-1`을 실행하고, 조건이 거짓일 경우 `else` 블록의 `statements-2`를 실행한다.
- 즉, 특정 조건에 따라 두 개의 실행 경로 중 하나를 선택할 수 있다.

### 기본 구조
```sh
if [ condition ]; then
    statements-1
else
    statements-2
fi
```
- `[ condition ]`이 참이면 `statements-1`이 실행된다.
- `[ condition ]`이 거짓이면 `else` 블록의 `statements-2`가 실행된다.

### Example:
```sh
if [ -d "$1" ]; then
    echo "$1 is a directory."
else
    echo "$1 is not a directory."
fi
```
- `$1`이 디렉토리이면 `"$1 is a directory."` 출력.
- `$1`이 디렉토리가 아니면 `"$1 is not a directory."` 출력.
- `-d` 옵션은 지정된 파일이 디렉토리인지 확인한다.

---

## THE IF…STATEMENT

### 설명
- `elif`는 "else if"를 의미하며, `if` 문에서 추가적인 조건을 검사할 때 사용된다.
- `elif`는 단독으로 사용할 수 없으며 반드시 `if` 문과 함께 사용해야 한다.

### 기본 구조
```sh
if [ condition ]; then
    statements
elif [ condition ]; then
    statement
else
    statements
fi
```
- `[ condition ]`이 참이면 `then` 블록의 명령어가 실행된다.
- 첫 번째 조건이 거짓이고 `elif`의 조건이 참이면 해당 블록이 실행된다.
- 모든 조건이 거짓이면 `else` 블록의 명령어가 실행된다.

### Example:
```sh
if [ $1 -gt 10 ]; then
    echo "Number is greater than 10"
elif [ $1 -eq 10 ]; then
    echo "Number is exactly 10"
else
    echo "Number is less than 10"
fi
```
- `$1`이 10보다 크면 "Number is greater than 10" 출력.
- `$1`이 10과 같으면 "Number is exactly 10" 출력.
- `$1`이 10보다 작으면 "Number is less than 10" 출력.
- `-gt`(greater than), `-eq`(equal to), `-lt`(less than) 연산자를 사용하여 숫자 비교를 수행한다.

---

## RELATIONAL OPERATORS

### 설명
- 관계 연산자는 숫자 및 문자열을 비교하는 데 사용된다.
- `[[ ... ]]` 내에서 문자열 비교를 수행할 때는 `<`, `>` 기호를 사용해야 한다.

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

## COMPOUND LOGICAL EXPRESSIONS

### 설명
- `!`, `&&`, `||` 연산자를 사용하여 여러 조건을 결합할 수 있다.
- `[[ ... ]]` 구문을 사용하여 복합 조건을 평가해야 한다.

### 연산자 목록
| 연산자 | 의미 |
|--------|------|
| `!` | NOT (부정) |
| `&&` | AND (논리곱) |
| '| |' | OR (논리합) |

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
- 입력한 근무 연수가 20년 미만이면 "You need 20+ years to retire" 출력.
- `!` 연산자를 사용하여 `"$Years" -lt 20` 조건을 부정.

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
- `&&` 연산자를 사용하여 두 조건이 모두 참일 경우 실행.
- `Status`가 `H`(Hourly)이고 `Shift`가 3이면 보너스를 지급.












