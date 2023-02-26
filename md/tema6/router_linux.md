## Máquina Linux actuando como router

En ciertas ocasiones nos va a ser de mucha utilidad tener una máquina que se encargue de hacer de router entre una red y otra. Un ejemplo lo podemos tener en una sala de formación en una empresa donde el ordenador del profesor actúa de router para el resto de ordenadores de la sala, independizando esa sala del resto de la empresa pero permitiéndoles la salida hacia fuera, así como la gestión de otros parámetros que veremos posteriormente.

Para configurar un equipo Linux como router necesitamos realizar unos pasos muy sencillos:

!!!note "Nota" 
	Evidentemente, lo más importante es tener dos tarjetas de red, cada una de ellas conectada a una de las redes que queremos unir

1. Configurar sus interfaces
2. Decirle al sistema que va a actuar como un router
3. Hacer el enmascaramiento de la red interna hacia fuera

¿Qué significa todo esto?

- El *paso 1* lo tenemos claro, configuramos cada interfaz como corresponda en base a la red en la que está conectada
- El *paso 2* es tan sencillo como modificar un parámetro del sistema. Debemos editar el fichero */etc/sysctl.conf* y modificar el valor de *net.ipv4.ip_forward* para que valga 1:

```
net.ipv4.ip_forward = 1
```

- Para el *paso 3* debemos añadir una regla de *iptables* para decirle que realiza dicho enmascaramiento:

```
iptables -t nat -A POSTROUTING -s IP_RED_INTERNA/MASCARA -o INTERFAZ_EXTERNA -j SNAT --to IP_INTERFAZ_EXTERNA
```
*IP_RED_ITERNA/MASCARA* se refiere a la dirección IP y la máscara de la red que va a tener como puerta de enlace la máquina Linux, es decir, en nuestro ejemplo sería la direcicón de la red del aula de formación.
*INTERFAZ_EXTERNA* se refiere al nombre de la interfaz que está conectada a la otra red.
*IP_INTERFAZ_EXTERNA* se refiere a la dirección IP de dicha interfaz.

Si no conociésemos la ip de la interfaz “externa” o fuese dinámica, usaríamos este otro comando:

```
iptables -t nat -A POSTROUTING -s IP_RED_INTERNA/MASCARA -o INTERFAZ_EXTERNA -j MASQUERADE
```

### Cómo incluir una máquina virtual en GNS3

Para poder comprobar el funcionamiento de una máquina Linux como router, podemos configurarla en una máquina virtual e incluirla en uno de nuestros proyectos de GNS3 en los que simularemos las dos redes que interconecta.

Para ello se siguen estos pasos:

- Vamos al menú *Edit-->Preferences-->VirtualBox-->VirtualBox VMs*
- Añadimos la máquina virtual como una plantilla

Una vez hecho esto ya podemos añadir esa máquina a nuestro proyecto.

!!!warning "OJO"
	Tendremos que marcar la casilla correspondiente para que GNS3 se encargue de administrar las interfaces de red y así poder añadir las que necesitemos y conectarlas a las redes internas de GNS3


