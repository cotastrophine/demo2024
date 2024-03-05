# demo2024
# Таблица
| Имя устройства | Интерфейс | IPv4/IPv6 | Маска/Префикс | Шлюз |
| ----------- | ----------- | ----------- | ------------ | ----- |
| ISP         | ens192         | 10.12.34.6 | /24 255.255.255.0 | 10.10.201.254  |
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

* Сохранила конфигурацию
```
Ctrl+S
```
* Вышла из конфигурационного файла
```
Ctrl+X
```
* Перезагрузила сервис работы с сетью
```
systemctl restart networking
```
## 2. Установка и настройка frr
* Установила пакет frr
```
apt-get install frr
```
* Проверила состояние
```
systemctl statys frr
```
* Вошла в файл конфигурации
```
nano /etc/frr/daemons
```
* Изменила значение 
```
ospf=yes
```
* Перезагрузила службу 
```
systemctl restart frr
```
* Вошла в настройку маршрутизации 
```
vtysh
```
* Просмотрела ip адреса и их состояние
```
show ip interface brief
```
* Вошла в конфигурацию терминала 
```
conf t
```
* Запустила процесс 
```
router ospf
```
* Добавила интерфейсы 
```
network (ip адрес) area 0
```
* Просмотрела соседей  
```
do show ip ospf neighbor
```
* Сохранила конфигурацию  
```
copy running-config startup-config
```

## 3.Установка и настройка DHCP
* Установила DHCP
```
apt update
``` 
```
apt install isc-dhcp-server
```
* Вошла в файл настройки
```
nano /etc/default/isc-dhcp-server
```
* Указала интерфейс который смотрит в сторону сервера
```
INTERFACESV4="ens192"
```
* Настроила раздачу адресов
```
nano /etc/dhcp/dhcpd.conf
```
* Пример настройки
```
subnet 192.168.0.0 netmask 255.255.255.128 {
range 192.168.0.2 192.168.0.126;
option domain-name-servers 8.8.8.8, 8.8.4.4;
}
```
* Применила настройку 
```
systemctl restart isc-dhcp-server.service
```
* Включили маршрутизацию 

```
sysctl -a | grep forward 
sysctl -w net.ipv4.ip_forward=1 >> /etc/sysctl.conf
```


# ALT
# Таблица
| Имя устройства | Интерфейс | IPv4/IPv6 | Маска/Префикс | Шлюз |
| ----------- | ----------- | ----------- | ------------ | ----- |
| ISP         |    ens160   | 10.12.34.6    | /24 255.255.255.0   | 10.12.12.254  |
|             |    ens192   | 192.168.0.165 | /30 255.255.255.252 |          |
|             |    ens224   | 192.168.0.161 | /30 255.255.255.252 |          |
| BR-R        |    ens160   | 192.168.0.162 | /30 255.255.255.224 | 192.168.0.161 |  
|             |    ens192   | 192.168.0.129 | /27 255.255.255.252 | |
| HQ-R        |    ens192   | 192.168.0.1   | /25 255.255.255.128 |        |
|             |    ens224   | 192.168.0.166 | /30 255.255.255.252 |192.168.0.165 |
| HQ-SRV      |    ens160   | 192.168.0.2   | /25 255.255.255.128 | 192.168.0.1  |
| BR-SRV      |    ens160   |192.168.0.130  | /27 255.255.255.224 | 192.168.0.129 |
| CLI         |             |               |                  |                |  

* это что бы nano (только там где пингуется на 8.8.8.8)
```
  apt-get update
apt-get install nano
 ```

* Что бы войти в root
```
su
```
*  Необходимо перейти в конфигурационный файл "/etc/net/ifaces/default/options" и поменять значение "CONFIG_IPV6=no на CONFIG_IPV6=yes
  
```
nano(vim) /etc/net/ifaces/default/options
```
* Если таких директорий не существует, то нужно их создать
  
```
mkdir /etc/net/ifaces/ens192
mkdir /etc/net/ifaces/ens224
mkdir /etc/net/ifaces/ens256
```

* В каждой папке нужно создать файл
  
```
touch /etc/net/ifaces/<NAME_INTERFACE>/options
```

```
mcedit /etc/net/ifaces/<NAME_INTERFACE>/options
```

* Для проверки команда

  ```
 cat /etc/net/ifaces/<NAME_INTERFACE>/options
  ```

* Назначить ip

```
nano /etc/net/ifaces/ens_/ipv4address
```

* без nano

```
mcedit /etc/net/ifaces/ens161/ipv4address
```

* Назначить шлюз

```
nano /etc/net/ifaces/ens192/ipv4route
default via 192.168.0.0
```

* В ISP, BR-R, HQ-R настрить маршрутизацию

```
mcedit /etc/net/sysctl.conf
net.ipv4.ip_forward = 1 (поменять 0 на 1)
```

# Тунели BR-R HQ-R
* в BR-R HQ-R в эдите меняет то что смотрит на ISP на WM Network и в optionse меняем static на dhcp
проверяем ping 8.8.8.8

```
apt-get update && apt-get install -y NetworkManager-{daemon,tui}
```

```
systemctl enable --now NetworkManager
```
