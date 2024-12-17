Configurando los dominios, agregando los dominios de epartamentos.centro.intranet y centro.intranet

	sudo mkdir /var/www/html/centro.intranet

Para hacer el sudo nos pide la contraseña para loguearse como superusuario

<h6>Foto 1</h6>

	sudo mkdir /var/www/html/departamentos.centro.intranet

<h6>Foto 2</h6>

<h2>APACHE</h2>

Instalamos el servidor web apache. 

	sudo apt install apache2

<h6>Foto 3</h6>

Usaremos dos dominios mediante el archivo hosts: centro.intranet y departamentos.centro.intranet. El primero servirá el contenido mediante wordpress y el segundo una aplicación en python

Para instalar Wordpress primero necesitamos instalar php, con el siguiente comando instalamos php y sus extensiones

	sudo apt install php libapache2-mod-php php-mysql \
	php-curl php-gd php-xml php-mbstring php-zip php-soap php-intl -y
	sudo apt install mysql-server -y

<h6>Foto 4</h6>

creamos un archivo php dentro de una carpeta 

	nano /var/www/html/centro.intranet/index.php

<h6>Foto 5</h6>

Ahora instalamos mysql 

	sudo apt install mysql-server

<h6>Foto 6</h6>

Deténemos el servicio de MySQL

	sudo service mysql stop

<h6>Foto 9</h6>

Me conecto a MySQL sin contraseña

	mysql -u root

<h6>Foto 10</h6>


Accedemos a la configuración de mysql con

	sudo mysql
<h6>Foto 7</h6>

Establecemos la contraseña para el usuario root, que será 'Hola123%

	alter user root '@' localhost identified with mysql_native_password by 'Hola123%'

<h6>Foto 8</h6>

Creamos una base de datos

	Create database ProyecTri Default Character set utf8 COLLATE  utf8_unicode_ci;

<h6>Foto 11</h6>

Creamos un usuario para que pueda usar la base de datos

	Grant all ON ProyecTri.* to ‘Usuario’@’localhost’ identified by 'Hola123%'

<h6>Foto 12</h6>


Salimos de la base

	mysql> exit

<h6>Foto 13</h6>

Añadimos estas líneas en:

	sudo cp /etc/apache2/sities-available/000-default.conf /etc/apache2/sities-available/WordPress.conf

<h6>Foto 14</h6>

	<Directory /var/www/html/centro.intranet>
		AllowOverride All
	</Directory>

<h6>Foto 17</h6>

Activamos el módulo rewrite y reiniciamos apache 

	sudo a2enmod rewrite

<h6>Foto 15</h6>

Modificamos el archivo de configuración de apache
	
	sudo nano /etc/apache2/apache2.conf

<h6>Foto 16</h6>

Preguntamos la ip

	ip a

<h6>Foto 18</h6>

Instalamos WordPress con wget

	wget https://wordpress.org/latest.zip

<h6>Foto 19</h6>

Movemos zip que se ha descargado a la carpeta /etc/www/html 

	sudo mv latest.zip /var/www/html

<h6>Foto 20</h6>

Nos movemos al archivo

	cd /var/www/html/

Vemos si hemos movido todo bien

	ls
 
<h6>Foto 21</h6>

Tras comprobar que está ahí lo vamos a descomprimir

	sudo unzip latest.zip

<h6>Foto 22</h6>

Movemos todo lo de la carpeta "wordpress" a la carpeta

	sudo mv -f wordpress/* centro.intranet/

Ahora  para acceder introducimos la IP/centro.intranet

<h6>Foto 23</h6>
