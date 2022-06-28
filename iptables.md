sudo apt update -y

sudo apt install iptables-persistent -y


sudo systemctl status netfilter-persistent


# list ip tables

iptables -n -L -v

sudo iptables -L -nv --line-numbers

# delete particular rule

sudo iptables -D INPUT 35


iptables-save  > /etc/iptables/rules.v4

iptables-restore  < /etc/iptables/rules.v4

insert rule with specific rule number
------------------------------------

 iptables -I INPUT 35 -p tcp -s  172.104.190.188/32 --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
 
 

 
 iptables -A INPUT -p tcp -s 192.53.172.92/32 --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
 
 sudo iptables -A OUTPUT -p tcp --sport 5432 -m conntrack --ctstate ESTABLISHED -j ACCEPT
 
 iptables -I INPUT -p tcp -s 192.53.172.92/32 --dport 5432 -j ACCEPT
 
 sudo iptables -A OUTPUT -p tcp --sport 5432 -m conntrack --ctstate ESTABLISHED -j ACCEPT
 
 
 
  iptables -A INPUT -p tcp --dport 80 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
  iptables -A OUTPUT -p tcp --sport 80 -m conntrack --ctstate ESTABLISHED -j ACCEPT
  iptables -A INPUT -p tcp --dport 443 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
  iptables -A OUTPUT -p tcp --sport 443 -m conntrack --ctstate ESTABLISHED -j ACCEPT
  
  
 # Block incoming ping requests

 iptables -A INPUT -p icmp -i eth0 -j DROP
 
 
 #  Block an IP address to a specific network interface on incoming

    iptables -A INPUT -i eth0 -s 192.168.1.102 -j DROP
    
# Block an IP address to reject all packets

  iptables -A INPUT -s 192.168.1.100 -j REJECT    
 
 
# Limit the number of concurrent connections per IP address

 iptables -A INPUT -p tcp --syn --dport 22 -m connlimit --connlimit-above 3 -j REJECT
 
 
 #  How to search entries/rules within the IPtables with grep

   iptables -L INPUT -v -n | grep 192.168.0.100
 
 
 

