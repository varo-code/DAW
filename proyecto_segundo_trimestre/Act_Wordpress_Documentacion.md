<h1>Instalación de Wordpress en instancia Debian(o Ubuntu) EC2 con soporte de base de datos RDS y EFS</h1>

<h2>Creamos la VPC</h2>

<ul>Lo Primero que vamos ha hacer dentro de nuestro labotario en AWS Buscar la opción de VPC.</ul>

![Foto 1](imagen_trabajo/foto_1.png)

<ul>Una vez dentro hacemos click sobre el boton de "<b>Crear VPC</b>".</ul>

![Foto 2](imagen_trabajo/foto_2.png)

<ul>Tras hacer click podremos configurar la máquina adaptandonos a los requisitos requeridos.</ul>

![Foto 3](imagen_trabajo/foto_3.png)

![Foto 4](imagen_trabajo/foto_4.png)

![Foto 5](imagen_trabajo/foto_5.png)

<ul>Tras completar los campos de los atributos de la VPC, hacemos click sobre el boton de "<b>Crear VPC</b>".</ul>

![Foto 6](imagen_trabajo/foto_6.png)

<ul>Ahora se estará creando la VPC, y podemos verla en  "<b>Ver VPC</b>".</ul>

![Foto 7](imagen_trabajo/foto_7.png)

<h2>Creamos la EC2</h2>

<ul>Vamos al buscador dentro de nuestro labotario en AWS Buscar la opción de EC2.</ul>

![Foto 8](imagen_trabajo/foto_8.png)

<ul>Tras marcar la opción de EC2, en el menu izquierdo hacemos click sobre <b>Instancias</b>.</ul>

![Foto 9](imagen_trabajo/foto_9.png)

<ul>Para lanzar la instancia pulsamos sobre el boton de <b>Lanzar Instacias</b>.</ul>

![Foto 10](imagen_trabajo/foto_10.png)

<ul>Ahora le pondremos un nombre y eligiremos el OS que será Ubuntu.</ul>

![Foto 11](imagen_trabajo/foto_11.png)

<ul>Tras finalizar la configuración, lo guardamos pulsando sobre el boton de <b>Lanzar Instacias</b>.</ul>

![Foto 12](imagen_trabajo/foto_12.png)

<ul>Nos permetirá ver todas las instancias si pulsamos el boton de <b>Ver todas las instancias</b>.</ul>

<ul>Seleccionamos la instancia que nos interese comprobamos si las IPs esten correctas.</ul>

![Foto 13](imagen_trabajo/foto_13.png)

<ul>Como hemos seleccionado la instancia que nos interese pulsamos el boton de "<b>Conectar</b>".</ul>

![Foto 14](imagen_trabajo/foto_14.png)

<ul>Tras pulsar nos saldra un menú en el cual podremos elegir la manera de como podremos tener la conexión.</ul>

![Foto 15](imagen_trabajo/foto_15.png)

<ul>Finalmente nos conectamos a la máquina.</ul>

![Foto 16](imagen_trabajo/foto_16.png)

<h2>Instalación de Apache y PHP</h2>

<ul>Ahora instalaremos el servidor apache mediante los siguientes comandos.</ul>


    sudo apt update
    sudo apt install apache
    
![Foto 17](imagen_trabajo/foto_17.png)

![Foto 18](imagen_trabajo/foto_18.png)

<ul>Actualizamos nuestra máquina e instalamos apache.</ul>

<ul>Iniciamos apache y habilitamos para que incie siempre.</ul>

    sudo systemctl start apache2
    sudo systemctl enable apache2


<ul>Con el siguiente comando instalaremos como un módulo de Apache el php</ul>

    sudo apt -y update && sudo apt upgrade

![Foto 19](imagen_trabajo/foto_19.png)

<ul>Ahora comprobamos la versión de y que la instalación es correcta.</ul>

    php -v

<ul>Tambien necesitamos un modulo de apache  para la bsae de datos en este caso usaremos MySQL.</ul>

    sudo apt install php-mysql

![Foto 20](imagen_trabajo/foto_20.png)

<ul>Tras añadir la base de datos reiniciamos apache</ul>

    sudo systemctl restart apache2

<h2>Creación de Base de Datos</h2>

<ul>Vamos ha hacer dentro de nuestro labotario en AWS Buscar la opción de RDS.</ul>

![Foto 21](imagen_trabajo/foto_21.png)

<ul>Le damos al botónde "<b>Crear base de datos</b>"</ul>

![Foto 22](imagen_trabajo/foto_22.png)

<ul>Vamos ha configuramos la base de datos.</ul>

![Foto 23](imagen_trabajo/foto_23.png)

![Foto 24](imagen_trabajo/foto_24.png)

<ul>Introducimos un nombre a la base de datos, una credenciales y contraseña.</ul>

![Foto 25](imagen_trabajo/foto_25.png)

![Foto 26](imagen_trabajo/foto_26.png)

![Foto 27](imagen_trabajo/foto_27.png)

![Foto 28](imagen_trabajo/foto_28.png)

![Foto 29](imagen_trabajo/foto_29.png)

<ul>Una vez todo configurado, creamos la base de datos.</ul>

![Foto 22](imagen_trabajo/foto_22.png)

<ul>Ahora configuramos la conexión a la base de datos con una configuración insegura para un proyecto de una empresa pero este proyecto servirá.</ul>

![Foto 30](imagen_trabajo/foto_30.png)

<ul>La configuración de conexión de EC2.</ul>

<ul>Seleccionamos la instancia EC2 que nos interese.</ul>

<h2>Elastic File System</h2>

<ul>Vamos a hacer dentro de nuestro labotario en AWS Buscar la opción de EFS.</ul>

![Foto 31](imagen_trabajo/foto_31.png)

<ul>Hacemos click sobre el btón de <b>Crear un sistemas de archivos</b></ul>

![Foto 32](imagen_trabajo/foto_32.png)

<ul>Le pondremos un nombre y elegimos la VPC de la práctica</ul>

![Foto 33](imagen_trabajo/foto_33.png)

<ul>Confirmamos que se haya creado</ul>

![Foto 34](imagen_trabajo/foto_34.png)

<ul>Asociamos la EFS a nuestra instancia y haciendo clic en "Asociar"</ul>

![Foto 35](imagen_trabajo/foto_35.png)

<ul>Nos explica como poder conectarse y elegimos la segunda opción</ul>

![Foto 36](imagen_trabajo/foto_36.png)

<ul>Antes de ejecutar el comando proporcionado crearemos la carpeta "efs".</ul>

    sudo mkdir efs
    
<ul>Después de crear la carpeta "efs" ejecutamos el comando de creación del paquete nfs-common</ul>

    apt-get install nfs common

![Foto 37](imagen_trabajo/foto_37.png)

<h2>Instalación de Wordpress</h2>

<ul>Accedemos al directorio /var/www/html y ejecutamos el siguiente comando para poder descargar wordpress</ul>

    sudo wget https://wordpress.org/latest.tar.gz

![Foto 38](imagen_trabajo/foto_38.png)

<ul>Para descomprimirlo</ul>

    sudo tar -xf latest.tar.gz
    
<ul>Ahora la carpeta de wordpress esta descomprimida y tenenmos que crear unas credenciales, con las cuales nos conectaremos a la instancia de la base de datos mediante el punto de acceso de nuestra propia base de datos y poniendo nuestra contraseña</ul>

    sudo apt install default-mysql-client
    sudo mysql -u admin -h database-1.c1xhozphuei9.us-east-1.rds.amazonaws.com -p


<ul>Creamos la base de datos y el usuario</ul>

    CREATE DATABASE wordpress; 
    CREATE USER 'usuario' IDENTIFIED BY 'usuario'; 
    GRANT ALL PRIVILEGES ON wordpress.* TO 'usuario'; 
    FLUSH PRIVILEGES;

<ul>Ahora buscamos la nuestra IP publica mas /wordpress nos aparecerá esto.</ul>

![Foto 39](imagen_trabajo/foto_39.png)

<ul>Le damos al botón que pone "<b>Let's go</b>" y rellenamos los campos requeridos.</ul>




