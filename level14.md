level14
===
1. hint 파일을 열어본다. 다음과 같은 내용이 적혀져 있다. 

```c
/*레벨 14이후로는 mainsource의 문제를 그대로 가져왔습니다. 
버퍼 오버 플로우, 포맷 스트링을 학습하는데는 이 문제들이 최고의 효과를 가져다 줍니다.*/
#include<stdio.h>
#include<unistd.h>

main(){
    int crap;
    int check;
    char buf[20];
    fgets(buf, 45, stdin);
    if (check==0xdeadbeef){
        setreuid(3095, 3095);
        system("/bin/sh");
    }
}
```
전 문제들과 마찬가지로 attackme의 소스파일인 것 같다.

위의 소스들을 잘 살펴보면 buf를 20만큼 할당했는데 값은 45만큼 입력받을 수 있다. 그리고 check값을  0xdeadbeef로 하면 level15의 권한이 열린다고 되어있다. 이 정보들을 이용하여 문제들을 풀어보자
2. gdb를 이용하여 안의 내용을 살펴보면 필요한 buf[20]+dummy[20]+check[4]+.....으로 되어있는 것을 확인 할 수 있다. 
3. 위의 정보를 이용해서 40만큼의 더미와 check부분에 deadbeef를 넣어주면 level15의 password를 알 수 있다. 