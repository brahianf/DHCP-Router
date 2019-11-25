# DHCP-Router

Es importante tener la capacidad de conectar en red a todos los dispositivos de forma
rápida y fácilmente, en un mundo hiperconectado donde la falta de conexión es crítica,
aunque se ha implementado durante décadas, DHCP sigue siendo un método esencial
para garantizar que los dispositivos puedan unirse a redes y estén configurados
correctamente de forma automática.
DHCP reduce en gran medida los errores que se producen cuando las direcciones IP se
asignan de forma manual, y puede estirar las direcciones IP al limitar el tiempo que un
dispositivo puede mantener una dirección IP individual.
DHCP simplifica la administración de direcciones IP

### Topología de red

![alt text](https://github.com/brahianf/DHCP-Router/blob/master/TOPOLOGIARED.PNG)


DHCP significa protocolo de configuración de host dinámico y es un protocolo de red utilizado en redes IP donde un servidor DHCP asigna automáticamente una dirección IP y otra información a cada host en la red para que puedan comunicarse de manera eficiente con otros puntos finales.
Además de la dirección IP, DHCP también asigna la máscara de subred, la dirección de puerta de enlace predeterminada, la dirección del servidor de nombres de dominio (DNS) y otros parámetros de configuración pertinentes. La solicitud de comentarios (RFC) 2131 y 2132 define DHCP como un estándar definido por IETF (Internet Engineering Task Force) basado en el protocolo BOOTP.

### Tabla de direccionamiento

![alt text](https://github.com/brahianf/DHCP-Router/blob/master/TABLADIRECCIONAMIENTO.PNG)

La razón principal por la que se necesita DHCP es para simplificar la administración de las direcciones IP en las redes. No hay dos hosts que puedan tener la misma dirección IP, y configurarlos manualmente puede generar errores. Incluso en redes pequeñas la asignación manual de direcciones IP puede ser confusa, especialmente con dispositivos móviles que requieren direcciones IP de forma no permanente.

### Comandos CLI

Router ACADEMICO
```
	Router>enable
    Router#configure terminal 
    Router(config)#hostname ACADEMICO

    ACADEMICO(config)#interface fastEthernet 0/0
    ACADEMICO(config-if)#ip address 172.16.0.1 255.255.0.0
    ACADEMICO(config-if)#ip helper-address 192.168.1.2
    ACADEMICO(config-if)#no shutdown 
    ACADEMICO(config-if)#exit

    ACADEMICO(config)#interface fastEthernet 0/1
    ACADEMICO(config-if)#ip address 10.0.0.1 255.0.0.0
    ACADEMICO(config-if)#ip helper-address 192.168.1.2
    ACADEMICO(config-if)#no shutdown 
    ACADEMICO(config-if)#exit

    ACADEMICO(config)#interface serial 0/0/0
    ACADEMICO(config-if)#ip address 192.168.1.1 255.255.255.0
    ACADEMICO(config-if)#clock rate 64000
    ACADEMICO(config-if)#no shutdown 
    ACADEMICO(config-if)#exit

    ACADEMICO(config)#router rip 
    ACADEMICO(config-router)#version 2
    ACADEMICO(config-router)#no auto-summary
    ACADEMICO(config-router)#passive-interface fastEthernet 0/0
    ACADEMICO(config-router)#passive-interface fastEthernet 0/1 

    ACADEMICO(config-router)#network 172.16.0.0
    ACADEMICO(config-router)#network 10.0.0.0
    ACADEMICO(config-router)#network 192.168.1.0
    ACADEMICO(config-router)#exit



```

Router GESTION
```
    Router>enable 
    Router#configure terminal 
    Router(config)#hostname GESTION
    GESTION(config)#interface fastEthernet 0/0
    GESTION(config-if)#ip address 192.168.55.1 255.255.255.0
    GESTION(config-if)#no shutdown 
    GESTION(config-if)#exit

    GESTION(config)#interface fastEthernet 0/1
    GESTION(config-if)#ip address 192.168.10.1 255.255.255.0
    GESTION(config-if)#no shutdown 
    GESTION(config-if)#exit

    GESTION(config)#interface serial 0/0/0
    GESTION(config-if)#ip address 192.168.1.2 255.255.255.0
    GESTION(config-if)#no shutdown 
    GESTION(config-if)#exit

    GESTION(config)#router rip 
    GESTION(config-router)#version 2
    GESTION(config-router)#no auto-summary
    GESTION(config-router)#default-information originate  
    GESTION(config-router)#passive-interface fastEthernet 0/0
    GESTION(config-router)#passive-interface fastEthernet 0/1 

    GESTION(config-router)#network 192.168.1.0 
    GESTION(config-router)#network 192.168.55.0
    GESTION(config-router)#network 192.168.10.0
 
    GESTION(config)#ip dhcp excluded-address 192.168.10.1 192.168.10.9
    GESTION(config)#ip dhcp excluded-address 192.168.10.254
    GESTION(config)#ip dhcp pool LAN-ADMIN
    GESTION(dhcp-config)#network 192.168.10.0 255.255.255.0
    GESTION(dhcp-config)#default-router  192.168.10.1
    GESTION(dhcp-config)#dns-server 192.168.55.10

    GESTION(config)#ip dhcp excluded-address 172.16.0.1 172.16.0.9
    GESTION(config)#ip dhcp excluded-address 172.16.0.254
    GESTION(config)#ip dhcp pool LAN-PROFESORES
    GESTION(dhcp-config)#network 172.16.0.0 255.255.0.0
    GESTION(dhcp-config)#default-router 172.16.0.1 
    GESTION(dhcp-config)#dns-server 192.168.55.10

    GESTION(config)#ip dhcp excluded-address 10.0.0.1 10.0.0.9
    GESTION(config)#ip dhcp excluded-address 10.0.0.254
    GESTION(config)#ip dhcp pool LAN-ESTUDIANTES
    GESTION(dhcp-config)#network 10.0.0.0 255.0.0.0
    GESTION(dhcp-config)#default-router 10.0.0.1 
    GESTION(dhcp-config)#dns-server 192.168.55.10 
    GESTION(dhcp-config)#end

    GESTION#copy running-config startup-config 
```

### RIPv2.pkt

https://github.com/brahianf/DHCP-Router/blob/master/DHCP-Router.pkt

