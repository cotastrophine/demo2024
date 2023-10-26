# demo2024
# Таблица
| Имя устройства | Интерфейс | IPv4/IPv6 | Маска/Префикс | Шлюз |
| ----------- | ----------- | ----------- | ------------ | ----- |
| ISP         | ens192         | 10.10.201.100 | /24 255.255.255.0 | 10.10.201.254  |
|             | ens224         | 192.168.0.161 | /30 255.255.255.252 |           |
|             |  ens225        |  192.168.0.165 | /30 255.255.255.2 |        |
| BR-R        |  ens192        | 192.168.0.129 | /27 255.255.255.224 |       |  
|             |  ens224        | 192.168.0.162 | /30 255.255.255.252 |192.168.0.161 |
| HQ-R        | ens192         | 192.168.0.1 | /25 255.255.255.128 |          |
|             |    ens224      | 192.168.0.166 | /30 255.255.255.252 |192.168.0.165 |
| HQ-SRV      |  ens192      | 192.168.0.2|   /25 255.255.255.128     | 192.168.0.1 |
| BR-SRV      |     ens192   |192.168.0.130 |  /27 255.255.255.224 | 192.168.0.129 |

# Топология
![eca523ff-a15d-45bd-9a3f-afb7fb81d438](https://github.com/cotastrophine/demo2024/assets/148868116/c5ae32a9-a995-4bf7-9e46-b6b17f77c55c)
