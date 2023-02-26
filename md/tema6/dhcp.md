## Configuración de servidor DHCP en router MikroTik

Vamos a seguir los siguientes pasos para habilitar DHCP en un router y configurarlo de manera que podamos especificar el rango de direcciones que queremos asignar y algunas que queramos excluir para que no sean asignadas nunca.

### Router DHCP

En primer lugar debemos entrar en modo configuración de dhcp, por lo que nos movemos a 

```
/ip/dhcp-server
```
 y, desde ahí, ejecutaremos los siguientes comandos para inr configurando el servicio.
A pesar de que podemos cambiar todos los parámetros con diferentes comandos, lo más cómodo para configurar el servidio desde cero es utilizar el asistente que incorpora RouterOS. Para ello ejecutamos el comando:

```
setup
```

Ahora nos irá preguntando una serie de parámetros. Vamos a verlos uno a uno:
Lo primero que nos solicita es la interfaz en la que vamos a instalar el servidor DHCP.
Elegiremos aquella que nos interese, por ejemplo *ether1*

```
Select interface to run DHCP server on

dhcp server interface: ether1
```

Ahora nos pregunta la red sobre la que va a trabajar el servicio. Le debemos especificar la dirección de red y máscara de la red en la que vamos a trabajar:

```
Select network for DHCP addresses

dhcp address space: 192.168.0.0/24
```

Seguidamente nos solicita la dirección del gateway que va a asignar a los clientes. 

!!!warning "OJO"
	Podemos tener el servidor DHCP en un router diferente al que actúa como gateway para los equipos en la red.

```
Select gateway for given network

gateway for dhcp network: 192.168.0.1
```

Ahora nos solicita la pool de IPs disponibles para asignar. Aquí debemos indicar un rango de IPs que serán las que el servidor asigne, por lo que podemos organizarnos la red de manera que reservemos unos rangos para equipos con configuración estática y otro rango para equipos con DHCP.

```
Select pool of ip addresses given out by DHCP server

addresses to give out: 192.168.0.100-192.168.0.199
```

Ahora nos solicita la dirección de los DNS. Los introduciremos separados por comas:
```
Select DNS servers

dns servers: 10.239.3.7, 10.239.3.8
```

Finalmentenos solicitará el tiempo que va a durar la concesión. Podemos especificarlo en segundos, minutos, horas o días, añadiendo la letra correspondiente a continuación del número que introduzcamos (s,m,h,d)

```
Select lease time

lease time: 3d
```
Con esto ya tendríamos la configuración aplicada.
Como siempre, podemos ver cómo ha quedado mediante el comando:
```
print
```
