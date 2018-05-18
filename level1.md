level1
===
1. 힌트 파일을 열어본다. 그러면 다음과 같은 것이 쓰여져 있는 것을 볼 수 있다.
 
 level2권한에 setuid가 걸린 파일을 찾는다. 

 2. find 명령어를 이용하여 다음과 같이 검색한다.
 __find / -user level2 -perm -4300 2>/dev/null__

 그러면 /bin/ExcuteMe 파일을 찾을 수 있다.
 3. /bin/ExcuteMe 파일을 실행하면 다음과 같은 메세지가 화면에 뜬다.
 
 <p>레벨 2의 권한으로 당신이 원하는 명령어를 한 가지 실행시켜 드리겠습니다.(단, my-pass와 chmod는 제외) 어떤 명령을 실행시키겠습니까?</p>

4. my-pass와 chmod 명령어를 사용하지 못하므로 /bin/bash명령어를 실행시킨다.
5. level2의 권한을 얻은 것을 확인하고, my-pass를 입력하면 level3의 password를 알아 낼 수 있다.
