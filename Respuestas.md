# Respuestas

## ¿Cuántos y cuáles recursos crea Azure junto con la VM?
Se crean 7 recursos donde nos dan: SSH key, Virtual Network, Virtual machine, Public IP address, 
Network Security group, network interface y a Disk.

## ¿Brevemente describa para qué sirve cada recurso?
**SSH Key:** Azure nos ofrece un par de llaves para poder ingresar a nuestra máquina virtual por medio de SSH, para conectarnos debemos usar nuestra llave privada.

**Virtual Network:** Azure proporciona un entorno aislado, donde podemos usar nuestras propias ip privadas y definir subredes.

**Virtual Machine:** Azure nos proporciona diferentes opciones de sistemas operativos que podemos escoger.

**Public IP addres:** Es una dirección ip que funciona para que distintos usuarios puedan acceder a la máquina virtual mediante la red pública que genera azure.

**Network Security group:** Azure nos permite usar un filtro en el tráfico de red, es decir, que podemos generar reglas que permitan o denieguen el tráfico.

**Network interface:** Azure genera una interfaz de red que nos permite comunicarnos con otros recursos ya sean locales o en internet.

**Disk:** Azure genera un tamaño de almacenamiento para nuestra máquina virtual.

## ¿Al cerrar la conexión ssh con la VM, por qué se cae la aplicación que ejecutamos con el comando npm FibonacciApp.js? ¿Por qué debemos crear un Inbound port rule antes de acceder al servicio?

El comando npm FibonacciApp.js solo ejecuta la aplicación, sin embargo, para mantenerlo activo debemos ejecutar el comando forever start FibinacciApp.js después de haber instalado ***forever***, esto garantizara que después de haber cerrado la conexión la máquina seguirá prestando el servicio.
Debemos crear un Inbound port rula para permitir el tráfico que llega por un puerto determinado, en este caso el 3000

## Adjunte tabla de tiempos e interprete por qué la función tarda tanto tiempo.
![tiempos con size B1ls](img/B1ls)
![tiempos con size B2ms](img/B2ms)
La función tarda tanto tiempo ya que la función tiene un complejidad lineal, por lo tanto a medida que el numero aumenta el tiempo de respuesta de la función es mayor, también como podemos observar el tiempo de respuesta disminuyo drásticamente cuando se le aumento el tamaño (CPUs y ram), y en algunos casos se veía que el tiempo ya no era lineal, ahora bien, depende también de la red al hacer estas pruebas.

## Adjunte imagenes del consumo de CPU de la VM e interprete por qué la función consume esa cantidad de CPU.
![Consumo CPU B1ls](img/CPUB1ls)
![Consumo CPU B2ms](img/CPUB2ms)
Como podemos observar cuando tenemos un tamaño B1ls el consumo de CPU es bastante alto después de realizado las pruebas de carga, está casi llega a un 100%, por otro lado, al usar el tamaño B2ms el consumo de CPU mejora bastante, ya que ahora se encuentra entre un 30% y 40% máximo.


## Adjunte la imagen del resumen de la ejecución de Postman. Interprete:
### Tiempos de ejecución de cada petición.
### Si hubo fallos documéntelos y explique.
![Postman B1ls](img/POSB1ls)
![Postman B2ms](img/POSB2ms)
Al ver el resultado de la ejecución de la carga concurrente, podemos observar que los tiempos difieren uno del otro, sin embargo la cantidad de fallos son muy similares, esto nos da a entender que al hacer un escalamiento horizontal mejoramos los tiempos de respuestas pero no mejoramos su disponibilidad.

## ¿Cuál es la diferencia entre los tamaños B2ms y B1ls (no solo busque especificaciones de infraestructura)?
En infraestructura encontramos que B1ls contiene solo una CPU con 0.5 de RAM, mientras que B2ms tiene 2 CPUs y 8 de RAM. Además, el rendimiento base de B2ms es mucho mejor B1lm.

## ¿Aumentar el tamaño de la VM es una buena solución en este escenario?,

Si se quiere garantizar rendimiento y tiempos de respuestas mejores, es una buena solución, pero se afecta la disponibilidad de la aplicación, ya que como vimos en las pruebas concurrentes, al tener múltiples peticiones, algunas fallan.

### ¿Qué pasa con la FibonacciApp cuando cambiamos el tamaño de la VM?
Mejora el tiempo de respuesta y ya no sobrecargamos la CPU.
### ¿Qué pasa con la infraestructura cuando cambia el tamaño de la VM?
La infraestructura cambia por lo tanto los recursos que usa los diferentes servicios se ve afectada para bien o para mal.
### ¿Qué efectos negativos implica?
Al parecer al cambiar la infraestructura, es necesario reiniciar el servidor, por lo tanto, esto podría costar un tiempo de indisponibilidad, además, si queremos aumentar nuestros recursos de infraestructura, el costo se ve implicado.

### ¿Hubo mejora en el consumo de CPU o en los tiempos de respuesta? Si/No ¿Por qué?
Si, en los dos, ya que, al aumentar los recursos de la máquina, el consumo de CPU disminuyo y los tiempos de respuesta mejoraron.

### Aumente la cantidad de ejecuciones paralelas del comando de postman a 4. ¿El comportamiento del sistema es porcentualmente mejor?
![Postman2](img/POS2)
No, aumentaron la cantidad de fallos en el servidor, por lo tanto, muchas de estas peticiones no se llevaron a cabo.
