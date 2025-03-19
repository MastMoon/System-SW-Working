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

## Input
# 사용자 입력 (Prompting User)
#!/bin/bash
echo "이름을 입력하세요:"
read name
echo "안녕하세요, $name!"

# 명령줄 인수 (Command Line Arguments)
#!/bin/bash
echo "첫 번째 인수: $1"
echo "두 번째 인수: $2"
echo "모든 인수: $@"
# 실행: ./script.sh Hello World

## Decision (조건문)
# if-then-else
#!/bin/bash
echo "숫자를 입력하세요:"
read num
if [ $num -gt 10 ]; then
    echo "입력한 숫자가 10보다 큽니다."
elif [ $num -eq 10 ]; then
    echo "입력한 숫자가 10과 같습니다."
else
    echo "입력한 숫자가 10보다 작습니다."
fi

# case 문
#!/bin/bash
echo "옵션을 선택하세요 (start/stop/restart):"
read option
case $option in
    start) echo "서비스 시작";;
    stop) echo "서비스 중지";;
    restart) echo "서비스 재시작";;
    *) echo "잘못된 입력";;
esac

## Repetition (반복문)
# while 문 (do-while)
#!/bin/bash
count=1
while [ $count -le 5 ]; do
    echo "반복 횟수: $count"
    ((count++))
done

# for 문
#!/bin/bash
for i in {1..5}; do
    echo "반복 횟수: $i"
done

# until 문 (repeat-until)
#!/bin/bash
count=1
until [ $count -gt 5 ]; do
    echo "반복 횟수: $count"
    ((count++))
done

# select 문 (메뉴 선택)
#!/bin/bash
echo "원하는 옵션을 선택하세요:"
select option in 시작 중지 종료; do
    case $option in
        시작) echo "서비스 시작"; break ;;
        중지) echo "서비스 중지"; break ;;
        종료) echo "스크립트 종료"; exit ;;
        *) echo "잘못된 선택입니다." ;;
    esac
done

## Functions (함수)
#!/bin/bash
function say_hello {
    echo "안녕하세요, $1!"
}
say_hello "사용자"

## Traps (트랩, Ctrl+C 방지)
#!/bin/bash
trap "echo 'Ctrl+C가 감지되었습니다! 종료하지 않습니다.'" SIGINT
while true; do
    echo "프로그램 실행 중... (Ctrl+C를 눌러보세요)"
    sleep 2
done
