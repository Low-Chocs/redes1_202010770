# UNIVERSIDAD DE SAN CARLOS DE GUATEMALA
# REDES DE COMPUTADORAS 1
# PRACTICA 2
## Catedrático: Ing. Pedro Pablo Hernández Ramírez
## Auxiliar: Melani López
## ALUMNO: Luis Mariano Moreira García
## CARNET: 202010770

<br>

## Topología de la red
<img src="./Imagenes/1.png" alt="drawing"/><br>
## Ping entre VPC11 Y VP12
<img src="./Imagenes/3.png" alt="drawing"/><br>
## Configuraciones de las pc
<img src="./Imagenes/4.png" alt="drawing"/><br>
<img src="./Imagenes/5.png" alt="drawing"/><br>

## Comandos para verificar:
- show running-config
- show standby

### Creacion del PortChannel PAGP Y LACP
#### PAGP 
##### switch 0
- enable
- configure terminal
- interface range f0/11-12
- channel-group 1 mode desirable
- exit 
- interface port-channel 1
- switchport mode trunk
- end
- wr

##### switch 1
- enable
- configure terminal
- interface range f0/11-12
- channel-group 1 mode auto
- exit 
- interface port-channel 1
- switchport mode trunk
- end
- wr

#### LACP 
##### Switch 2-3
- enable
- configure terminal
- interface range f0/11-12
- channel-group 1 mode active
- exit
- interface port-channel 1
- switchport mode trunk
- end
- wr


### Configuracion de ip a cada router
#### R1
Primera ip configurada:  
- enable
- configure terminal
- interface fa0/1
- ip address 102.168.2.2 255.255.255.248
- no shutdown
Segunda ip configurada:
- enable
- configure terminal
- interface fa0/0
- ip address 102.168.1.2 255.255.255.248
- no shutdown
Tercera ip configurada:
- enable
- configure terminal
- interface se1/0
- ip address 10.0.0.1 255.255.255.252
- no shutdown

#### R2
Primera ip configurada:
- enable
- configure terminal
- interface fa0/0
- ip address 102.168.1.1 255.255.255.248
- no shutdown
Segunda ip configurada:
- enable
- configure terminal
- interface fa0/1
- ip address 102.168.0.2 255.255.255.0
- no shutdown

#### R3
Primera ip configurada:
- enable
- configure terminal
- interface fa0/0
- ip address 102.168.2.1 255.255.255.248
- no shutdown
Segunda ip configurada: 
- enable
- configure terminal
- interface fa0/1
- ip address 102.168.0.3 255.255.255.0
- no shutdown

#### R4
Primera ip configurada:
- enable
- configure terminal
- interface fa0/0
- ip address 102.178.1.1 255.255.255.248
- no shutdown
Segunda ip configurada: 
- enable
- configure terminal
- interface fa0/1
- ip address 102.178.2.1 255.255.255.248
- no shutdown
Tercera ip configurada: 
- enable
- configure terminal
- interface se1/0
- ip address 10.0.0.2 255.255.255.252
- no shutdown

#### R5
Primera ip configurada: 
- enable
- configure terminal
- interface fa0/0
- ip address 102.178.1.2 255.255.255.248
- no shutdown
Segunda ip configurada:
- enable
- configure terminal
- interface fa0/0
- ip address 102.178.0.2 255.255.255.0
- no shutdown
#### R6
Primera ip configurada:
- enable
- configure terminal
- interface fa0/0
- ip address 102.178.2.2 255.255.255.248
- no shutdown
Segunda ip configurada:
- enable
- configure terminal
- interface fa0/0
- ip address 102.178.0.3 255.255.255.0
- no shutdown

## HSRP 
### R2
- enable
- config t
- standby 10 ip 102.168.0.1
- standby 10 priority 150
- standby 10 preempt
### R3
- enable
- config t
- standby 10 ip 102.168.0.1
- standby 10 priority 150
### R5
- enable
- config t
- standby 10 ip 102.178.0.1
- standby 10 priority 150
### R6
-  enable
- config t
-  standby 10 ip 102.178.0.1
- standby 10 priority 150
- standby 10 preempt


## Configuración de las rutas estatícas

### R1
- enable
- config t
- ip route 102.168.0.0 255.255.255.0 102.168.1.1 
- ip route 10.0.0.0 255.255.255.252 10.0.0.2 
- ip route 102.178.1.0 255.255.255.248 10.0.0.2 
- ip route 102.178.0.0 255.255.255.248 10.0.0.2 
- ip route 102.178.2.0 255.255.255.248 10.0.0.2 
### R2
- enable
- config t
- ip route 102.168.1.0 255.255.255.248 102.168.1.2 
- ip route 10.0.0.0 255.255.255.252 102.168.1.2 
- ip route 102.178.1.0 255.255.255.248 102.168.1.2 
- ip route 102.178.0.0 255.255.255.248 102.168.1.2 
- ip route 102.178.2.0 255.255.255.248 102.168.1.2

### R3
- enable
- config t
- ip route 102.178.0.0 255.255.255.0 102.168.2.2 

### R4
- enable
- config t
- ip route 102.178.0.0 255.255.255.0 102.178.1.2 
- ip route 102.178.0.0 255.255.255.0 102.178.2.2 
- ip route 102.168.0.0 255.255.255.0 10.0.0.1 
- ip route 102.168.2.0 255.255.255.248 10.0.0.1 
- ip route 102.178.0.0 255.255.255.0 102.178.0.3 
- ip route 102.168.1.0 255.255.255.248 10.0.0.1 

### R5
- enable
- config t
- ip route 102.178.1.0 255.255.255.248 102.178.1.1 
- ip route 102.168.0.0 255.255.255.0 102.178.1.1 
- ip route 10.0.0.0 255.255.255.252 102.178.1.1 

### R6
- ip route 102.178.2.0 255.255.255.248 102.178.2.1 
- ip route 102.168.0.0 255.255.255.0 102.178.2.1 
- ip route 102.168.2.0 255.255.255.248 102.178.2.1 
- ip route 10.0.0.0 255.255.255.252 102.178.2.1 
- ip route 102.168.1.0 255.255.255.248 102.178.2.1
