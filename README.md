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


# SPECIAL SHELL VARIABLES

| Parameter | Meaning |
|-----------|------------------------------------------------|
| `$0`      | Name of the current shell script              |
| `$1-$9`   | Positional parameters 1 through 9            |
| `$#`      | The number of positional parameters          |
| `$*`      | All positional parameters (as a single string) |
| `$@`      | All positional parameters (as separate strings) |
| `$?`      | Return status of the most recently executed command |
| `$$`      | Process ID of the current process            |


