# 
ubunt linux 20.04ver nc downlode \n

① xinetd 설치 및 nc 설치 \n
sudo apt-get install netcat          //nc 설치 \n
sudo apt-get install xinetd          //xinetd 설치 \n

② 설치가 완료되면 "/etc/xinetd.d/"라는 디렉터리가 생긴다. 이곳에 스크립트 작성해야 한다. \n
cd /etc/xinetd.d/ \n
vi/etc/xinetd.d/ 설정할 파일 이름 \n

③ 스크립트가 켜지면 아마 빈화면일텐데, 아래와 같이 작성해준다. \n
service "알아보기 편한 이름" \n
{ \n
       socket_type = stream (사용하는 소켓의 종료를 입력하는곳) \n
       flags = REUSE \n
       wait = no \n
       protocol = tcp \n
       user = root (자신의 계정을 입력해야 함 == 현재 권한계정?!) \n
       disable = no \n
       server = "문제 파일" \n
} \n

 .py이 문제파일일 경우 아래와 같이 2줄을 추가해줘야 한다. \n
 server = /usr/bin/python     // which python을 통해 찾은 경로를 넣어줘야함. \n
server_args = /home/srcipt.py    // 문제파일의 경로임. \n

④ 문제에 대한 서비스 설정은 끝났지만, 포트를 개방해주는 설정을 해줘야한다. \n
vi /etc/services     // 서비스에서 포트와 "알아보기 편한 이름"을 설정해주기 위함. \n

⑤ 위 과정을 모두 다했다면 nc연결에 필요한 과정은 전부 끝난 것이며, 아래 와 같이 서비스를 재실행 후 
 점검해보고 정상작동 했다면 끝! \n
 
 service xinetd restart          // xinetd 재시작해야 서비스가 실행된다. \n
nc localhost 1234               // 127.0.0.1 1234이라는 뜻 \n
