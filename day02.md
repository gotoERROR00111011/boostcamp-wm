# day02

## Linux

리눅스는 개발자에게 중요한 OS, 개발환경이다.

특히 terminal 환경은 개발자에게 특화되어있다.
반복 작업이 많은 개발자에게 terminal은 gui 중심의 윈도우, 맥 보다 유용하다.

실제로 윈도우는 리눅스의 중요성을 알고 wsl 으로 윈도우에 리눅스 terminal 을 포함시켰다.

그리고 최신의 오픈소스 프로그램들은 리눅스를 우선적으로 개발하는 추세다.
그 예로 인공지능 딥러닝 프레임워크 tensorflow, pytorch 가 있다

### 접근 권한

리눅스는 사용자에 따른 권한 부여로 보안을 지킨다.

파일에 대한 접근 권한은 read, write execute 가 있으며 user, group, other 에 각각 부여된다.

r:4, w:2, x:1 으로 지정한다.

```
# 764 : rwx / rw- / r--
chmod 764
```

그리고 일반 사용자는 사용하지 못하는 root 권한이 있다.
다음 `chown` 처럼 소유자를 바꾸는 명령이 있는데 일반 사용자들이 사용할 수 있다면 접근 권한에 큰 구멍이 뚫리게 된다.

```
chown [USER ID] [FILE]
```

따라서 root와 일부 등록된 sudoers만 root 암호를 통해 행사할 수 있는 권한이다.

### OpenSSH

서버에 원격 접속을 하는 ssh 는 개발자들에게 중요한 기능이다.

ssh를 호스트하기 위해서는 필요한 설치를 진행해야한다.

```bash
sudo apt install openssh-server
```

설치 후 다음 명령으로 상태를 확인할 수 있다.

```
sudo systemctl status ssh
```

그리고 접속을 허용하기 위해서는 다음 명령으로 ssh 포트 방화벽을 허용해야한다.
ssh는 22번 포트를 기본으로 사용하도록 되어있다.

```
sudo ufw allow ssh
```

클라이언트 접속 시에는 서버의 ip를 알고있어야 한다. (`ifconfig`)
접속시에는 공개키 or 비밀번호가 필요하다.

```
ssh [USER ID]@[SERVER IP]
```

백그라운드에서 지속적으로 작동하기 때문에 필요에 따라 on/off 할 수 있다.

```
service ssh stop
service ssh start
service ssh restart
```

## Shell Script

셸 스크립트는 terminal 에서 사용하는 스크립트 언어다.

변수, 조건문, 반복문 등 프로그래밍에 필요한 기능을 가지고 있다.
잘 활용하면 gui 에서 마우스로 수작업 해야하던 것들을 자동화 할 수 있다.

### 명령어

다음은 gui 환경에서 마우스를 통해 자주 일어나는 작업의 명령어들이다.
이것들 이외에도 수많은 명령어들이 있고, 활용법이 있다.
당장 아래의 명령어들도 옵션에 따라서 더 다양한 기능을 제공한다.

파일 리스트를 얻는 명령어

```
ls
```

디렉토리 이동 명령어

```
cd
```

파일 이동 명령어

```
mv
```

파일 복사 명령어

```
cp
```

파일 삭제 명령어

```
rm
```

super user do, root 권한을 사용하는 명령어

```
sudo
```

### curl (Client URL)

curl 명령으로 url 을 통한 송수신이 가능하다.

이를 활용하면 일반적으로 gui 환경에서 작업해야 하는 것들을 자동화 가능하다.

### crontab

특정 시간간격으로 스크립트를 실행하는 기능이다.

다음 명령으로 열린 에디터(nano)에 규칙을 작성하면 된다.

```
crontab -e
```

```
# 분, 시간, 일, 월, 요일
* * * * * [SCRIPT]
*/10 */1 * * * /crontab_script/test.sh
```

[crontab 실험](https://crontab.guru/)

```
service cron stop
service cron start
service cron restart
```
