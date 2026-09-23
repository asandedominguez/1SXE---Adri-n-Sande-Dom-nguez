
| Elemento | Lo que dice la documentación | Lo que necesita la VM | Otros (comentarios que consideres relevantes) | Fuente de info |
| --- | --- | --- | --- | --- |
| S.O | Cualquier S.O puede alojar WordPress. Requiere bases de datos, lenguajes de programación, servidor web y servicios compatibles con este (MySQL, PHP)| Utilizo Ubuntu server. límite genérico de 512MB  de memoria RAM por defecto (4GB en mi máquina) <br/> <br/> 1 procesador como mínimo (2 en mi máquina) <br/> <br/> 1GB de disco como mínimo (20 en mi máquina) | Utilizo Ubuntu serever ya que estoy acostumbrado a trabajar con el, además de que es muy estable y podré sacar el máximo provecho a las utilidades de WordPress. | https://www.wpsysadmin.com/seguridad/hosting/versiones/#sistema-operativo <br/> <br/> https://cloudmax.es/aumentar-wp-memory-limit-en-wordpress/ <br/><br/> https://www.wpbeginner.com/es/beginners-guide/important-wordpress-server-requirements-you-should-know/ <br/> <br/> https://www.wpbeginner.com/es/beginners-guide/important-wordpress-server-requirements-you-should-know/ <br/> <br/> https://es.wordpress.org/about/features/|
| Servidor web | Debe contar con: PHP, MariaDB o MySQL, HTTPS, Apache o Nginx. 10GB de capacidad recomendada. "mod_rewrite" (permite reescribir y redirigir URL) | PHP 8.3, MariaDB 10.11, MySQL 8.0, Apache con modo "mod_rewrite" (permite reescribir y redirigir URL)| Se pueden utilizar versiones muy anteriores como PHP 7.4 o MySQL 5.5.5 | https://wordpress.org/about/requirements/ <br/> <br/> https://www.doominio.com/blog/cuanto-espacio-necesito-para-mi-web#1_GB_es_espacio_de_sobra_para_cualquier_web|
| Versión de PHP | 8.3 | 8.3 | No utilizó la versión 8.5 ya que la 8.3 es la mas recomendada | https://wordpress.org/about/requirements/ |
| Gestor de BBDD | MySQL o MariaDB | MySQL | Utilizo MySQL porque ya trabajé con el anteriormente| https://wordpress.org/about/requirements/ |
| Memoria y Disco | Lo recomendado es entre 2-4 RAM y 10 MB de memoria| 4GB de RAM y 20MB memoria en este caso| No le doy lo máximo recomendado ya que considero que no hará falta | https://valebyte.com/es/blog/cu%C3%A1nta-ram-se-necesita-para-alojar-50-sitios-de-wordpress/ |

<br>

En primer lugar prepararemos la máquina virtual, para ello pondremos las siguientes especificaciones (mencionadas en la tabla):

![1.png](Capturas/1.png)

![2.png](Capturas/2.png)

Añadimos la ISO de ubuntu server.

![3.png](Capturas/3.png)

![3.png](Capturas/4.png)

Ponemos el adaptador en puente para que pueda haber comunicación entre la máquina padre y el sistema virtualizado.

![1.png](Capturas/5.png)

Ya está lista para la instalación del sistema operativo, así que la abrimos y comenzamos el proceso (solo explicaré las partes que no sean obvias):

![1.png](Capturas/6.png)

![1.png](Capturas/7.png)

![1.png](Capturas/8.png)

Elegimos la versión estandar de Ubuntu server.

![1.png](Capturas/9.png)


![1.png](Capturas/11.png)

![1.png](Capturas/12.png)

Dejamos que se descarguen estas librerías.

![1.png](Capturas/13.png)

Dejamos la configuración de almacenamiento predeterminada.

![1.png](Capturas/14.png)

![1.png](Capturas/15.png)

Continuamos con el formateo del disco.

![1.png](Capturas/16.png)

![1.png](Capturas/17.png)

Skipeamos la siguiente opción.

![1.png](Capturas/18.png)

Instalamos el servidor SSH para las operaciones posteriores.

![1.png](Capturas/19.png)

Saltamos las siguientes funcionalidades.

![1.png](Capturas/20.png)

Último proceso de descarga

![1.png](Capturas/21.png)

Iniciamos sesión y el S.O, y ya está listo para trabajar.

![1.png](Capturas/22.png)

Nos conectamos mediante SSH desde nuestrá máquina principal

![1.png](Capturas/23.png)

Comenzamos con el proceso de instalación de WordPress con la descarga de las siguientes librerias:

![1.png](Capturas/24.png)

![1.png](Capturas/25.png)

Creamos el directorio /srv/www (la opción -p es para crear el padre si no existe y que no haya errores si ya esta creado).

Hacemos propietario al usuario y grupo www-data, que es el usuarido estandar de Apache, así tendremos todos los privilegios al operar en el.

Con curl descargaremos la versión mas reciente de WordPress y lo guarda en el directorio que creamos antes

![1.png](Capturas/26.png)

Modificamos el fichero de texto especificado con la información que se ve. Hará las siguientes acciones:

- Se escucharán las conexiones provenientes del puerto 80 para que la web se pueda ver en internet.
- Los archivos de la web se guardarán en el directorio /srv/www/wordpress.
- Cualquier usuario puede acceder a la web.
- Habilitá el funcionamiento de WordPress.

![1.png](Capturas/27.png)

Habilitamos WordPress en el servidor Apache.

![1.png](Capturas/28.png)

Habilita el modo mod_rewrite, que permitirá reescribir las URLs para que sean mas legibles a la hora de consultarlas.

![1.png](Capturas/29.png)

Desabilitamos el sitio web que viene por defecto en Apache para poner el nuestro.

![1.png](Capturas/30.png)

Reiniciamos Apache

![1.png](Capturas/32.png)

Accedemos a la consola de SQL con root.

![1.png](Capturas/33.png)

Creamos el usuario WordPress, el cual solo se podrá conectar a SQL en el servidor (es decir, solo se puede conectar localmente). Le ponemos contraseña.

El mensaje de abajo demuestra que la operación se realizó correctamente.

![2.png](Capturas/34.png)

Le damos todos los permisos necesarios al usuario WordPress para operar en el servidor.

![2.png](Capturas/35.png)

Actualizamos y aplicamos los permisos.

![2.png](Capturas/36.png)

Generamos el archivo de configuración de WordPress.

![2.png](Capturas/37.png)

Estas 3 lineas harán lo siguiente (van por orden):

1. Sustituye el nombre predeterminada del servidor por WordPress.
2. El nombre de usuario por por WordPress (el que establecimos).
3. La contraseña por la que pusimos.

(Toda esta información la se porque es la que está en el fichero de configuración, se puede confirmar en la captura de pantalla nº 41).

![2.png](Capturas/38.png)

Entramos en la siguiente ubicación y borramos las líneas que se muestran en la primera imagen, esto sirve para reforzar la seguridad y que las credenciales sean inaccesibles.

![2.png](Capturas/39.png)

![2.png](Capturas/40.png)

Y ponemos la contraseña del servidor en la línea que corresponde.

![2.png](Capturas/41.png)

Con todas estas operaciones ya tendriamos todo correcto para abrir y trabajar en el servidor. Seguí la siguiente guía para realizar este proceso:

https://ubuntu.com/tutorials/install-and-configure-wordpress#1-overview

<br>
<br>

Ahora ponemos nuestra ip en un buscador y ya se abrirá el menú inicial de WordPress.

Ponemos el idioma en español.

![2.png](Capturas/42.png)

Y rellenamos con la información que se ve en pantalla.

![2.png](Capturas/43.png)

![2.png](Capturas/44.png)

Iniciamos sesión con nuestro usuario y contraseña.

![2.png](Capturas/45.png)

Y ya tenemos nuestro servidor abierto, configurado y operativo.

![2.png](Capturas/46.png)
