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

Create a config file <code>/etc/shadowsocks.json.</code> Example:

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
    