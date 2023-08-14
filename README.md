# oracle-cpu-ram
目前甲骨文个人用户已经基本不能注册免费账号了，因此目前保护好自己的账号内的机器显得尤为重要。
以下教程来自荒岛大佬
这里介绍个小工具：lookbusy，这是一个linux系统负载生成器，可以根据你的配置来占用cpu、内存等资源。

apt -y update
apt -y install curl build-essential
curl -L https://github.com/zhangce4221/oracle-cpu-ram/blob/main/lookbusy-1.4.tar.gz -o lookbusy-1.4.tar.gz
tar -xzvf lookbusy-1.4.tar.gz
cd lookbusy-1.4/
./configure && make && make install

新建systemd服务：systemctl edit --full --force lookbusy.service
----------------------------------------------------------------
~~~
[Unit]
Description=lookbusy service
 
[Service]
Type=simple
ExecStart=/usr/local/bin/lookbusy -c 23 -m 51MB
Restart=always
RestartSec=10
KillSignal=SIGINT
 
[Install]
WantedBy=multi-user.target
~~~
----------------------------------------------------------------
参数-c指cpu使用率，-m指内存使用率。
启动并保存:systemctl enable --now lookbusy.service
如果要停止:systemctl disable --now lookbusy.service
检查机器cpu、内存、负载情况:top
~~~
代码区域
~~~
[文章来源](https://ybfl.xyz/sites/167.html)

