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
if command
then
    statements
fi

## 설명
- `command` 가 성공(리턴 상태 `0`)하면 `then` 블록 내의 `statements` 가 실행됨.
- `command` 가 실패(리턴 상태 `0`이 아님)하면 `then` 블록을 건너뜀.

## 동작 방식
1. `command` 실행 후 종료 상태 확인
2. 종료 상태가 `0`이면 `then` 블록 실행
3. 종료 상태가 `0`이 아니면 `then` 블록 건너뜀





