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
chmod +x script.sh  # 실행 권한 부여
./script.sh         # 실행

# '! /bin/bash'를 사용하면 자동으로 Bash 환경에서 실행됨
