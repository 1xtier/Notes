# Настройка ansible для работы с bastion сервером
Настройка ** ssh/config**
```ini
Host jumphost
    HostName 192.168.19.91
    User floki
    IdentityFile ~/.ssh/id_ed25519
Host test1
    HostName 172.2.0.10
    User root
    IdentityFile ~/.myconfig//id_ed25519
    ProxyJump jumphost
```
jumphost Это через какой сервер Ansible пойдет на удаленные хосты!\
test1 Это конечный сервер куда нам нужно достучаться!\
Настройка **ansible/inventory**
```ini
test1 ansible_ssh_host=test1 ansible_ssh_port=22
test2 ansible_ssh_host=test2 ansible_ssh_port=22
test3 ansible_ssh_port=test3 ansible_ssh_port=22
```
Тут важно в ansible_ssh_host указываем имя хостя с **ssh/config** 
