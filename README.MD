WELL
IT WELL RUN ON 2018/1

MAY BE USEFULL FOR THE OTHER

SAMPLE IS SET ON TAIWAN ISP

树莓
	
	用网线SSH直插树莓
		电脑设定共享网路 - RJ45 会变DHCP SERVER，自动分IP给树莓，再用arp -a刷出树莓的IP
	登入改密码
		用PUTTY SSH连到树莓 帐:pi  密:raspberry，输入passwd，改pi的密码
		改成pi  pwDESU123456789
		开root
			sudo passwd root
			sudo passwd --unlock root
			su root
			 登入看看
	开启WIFI，开完就可以拔网线了
		#找ssid
		sudo iwlist wlan0 scan  
		#用nano指令设定wifi，
		sudo nano /etc/wpa_supplicant/wpa_supplicant.conf  
			    network={  
					ssid="XXXX"  
					psk="XXXX"  
				}  
		#改完重开树莓
		sudo reboot
	python 2.7 -> 3.6.2
		wget https://www.python.org/ftp/python/3.6.2/Python-3.6.2.tar.xz
		xz -d  Python-3.6.2.tar.xz
		tar -xvf  Python-3.6.2.tar
		cd Python-3.6.2
		./configure
	shadowsocks   run as root
		sudo apt-get update
		sudo apt-get install python-pip
		sudo pip install shadowsocks
		
		
		
ubuntu mate on raspi  use  ssr bbr
	*1.开SSH，开ROOT，必须用HDMI跟键盘滑鼠
	*2.开PPPOE，开机自动刷到固定IP
	*3.刷TEDDY SSR 或PYTHON SSR 
	*4.刷新内核，开启tcp-bbr
	*5.安装远端，特殊异常排除
	
	1.开SSH，开ROOT必须在HDMI GUI，必须用HDMI跟键盘滑鼠
		sudo systemctl enable ssh
		sudo systemctl start ssh
		
		sudo passwd root
		sudo passwd --unlock root
		su
	2.开PPPOE，开机自动刷到固定IP
		sudo apt-get -y install pppoeconf
		sudo pppoeconf
		YOUR HINET ACCOUNT@ip.hinet.net
		YOUR HINET PW
		#出现的全部按是，ifconfig 确认ppp的ip是否为ISP给的固定IP
		reboot
	3.进root刷teddy的SSR  https://teddysun.com/486.html  (THX TEDDY ，NICE BASH FOR SSR)
		wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
		chmod +x shadowsocks-all.sh
		./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
	4.刷新内核到4.9，开启tcp-bbr
		sudo  rpi-update
		sudo reboot
		uname -r
		sudo bash -c 'echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf'
		sudo bash -c 'echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf'
		sysctl -p
		sudo reboot
		
		# sysctl net.ipv4.tcp_available_congestion_control
		net.ipv4.tcp_available_congestion_control = bbr cubic reno
 
		# lsmod | grep bbr
		tcp_bbr                20480  14
	5.安装远端，特殊异常排除
		sudo apt-get install xrdp
		sudo /etc/init.d/xrdp start
	


	使用VPS WGET 简易下载东西
		WGET -c -O GOGOSETUP.ZIP http://yoyoyo.com/defsdfasefawefawefawef.zip
		-c : 断线自动续传	-O : 类似另存新档，直接给定挡案名称
