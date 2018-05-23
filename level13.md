level13
===
1. hint 파일을 열어본다. 그러면 다음과 같은 내용을 볼 수 있다. 
```c
#include <stdio.h>

main(int argc, char *argv[]){
    long i=0x1234567;
    char buf[1024];

    setreuid(3094, 3094);
    if(argc>1)
    strcpy(buf, argv[1]);

    if (i != 0x1234567){
        printf("Warnning: Buffer Overflow !!! \n");
        kill(0, 11);
    }
}
```
attackme의 소스파일로 보인다.
위의 소스코드를 보니 attackme를 공격할 때 i의 값을 0x1234567로 만들어 주면 될 것 같다.
2. gdb -q attackme 명령어를 이용해 attackme내부를 살펴보면 buf가 1048만큼 할당되어 있는 것이 보인다. 
3. 위의 정보를 이용하여 공격코드를 짜보면

buf[1024]+dummy[12]+i[4]+dummy[8]+sfp[4]+shellcode의 주소[4]

4. /tmp/getenv를 이용하여 shellcode의 주소를 구한 후 attackme를 공격하면 level14의 password를 알 수 있다. 
