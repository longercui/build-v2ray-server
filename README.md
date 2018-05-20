# build-v2ray-server
how to build a v2ray server on GCE

ALL OPERATION MUST UNDER SU MODE

#sudo -i

1.calibrate your vps's time
        
        1）calibrate time zone
        
        tzselect
        cat >>~/.profile<<EOF
        TZ='Asia/Shanghai'; export TZ
        EOF
        rm -rf /etc/localtime
        cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
        
        2）auto calibrate time VIA NTD
        vim /etc/ntp.conf
	server 0.debian.pool.ntp.org iburst dynamic
	server 1.debian.pool.ntp.org iburst dynamic
	server 2.debian.pool.ntp.org iburst dynamic
	server 3.debian.pool.ntp.org iburst dynamic
	/etc/init.d/ntp restart
        
        3)check VPS time
        date
        hwclock --show
        
2.upddate&upgrade your VPS OS

        rm /etc/apt/sources.list && vi /etc/apt/sources.list
	deb http://debian-archive.trafficmanager.net/debian jessie main contrib non-free
	deb http://debian-archive.trafficmanager.net/debian-security jessie/updates main contrib non-free
	deb http://debian-archive.trafficmanager.net/debian jessie-updates main contrib non-free
	deb http://debian-archive.trafficmanager.net/debian jessie-backports main contrib non-free
	apt-get update && apt-get upgrade -y
	apt-get -t jessie-backports update && apt-get -t jessie-backports upgrade -y
	apt-get -t jessie-backports install linux-image-amd64 linux-headers-amd64 -y
        
3.install BBR first via one key script

        wget -N --no-check-certificate https://raw.githubusercontent.com/FunctionClub/YankeeBBR/master/bbr.sh && bash bbr.sh install
        ------------push TAB button,choose NO,and REBOOT------------
        bash bbr.sh start
4.install v2ray server

        bash <(curl -L -s https://install.direct/go.sh)
        -------wait and done--------
     
5.install some useful command
        apt-get install lrzsz
        
6.v2ray files directory

        /usr/bin/v2ray/v2ray：V2Ray 程序；
	/usr/bin/v2ray/v2ctl：V2Ray 工具；
	/etc/v2ray/config.json：配置文件；
	/usr/bin/v2ray/geoip.dat：IP 数据文件
	/usr/bin/v2ray/geosite.dat：域名数据文件

	编辑 /etc/v2ray/config.json 文件来配置你需要的代理方式；
	运行 service v2ray start 来启动 V2Ray 进程；
	之后可以使用 service v2ray start|stop|status|reload|restart|force-reload 控制 V2Ray 的运行
        
7.v2ray Commonly used commands

	systemctl start v2ray   开始
	systemctl stop v2ray   停止
	systemctl restart v2ray 重启
	systemctl status v2ray  状态
	
	/usr/bin/v2ray/v2ray -test -config config.json -检查json配置文件正确性
        
 hope you enjoy the real internet!
        





