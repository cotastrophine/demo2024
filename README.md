# demo2024
# Таблица
| Имя устройства | Интерфейс | IPv4/IPv6 | Маска/Префикс | Шлюз |
| ----------- | ----------- | ----------- | ------------ | ----- |
| ISP         | ens192         | 10.10.201.100 | /24 255.255.255.0 | 10.10.201.254  |
|           | ens224         | 192.168.0.165 | /30 255.255.255.252 |          |
|           |  ens256|  192.168.0.161 | /30 255.255.255.252 |        |
| BR-R        |  ens192        | 192.168.0.129 | /27 255.255.255.224 |     |  
|           |  ens224        | 192.168.0.162 | /30 255.255.255.252 |192.168.0.161 |
| HQ-R        | ens192         | 192.168.0.1 | /25 255.255.255.128 |        |
|        |    ens224      | 192.168.0.166 | /30 255.255.255.252 |192.168.0.165 |
| HQ-SRV      |  ens192      | 192.168.0.2|   /25 255.255.255.128     | 192.168.0.1 |
| BR-SRV      |     ens192   |192.168.0.130 |  /27 255.255.255.224 | 192.168.0.129 |

# Топология
![eca523ff-a15d-45bd-9a3f-afb7fb81d438](https://github.com/cotastrophine/demo2024/assets/148868116/c5ae32a9-a995-4bf7-9e46-b6b17f77c55c)
1640017)
# Настройка интерфейсов
* Расписала ip адреса с помощью команды

`` nano /etc/network/interfaces ``
* ISP:

```
auto ens192 
  
 iface ens192 inet static 
 
 address 10.10.201.100
 
 geteway 10.10.201.254
 
 netmask 255.255.255.0
```

```
auto ens224 

iface ens224 inet static 
 
address 10.10.0.165
 
 netmask 255.255.255.252
```

```
auto ens256 

iface ens256 inet static 
 
address 192.168.0.161
 
netmask 255.255.255.252``
```
* HQ-R

```
auto ens192 
  
iface ens192 inet static 
 
address 192.168.0.1
 
netmask 255.255.255.128
```


```
auto ens224 
  
iface ens224 inet static 
 
address 192.168.0.166
 
geteway 192.168.0.165
 
netmask 255.255.255.252
```

* BR-R

```
auto ens192 
  
iface ens192 inet static 
 
address 192.168.0.129
 
netmask 255.255.255.224
```

```
auto ens224 
  
iface ens224 inet static

 address 192.168.0.162

 geteway 192.168.0.161
 
 netmask 255.255.255.252
 ```

* HQ-SRV

```
auto ens192 
  
iface ens192 inet static 
 
address 192.168.0.2

geteway 192.168.0.1
 
netmask 255.255.255.128
```

* BR-SRV

```
auto ens192 
  
iface ens192 inet static 
 
address 192.168.0.130``

geteway 192.168.0.129``
 
netmask 255.255.255.224``

systemctl restart networking.service
```

# NAT на ISP, HQ-R,BR-R


``apt install iptables``



 
