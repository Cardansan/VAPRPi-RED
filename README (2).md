# Carrito3D v2 (VAPRPi-RED)
## Pasos para la instalación del software
### 1) Instalar Node-RED.
Descargar la última versión de Node-RED para la imagen de Raspbian que usará la raspberry. Habilitar el servicio para que Node-RED corra en cada encendido.
### 2) Liberar el mayor espacio posible para ejecutar Node-RED.
Ir a /lib/systemd/system/nodered.service para editar el max-old-space a una cantidad razonable. Se ha probado con 1024 exitosamente. Detener, ejecutar "sudo systemctl daemon-reload" y volver a correr Node-RED.
### 3) Habilitar la conexión a la cámara de la raspberry.
Desde raspi-config habilitar la cámara. Recuerda que después de esto necesitarás reiniciar la rasp (siguiente paso).
### 4) Configuración previa para el control de servos.
Modificar el documento /etc/rc.local y añadir la línea "/usr/bin/pigpiod" al final del archivo, justo antes del último "exit 0". Requiere reinicio de la Raspberry.

### 5) Activar la transmisión y recolección de video via web.
[Probablemente se necesite actualizar o instalar php como aquí: http://www.heidislab.com/tutorials/installing-php-7-1-on-raspbian-stretch-raspberry-pi-zero-w  o como se describe en el archivo Php_Install_Instructions hallado en este repo. (usar al menos la versión 7.3) Si se pausa el último comando y quedan dos puntos ":" oprimir "q" para continuar.]

Instalar RPi-Cam-Web-Interface tal como se menciona en la página: https://elinux.org/RPi-Cam-Web-Interface#Installation_Instructions

### 6) Importar los flujos.
Desde Node-RED importar los flujos hallados en este repositorio. 
### 7) Instalar los nodos faltantes.
No todos los nodos que se usarán vienen en la instalación default de Node-RED, así que se debe revisar cuáles se necesitan instalar desde Manage Palette.
### 8) Desplegar los flujos.
Esto hará que se empiecen a ejecutar siempre que se encienda la raspberry y la interfaz del vehículo deberá de aparecer en el Dashboard de Node-RED con todo y la transmisión del video en vivo.



## Notas
- Por la duración de las descargas e instalaciones, dura aproximadamente entre una y dos horas el proceso completo.
- Otra forma para que la Raspberry Zero se vuelva transmisora de video: https://chriscarey.com/blog/2017/04/30/achieving-high-frame-rate-with-a-raspberry-pi-camera-system/
(Tiene delay de 3 a 5 seg)
- Se presentó una vez el error "mmal: mmal_vc_component_enable: failed to enable component: ENOSPC" solucionado con el comando "sudo pkill raspimjpeg".
- Para que funcionaran los servos de manera correcta se utilizaron los nodos de aquí https://flows.nodered.org/node/node-red-node-pi-gpiod, tomar en cuenta que tienes que modificar el documento /etc/rc.local y añadir la línea "/usr/bin/pigpiod" antes del último "exit 0". Esto trae unas vulnerabilidades que se pueden atender según el mismo enlace. Se encontró que los servos funcionaron mejor con valores de 0-20.
