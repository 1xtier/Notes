# Работа с netplan
По умолчанию netplan предлагает нам один конфигурационный файл, но это не удобно когда у вас с 10 VLANS и к каждому VLANS с 10 маршрутов или того больше, на много удобнее работать когда конфигурация сети разбита на маленькие отдельные файлы к примеру как centOS или Debian в директории interfaces.d\
Тут стоит упомянуть что netplan будет обрабатывать конфиги по алфавитному порядку!

#### Команды 
Отладка 
```bash
netplan --debug generate
``` 
Применение на 2 минуты после откат на прежднее состояние!
```bash
netplan try
```
Если после TRY все ок то 
```bash
netplan apply
```
***
# Синтаксис конфигурации Netplan
### dchp
```yaml
network: 
  version: 2 
  renderer: networkd 
  ethernets:
    ens33:
      dhcp4: true
```
#### Добавяляем маршруты и DNS
```yaml
routes: 
    - to: default
      via: 0.0.0.0 
  nameservers:
    addresses:
      - 0.0.0.0
      - 0.0.0.0
```
***
### Static
```yaml
network:
  version: 2 
  renderer: networkd 
  ethernets: 
    ens33: 
      dhcp4: false 
      addresses: 
      - 0.0.0.0/0
      gateway4: 192.168.233.2  \ В данный момент использовать не стоит!
      nameservers:
        addresses: 
        - 0.0.0.0 
        - 0.0.0.0
```
#### Добавяляем маршруты и DNS
```yaml
routes: 
    - to: default
      via: 0.0.0.0 
  nameservers:
    addresses:
      - 0.0.0.0
      - 0.0.0.0
```
*** 

### VlANS
```yaml
vlans:
     vlan.45:
     id: 45
     link: ens19
     addresses:  
     - 0.0.0.0/0 
     routes:
       - to: default
         via: 0.0.0.)
     nameservers:
         search: 
         - domain.local 
         addresses: 
         - 0.0.0.0
```

