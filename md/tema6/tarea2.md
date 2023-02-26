## Tarea 2: El IES

Vamos a simular en GNS3 un instituo parecido al nuestro.

El instituto tiene 3 plantas. Hay una LAN principal en el instituto. Cada aula normal tiene un ordenador conectado a esta LAN. Se quiere identificar en qué planta está cada ordenador según su dirección ip.

El departamento de informática tiene una distribución diferente. Hay un router conectado a la LAN principal del instituto que hace que la red del departamento sea independiente..

Hay 3 aulas de formación profesional. Comparten la misma LAN. Se quiere saber a qué aula pertenece un ordenador según su dirección ip. Se quiere otro rango de ip para identificar todos los dispositivos de red de la LAN del departamento de informática (routers, etc)

Hay 2 aulas de informática independientes con un router entre el aula y la LAN del departamento.

- Implementa esta distribución en un Proyecto GNS3.

!!!note "NOTA"
	Crea dos aulas normales en cada planta. Utilice 2 VPCS para representar cada aula normal y 4 VPCS para representar cada aula del departamento de informática.

- Utiliza el direccionamiento ip que consideres mejor, así como la máscara que permita para cumplir con lo especificado.

- Una vez finalizado el ejercicio, exporta el proyecto y súbelo a *Aules*.
