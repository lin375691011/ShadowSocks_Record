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