level9
===
level9
===
1. 힌트 파일을 열면 다음과 같은 메세지가 적혀있다.

다음은 /usr/bin/bof의 소스이다.
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>

main(){
    char buf2[10];
    char buf[10];

    printf("Is can be overflow : ");
    fgets(buf, 40, stdin);

    if (strncmp(buf2, "go", 2)==0){
        printf("Good Skill!\n");
        setreuid(3010, 3010);
        system("/bin/bash");
    }
}
```
위의 소스파일을 보면 buf는 10칸을 할당받았는데 40까지 입력할 수 있게 되어있는 것이보인다. 이것을 이용하여 문제를 풀면 될 것 같다. 
2. /usr/bin에 접근해서 bof파일을 실행한다.
3. buf2에 go가 들어갈 수 있도록 0123456789012345go를 입력한다.
4. level10의 password를 알아낸다.

