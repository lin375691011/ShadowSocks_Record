ShadowSocks_Record
=====================

Record for my Debian 7 vps for shadowsocks  
### Delete Apache

    sudo service apache2 stop    
    sudo apt-get purge apache2 apache2-utils apache2.2-bin apache2-common  
    sudo apt-get autoremove  
    sudo rm -rf /etc/apache2


### Install ShadowsSocks
    apt-get install python-pip
    pip install shadowsocks

Create a config file /etc/shadowsocks.json. Example:

    {
        "server":"my_server_ip",
        "server_port":8388,
        "local_address": "127.0.0.1",
        "local_port":1080,
        "password":"mypassword",
        "timeout":300,
        "method":"aes-256-cfb",
        "fast_open": false
    }

Edit the limits.conf

    vim /etc/security/limits.conf

Add these two lines

    * soft nofile 51200
    * hard nofile 51200
    
Edit the sysctl.conf

    vim /etc/sysctl.conf 
    
Add 

    fs.file-max = 51200

    net.core.rmem_max = 67108864
    net.core.wmem_max = 67108864
    net.core.netdev_max_backlog = 250000
    net.core.somaxconn = 3240000

    net.ipv4.tcp_syncookies = 1
    net.ipv4.tcp_tw_reuse = 1
    net.ipv4.tcp_tw_recycle = 0
    net.ipv4.tcp_fin_timeout = 30
    net.ipv4.tcp_keepalive_time = 1200
    net.ipv4.ip_local_port_range = 1000065000
    net.ipv4.tcp_max_syn_backlog = 8192
    net.ipv4.tcp_max_tw_buckets = 5000
    net.ipv4.tcp_fastopen = 3
    net.ipv4.tcp_rmem = 40968738067108864
    net.ipv4.tcp_wmem = 40966553667108864
    net.ipv4.tcp_mtu_probing = 1
    
Input
    
    rm -f /sbin/modprobe
    ln -s /bin/true /sbin/modprobe
    rm -f /sbin/sysctl
    ln -s /bin/true /sbin/sysctl
    sysctl -p

### Install Net_speeder

    apt-get install libnet1
    apt-get install libpcap0.8
    apt-get install libnet1-dev
    apt-get install libpcap0.8-dev
    wget https://net-speeder.googlecode.com/files/net_speeder-v0.1.tar.gz
    tar -zxvf net_speeder-v0.1.tar.gz
    cd net_speeder
    sh build.sh 
    
### Start up

    ulimit -n 51200
    nohup ./net_speeder/net_speeder venet0:0 "ip" >/dev/null 2>log &
    ssserver -c /etc/shadowsocks.json -d start

### Stop

    ssserver -c /etc/shadowsocks.json -d stop
    




## vultr server

###

    wget –no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh
    chmod +x shadowsocksR.sh 
    ./shadowsocksR.sh 2>&1 | tee shadowsocksR.log
    rpm -ivh http://soft.91yun.org/ISO/Linux/CentOS/kernel/kernel-3.10.0-229.1.2.el7.x86_64.rpm --force
    firewall-cmd --zone=public --add-port=3306/tcp --permanent
    firewall-cmd --zone=public --add-port=3306/udp --permanent
    firewall-cmd --zone=public --add-port=1521/tcp --permanent
    firewall-cmd --zone=public --add-port=1521/udp --permanent
    firewall-cmd --zone=public --add-port=1433/tcp --permanent
    firewall-cmd --zone=public --add-port=1433/udp --permanent
    firewall-cmd --zone=public --add-port=1434/tcp --permanent
    firewall-cmd --zone=public --add-port=1434/udp --permanent
    reboot
    
    wget -N --no-check-certificate https://github.com/91yun/serverspeeder/raw/master/serverspeeder.sh && bash serverspeeder.sh
