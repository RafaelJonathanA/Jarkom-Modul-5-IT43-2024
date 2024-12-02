# Jarkom-Modul-5-IT43-2024

### Kelompok IT43 -

| Name                              |     NRP    |
| ----------------------------------|------------|
| Rafael Jonathan Arnoldus          | 5027231006 | 
| Gandhi Ert Julio                  | 5027231081 |

## Topologi

Topologi 

![image](https://github.com/user-attachments/assets/fa604584-fce0-47e8-be92-46b4acc92188) 

## Tree

![Ttreee](https://github.com/user-attachments/assets/e314edb3-88aa-4c9d-ab54-223b4666aaae)


NewEridu 
```
#NAT
auto eth0
iface eth0 inet dhcp

#A1
auto eth1
iface eth1 inet static
	address 192.238.1.217
	netmask 255.255.255.252

#A5
auto eth2
iface eth2 inet static
	address 192.238.1.221
	netmask 255.255.255.252
```
LuminaSquare
```
#A1
auto eth0
iface eth0 inet static
	address 192.238.1.218
	netmask 255.255.255.252
    gateway 192.238.1.217

#A2
auto eth1
iface eth1 inet static
	address 192.238.1.193
	netmask 255.255.255.248

#A3
auto eth2
iface eth2 inet static
	address 192.238.0.1
	netmask 255.255.255.0
```
BalletTwins
```
#A2
auto eth0
iface eth0 inet static
	address 192.238.1.195
	netmask 255.255.255.248
    gateway 192.238.1.193

#A4
auto eth1
iface eth1 inet static
	address 192.238.1.1
	netmask 255.255.255.128
```

SixStreet
```
#A5
auto eth0
iface eth0 inet static
	address 192.238.1.222
	netmask 255.255.255.252
    gateway 192.238.1.221

#A6
auto eth1
iface eth1 inet static
	address 192.238.1.201
	netmask 255.255.255.248

#A7
auto eth2
iface eth2 inet static
	address 192.238.1.209
	netmask 255.255.255.248
```
ScootOutpost
```
#A7
auto eth0
iface eth0 inet static
	address 192.238.1.211
	netmask 255.255.255.248
    gateway 192.238.1.209

#A8
auto eth1
iface eth1 inet static
	address 192.238.1.225
	netmask 255.255.255.252
```
Outering
```
#A7
auto eth0
iface eth0 inet static
	address 192.238.1.210
	netmask 255.255.255.248
    gateway 192.238.1.209

#A9
auto eth1
iface eth1 inet static
	address 192.238.1.129
	netmask 255.255.255.252
```
HIA
```
#A2 
auto eth0
iface eth0 inet static
	address 192.238.1.194
	netmask 255.255.255.248
    gateway 192.238.1.193
```
HDD
```
#A6 
auto eth0
iface eth0 inet static
	address 192.238.1.202
	netmask 255.255.255.248
    gateway 192.238.1.201
```
Fairy
```
#A6 
auto eth0
iface eth0 inet static
	address 192.238.1.204
	netmask 255.255.255.248
    gateway 192.238.1.201
```
HollowZero 
```
#A8 
auto eth0
iface eth0 inet static
	address 192.238.1.226
	netmask 255.255.255.248
    gateway 192.238.1.225
```
Client 
```
auto eth0
iface eth0 inet dhcp
```
NewEridu  
```
route add -net 192.238.1.128 netmask 255.255.255.192 gw 192.238.1.222 (A9) Ke NewEridu
route add -net 192.238.1.224 netmask 255.255.255.252 gw 192.238.1.222 (A7) Ke NewEridu
route add -net 192.238.1.200 netmask 255.255.255.248 gw 192.238.1.222 (A6) Ke NewEridu 
route add -net 192.238.1.0 netmask 255.255.255.128 gw 192.238.1.218 (A4) Ke NewEridu
route add -net 192.238.1.192 netmask 255.255.255.248 gw 192.238.1.218 (A2) Ke NewEridu
route add -net 192.238.0.0 netmask 255.255.255.0 gw 192.238.1.218 (A3) Ke NewEridu 
route add -net 192.238.1.208 netmask 255.255.255.248 gw 192.238.1.222 (A7) Ke NewEridu 

#Otomasi iptables awal
IP_ETH0=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $IP_ETH0

```

LuminaSquare
```
route add -net 192.238.1.0 netmask 255.255.255.128 gw 192.238.1.195 
route add -net 192.238.1.200 netmask 255.255.255.248 gw 192.238.1.217 
route add -net 192.238.1.128 netmask 255.255.255.192 gw 192.238.1.217
route add -net 192.238.1.224 netmask 255.255.255.252 gw 192.238.1.217 

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt install isc-dhcp-relay -y

echo 'SERVERS="192.238.1.204"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf

service isc-dhcp-relay restart
```

BalletTwins
```
route add -net 192.238.0.0 netmask 255.255.255.0 gw 192.238.1.193  
route add -net 192.238.1.200 netmask 255.255.255.248 gw 192.238.1.193 
route add -net 192.238.1.128 netmask 255.255.255.192 gw 192.238.1.193
route add -net 192.238.1.224 netmask 255.255.255.252 gw 192.238.1.193

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt install isc-dhcp-relay -y

echo 'SERVERS="192.238.1.204"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf

service isc-dhcp-relay restart
```
SixStreet
```
route add -net 192.238.1.128 netmask 255.255.255.192 gw 192.238.1.210
route add -net 192.238.1.224 netmask 255.255.255.252 gw 192.238.1.211
route add -net 192.238.1.192 netmask 255.255.255.248 gw 192.238.1.221
route add -net 192.238.0.0 netmask 255.255.255.0 gw 192.238.1.221
route add -net 192.238.1.0 netmask 255.255.255.128 gw 192.238.1.221 

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt install isc-dhcp-relay -y

echo 'SERVERS="192.238.1.204"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf

service isc-dhcp-relay restart
```
Outering 
```
route add -net 192.238.1.200 netmask 255.255.255.248 gw 192.238.1.209
route add -net 192.238.1.192 netmask 255.255.255.248 gw 192.238.1.209
route add -net 192.238.0.0 netmask 255.255.255.0 gw 192.238.1.209
route add -net 192.238.1.0 netmask 255.255.255.128 gw 192.238.1.209
route add -net 192.238.1.224 netmask 255.255.255.252 gw 192.238.1.211

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt install isc-dhcp-relay -y

echo 'SERVERS="192.238.1.204"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf

service isc-dhcp-relay restart
```
ScoutOutpost 
```
route add -net 192.238.1.128 netmask 255.255.255.192 gw 192.238.1.210
route add -net 192.238.1.200 netmask 255.255.255.248 gw 192.238.1.209
route add -net 192.238.1.192 netmask 255.255.255.248 gw 192.238.1.209
route add -net 192.238.0.0 netmask 255.255.255.0 gw 192.238.1.209
route add -net 192.238.1.0 netmask 255.255.255.128 gw 192.238.1.209

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
```
Fairy
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server netcat -y

echo 'INTERFACESv4="eth0"' > /etc/default/isc-dhcp-server

echo ' #A9
subnet 192.238.1.128 netmask 255.255.255.192 {
        range 192.238.1.130 192.238.1.190;
        option routers 192.238.1.129; # Gateway
        option broadcast-address 192.238.1.191;
        option domain-name-servers 192.238.1.202; #IP HDD
        default-lease-time 600;
        max-lease-time 7200;
}

#A3
subnet 192.238.0.0 netmask 255.255.255.0 {
        range 192.238.0.2 192.238.0.255;
        option routers 192.238.0.1;
        option broadcast-address 192.238.0.255;
        option domain-name-servers 192.238.1.202;
        default-lease-time 600;
        max-lease-time 7200;
}

#A4
subnet 192.238.1.0 netmask 255.255.255.128 {
        range 192.238.1.2 192.238.1.126;
        option routers 192.238.1.1;
        option broadcast-address 192.238.1.127;
        option domain-name-servers 192.238.1.202;
        default-lease-time 600;
        max-lease-time 7200;
}

subnet 192.238.1.216 netmask 255.255.255.252 {}
subnet 192.238.1.192 netmask 255.255.255.248 {}
subnet 192.238.1.220 netmask 255.255.255.252 {}
subnet 192.238.1.200 netmask 255.255.255.248 {}
subnet 192.238.1.224 netmask 255.255.255.252 {}
subnet 192.238.1.208 netmask 255.255.255.248 {}
' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```
HDD
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install bind9 netcat -y

echo 'options {
        directory "/var/cache/bind";

        forwarders {
                192.168.122.1;
        };

        // dnssec-validation auto;
        allow-query{any;};
        auth-nxdomain no;
        listen-on-v6 { any; };
}; ' >/etc/bind/named.conf.options

service bind9 restart
```
Hia
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install apache2 netcat -y

service apache2 start

echo 'Welcome to {Hiahiahia}' > /var/www/html/index.html

service apache2 restart
```
HollowZero
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install apache2 netcat -y

service apache2 start

echo 'Welcome to {Holloww}' > /var/www/html/index.html

service apache2 restart
```

Soal No 2
1. Cara agar masuk internet 
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source [IP eth0] 

2. Agar tidak ada node yang bisa ping ke Fairy tapi Fairy tetap bisa ping ke node lain, lakukan konfigurasi berikut di Fairy
```
# Blokir semua ping yang ditujukan ke Fairy
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP

#Perbolehkan ping yang berasal dari Fairy
iptables -A OUTPUT -p icmp --icmp-type echo-request -j ACCEPT
``` 
![image](https://github.com/user-attachments/assets/d745fcaf-268f-41d8-8905-50345b9df962)

![image](https://github.com/user-attachments/assets/4cfde91d-7922-4ed8-8791-cde7e8ca9613)

Menghapus Aturan
- iptables -D INPUT -p icmp --icmp-type echo-request -j DROP
- iptables -D OUTPUT -p icmp --icmp-type echo-request -j ACCEPT 

3. Agar HDD hanya bisa diakses oleh Fairy, lakukan konfigurasi berikut di HDD

- iptables -A INPUT -s 192.238.1.204 -j ACCEPT
- iptables -A INPUT -j REJECT 

![image](https://github.com/user-attachments/assets/efc2653c-f930-455b-97c7-ad450bcb413b)

![image](https://github.com/user-attachments/assets/6b0729f7-fc17-458b-a149-b5721858ddbd)

Tes NC

#Pada HDD
nc -l -p 1234

#Pada Fairy
nc 192.238.1.202 1234

![image](https://github.com/user-attachments/assets/1a5828cd-a84c-4309-99a9-c3d08297d8a2)

![image](https://github.com/user-attachments/assets/29c0cd33-bb18-41af-b7af-4634e54f576f)

4. Buat HollowZero hanya bisa diakses oleh 4 node dan hanya di hari Senin hingga Jumat, gunakan konfigurasi ini di HollowZero kalau yang lain tidak bisa
Bunice,Caesar,Jane,Policeboo
```
iptables -A INPUT -p tcp -s 192.238.1.130 --dport 80 -m time --timestart 00:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT

iptables -A INPUT -p tcp -s 192.238.1.131 --dport 80 -m time --timestart 00:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT

iptables -A INPUT -p tcp -s 192.238.0.2 --dport 80 -m time --timestart 00:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT

iptables -A INPUT -p tcp -s 192.238.0.3 --dport 80 -m time --timestart 00:00 --timestop 23:59 --weekdays Mon,Tue,Wed,Thu,Fri,Sun -j ACCEPT

iptables -A INPUT -p tcp --dport 80 -j REJECT
```

Untuk Validasi 

curl http://192.238.1.226 

![image](https://github.com/user-attachments/assets/72052e2e-6a70-4e55-8e72-c0ce735b7db4) 

![image](https://github.com/user-attachments/assets/cd912799-b67a-46a2-b564-c82736b5ab74)


5. Atur Konfigurasi sehingga HIA hanya bisa diakses oleh Ellen dan Lycaon pada pukul 08:00 - 21:00 dan bisa diakses oleh Jane serta Policeboo hanya pada pukul 03:00 - 23:00 

Ellen,Lycoan,Jane,Policeboo

```
# Akses Node Ellen dan Lycaon (08:00 - 21:00)
iptables -A INPUT -p tcp -s 192.238.1.2 --dport 80 -m time --timestart 08:00 --timestop 21:00 --weekdays Mon,Tue,Wed,Thu,Fri,Sat,Sun -j ACCEPT

iptables -A INPUT -p tcp -s 192.238.1.3 --dport 80 -m time --timestart 08:00 --timestop 21:00 --weekdays Mon,Tue,Wed,Thu,Fri,Sat,Sun -j ACCEPT

# Akses Node Jane dan Policeboo (03:00 - 23:00)
iptables -A INPUT -p tcp -s 192.238.0.2 --dport 80 -m time --timestart 03:00 --timestop 23:00 --weekdays Mon,Tue,Wed,Thu,Fri,Sat,Sun -j ACCEPT

iptables -A INPUT -p tcp -s 192.238.0.3 --dport 80 -m time --timestart 03:00 --timestop 23:00 --weekdays Mon,Tue,Wed,Thu,Fri,Sat,Sun -j ACCEPT

# Tolak semua koneksi lainnya
iptables -A INPUT -p tcp --dport 80 -j REJECT
```
Untuk Validasi 

curl http://192.238.1.194

![image](https://github.com/user-attachments/assets/60e49f4b-d4b1-469f-83ea-598f5a9a9bbf)

![image](https://github.com/user-attachments/assets/81ceb082-3ed7-4ba8-9006-3db66348a3c3)

6. 

Atur rate limit untuk port scanning (maksimum 25 koneksi per 10 detik)
    
    iptables -N PORTSCAN
    iptables -A INPUT -p tcp --dport 1:100 -m state --state NEW -m recent --set --name portscan
    iptables -A INPUT -p tcp --dport 1:100 -m state --state NEW -m recent --update --seconds 10 --hitcount 25 --name portscan -j PORTSCAN

Blokir IP yang terdeteksi melakukan port scanning tidak wajar
    
    iptables -A PORTSCAN -m recent --set --name blacklist
    iptables -A PORTSCAN -j DROP

Blokir semua aktivitas dari IP yang ada di daftar blacklist
    
    iptables -A INPUT -m recent --name blacklist --rcheck -j REJECT
    iptables -A OUTPUT -m recent --name blacklist --rcheck -j REJECT

Logging untuk port scanning
    
    iptables -A PORTSCAN -j LOG --log-prefix='PORT SCAN DETECTED' --log-level 4

Pengujian :
nmap -p 1-100 192.238.1.194

![image](https://github.com/user-attachments/assets/3c47a078-fa5e-49b4-a1f7-156601187e32)

![image](https://github.com/user-attachments/assets/243d2548-3396-459e-b2de-2e8d38ac33ea)

7. Hanya bisa 2 Ip berbeda

```
iptables -A INPUT -p tcp --dport 80 -m conntrack --ctstate NEW -m recent --set
iptables -A INPUT -p tcp --dport 80 -m conntrack --ctstate NEW -m recent --update --seconds 1 --hitcount 3 -j REJECT
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

Pengujian 
```
parallel curl -s http://192.238.1.226 ::: 192.238.1.2 192.238.1.3 192.238.0.2 192.238.0.3
```
8. 


Soal 3 

1. Memblokir Burnice Hehe byebye

iptables --policy INPUT DROP
iptables --policy OUTPUT DROP
iptables --policy FORWARD DROP 

Pengujian Ping

![image](https://github.com/user-attachments/assets/03c287cb-db29-4bc5-b2ce-46555c44065f)

![image](https://github.com/user-attachments/assets/8c4261fc-7468-4059-808f-994f9f6edbbd) 

Pengujian NC 

