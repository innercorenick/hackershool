level8
===
1. 힌트파일을 열어보면 다음과 같은 메세지가 있다.
level9의 shasow 파일이 서버 어딘가에 숨어있다.
그 파일에 대해 알려진 것은 용량이 "2700"이라는 것 뿐이다.
2. find / -size 2700c 2>/dev/null을 이용하여 찾으면 /etc/rc.d/found.txt파일을 찾을 수 있다.
3. /etc/rc.d/found.txt 파일에 접근해서 안의 내용을 살펴보면 다음과 같은 암호화된 구문이 보인다

level9:__$1$vkY6sSlG$6RyUXtNMEVGsfY7Xf0wps.__:11040:0:99999:7:-1:-1:134549524
4. $1$vkY6sSlG$6RyUXtNMEVGsfY7Xf0wps.이 구문을 johntheripper에 넣고 돌리면 level9의 password를 알아낼 수 있다.