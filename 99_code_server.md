# code server

VSCode 온라인

```sh
wget https://github.com/cdr/code-server/releases/download/1.1156-vsc1.33.1/code-server1.1156-vsc1.33.1-linux-x64.tar.gz
tar xvfz code-server1.1156-vsc1.33.1-linux-x64.tar.gz
sudo mv code-server1.1156-vsc1.33.1-linux-x64/code-server /usr/local/bin
mkdir ~/project
cd ~/project
PASSWORD=aqswde nohup code-server -p 8080 --allow-http &
```

http://xxxx:8080 접속합니다. 비밀번호는 1q2w3e4r 입니다.

----
아래 파일을 만들어서 /lib/systemd/system 에 복붙

```
$ sudo systemctl status code-server
$ sudo systemctl start code-server
```

```
cat code-server.service
[Unit]
Description=Code Server IDE
After=network.target

[Service]
Type=simple
User=zihado
Group=zihado
Restart=on-failure
Environment="PASSWORD=mypassword"
RestartSec=10

ExecStart=/usr/local/bin/code-server --port 8000 --allow-http --no-auth /home/zihado/

StandardOutput=file:/var/log/code-server-output.log
StandardError=file:/var/log/code-server-error.log

[Install]
WantedBy=multi-user.target

```
