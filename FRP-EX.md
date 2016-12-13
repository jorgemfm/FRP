#Fundamentos de Redes e Protocolos - Trabalho
## Instalar SSH

1. Instalar SSH
```bash
tce-load -wi openssh
```
2. Iniciar o serviço
```bash
sudo /usr/local/etc/init.d/openssh start
```
3. Adicionar o inicio do serviço qd a maquina faz boot
```bash
echo "/usr/local/etc/init.d/openssh start">> /opt/bootlocal.sh
```



Gravar as configurações
```bash
sudo /usr/bin/filetool.sh -b
```


## PC1
```bash
echo "/usr/local/etc/init.d/openssh start" >> /opt/bootlocal.sh
echo "hostname PC1">> /opt/bootlocal.sh
echo "ifconfig eth0 192.168.2.101 netmask 255.255.255.0" >> /opt/bootlocal.sh
echo "route add default gw 192.168.2.1" >> /opt/bootlocal.sh

sudo sh /opt/bootlocal.sh
sudo /usr/bin/filetool.sh -b
```


## PC2
```bash
echo "/usr/local/etc/init.d/openssh start">> /opt/bootlocal.sh
echo "hostname PC2">> /opt/bootlocal.sh
echo "ifconfig eth0 192.168.2.100 netmask 255.255.255.0" >> /opt/bootlocal.sh
echo "route add default gw 192.168.2.1" >> /opt/bootlocal.sh

sudo sh /opt/bootlocal.sh
sudo /usr/bin/filetool.sh -b
```

## PC3
```bash
echo "hostname PC3">> /opt/bootlocal.sh
echo "ifconfig eth0 192.168.1.100 netmask 255.255.255.0" >> /opt/bootlocal.sh
echo "route add default gw 192.168.1.1" >> /opt/bootlocal.sh

sudo sh /opt/bootlocal.sh
sudo /usr/bin/filetool.sh -b
```


## Router 3
###Interface 0/0
```bash
interface FastEthernet 0/0
ip address 192.168.0.1 255.255.255.0
no shutdown
```

###Interface 0/1
```bash
interface FastEthernet 0/1
ip address 192.168.1.1 255.255.255.0
no shutdown
```

###Rota
```bash
ip route 192.168.2.0 255.255.255.0 192.168.0.2
```

## Router 1
###Interface 0/0
```bash
interface FastEthernet 0/0
ip address 192.168.2.1 255.255.255.0
no shutdown
```

###Interface 0/1
```bash
interface FastEthernet 0/1
ip address 192.168.0.2 255.255.255.0
no shutdown
```

###Rota
```bash
ip route 192.168.1.0 255.255.255.0 192.168.0.1
```
