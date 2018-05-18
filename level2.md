level 2
===
1. 일단 directory안에 있는 파일을 확인하기 위해 ls -a 명령어를 입력하면 derectory안에 있는 hint 파일을 볼 수 있다. 
2. cat hint를 이용해서 hint 파일을 열어보면, 텍스트 파일 편집 중 쉘의 명령을 수행할 수 있다는데...라고 쓰여져 있다. 
3. 그래서 일단 level3의 setuid로 열 수 있는 파일을 찾는다.
find / -user level3 -perm -4300명령어를 입력하면 된다. 
4. 그러면 /usr/bin/editor을 찾을 수 있는데 이 파일에 접근해서 힌트대로 텍스트 파일에서 다음과 같은 명령을 입력하면 level3의 권한을 취득할 수 있다. < :!/bin/bash >
5. 마지막으로 my-pass를 입력하면 level3의 PW를 알아낼 수 있다. 