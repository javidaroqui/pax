## Configuración de un router en GNS3

GNS3 permite añadir diferentes imágenes de routers para poder configurarlos en nuestros proyectos.

Nosotros vamos a trabajar con MikroTik CHR. Para instalarlo debemos seguir tres pasos:

- Descargar el fichero del appliance
- Descargar los ficheros de una de las versiones soportadas (usaremos la más actual)
- Importar en GNS el fichero .gns3a

Tenemos las instrucciones a seguir en este enlace:

https://gns3.com/marketplace/appliances/mikrotik-cloud-hosted-router

## Operaciones a realizar en el router

Vamos a manejar el router mediante RouterOS, un sistema muy sencillo de gestionar que utilizan los routers MikroTik. En principio vamos a ver dos acciones que tendremos que realizar y, más adelante, ampliaremos con otras funciones.
RouterOS utiliza una especie de sistema de ficheros similar a la estructura de un sistema Linux. Para realizar las acciones de configuración, nos situaremos en el directorio correspondiente, como veremos a continuación.

### Configurar las interfaces

Para configurar las interfaces debemos movernos al directorio correspondiente a la configuración de interfaces (/ip/address) y allí utilizar el comando correspondiente para configurar una interfaz. En dicho comando indicaremos la IP que queremos asignar, la máscara y la interfaz que estamos configurando. 
Un ejemplo para ocnfigurar la interfaz ether1 con la IP 192.168.1.13 y máscara /24 sería el siguiente:

```
/ip/address
add address=192.168.1.13/24 interface=ether1
```

###Configurar las tablas de rutas

Para configurar las tabals de rutas debemos irnos al directorio /ip/route y ejecutar el comando correspondiente para añadir cada una de las rutas. El comando esbásicamente lo mismo que aparece en las tablas que diseñamos anteriormente pero incluso más sencillo, ya que no hace falta indicar la interfaz, pues el router deduce cuál es a partir de las IPs de la tabla. Veamos un ejemplo:

```
/ip/route
add dst-address=172.29.0.0/16 gateway=10.0.0.1
```

