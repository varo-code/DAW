<h1>Proyecto de Álvaro Delcán Pérez</h1>
<br><br>
Configurando los dominios, agregando los dominios de epartamentos.centro.intranet y centro.intranet


	sudo mkdir /var/www/html/centro.intranet

Para hacer el sudo nos pide la contraseña para loguearse como superusuario

![Foto 1](/Proyecto/FotosDeComands/ParteApache/Foto1.png)

<h6>Foto 1</h6>

	sudo mkdir /var/www/html/departamentos.centro.intranet

![Foto 2](/Proyecto/FotosDeComands/ParteApache/Foto2.png)

<h6>Foto 2</h6>

<br><br>

<h2>APACHE</h2>

<br><br>

Instalamos el servidor web apache. 

	sudo apt install apache2

![Foto 3](/Proyecto/FotosDeComands/ParteApache/Foto3.png)

<h6>Foto 3</h6>


Usaremos dos dominios mediante el archivo hosts: centro.intranet y departamentos.centro.intranet. El primero servirá el contenido mediante wordpress y el segundo una aplicación en python

Para instalar Wordpress primero necesitamos instalar php, con el siguiente comando instalamos php y sus extensiones

	sudo apt install php libapache2-mod-php php-mysql \
	php-curl php-gd php-xml php-mbstring php-zip php-soap php-intl -y
	sudo apt install mysql-server -y

![Foto 4](/Proyecto/FotosDeComands/ParteApache/Foto4.png)

<h6>Foto 4</h6>


creamos un archivo php dentro de una carpeta 

	nano /var/www/html/centro.intranet/index.php

![Foto 5](/Proyecto/FotosDeComands/ParteApache/Foto5.png)

<h6>Foto 5</h6>

Ahora instalamos mysql 

	sudo apt install mysql-server

![Foto 6](/Proyecto/FotosDeComands/ParteApache/Foto6.png)

<h6>Foto 6</h6>


Deténemos el servicio de MySQL

	sudo service mysql stop

![Foto 9](/Proyecto/FotosDeComands/ParteApache/Foto9.png)

<h6>Foto 9</h6>

Me conecto a MySQL sin contraseña

	mysql -u root

![Foto 10](/Proyecto/FotosDeComands/ParteApache/Foto10.png)

<h6>Foto 10</h6>


Accedemos a la configuración de mysql con

	sudo mysql

 ![Foto 7](/Proyecto/FotosDeComands/ParteApache/Foto7.png)
 
<h6>Foto 7</h6>

Establecemos la contraseña para el usuario root, que será 'Hola123%

	alter user root '@' localhost identified with mysql_native_password by 'Hola123%'

![Foto 8](/Proyecto/FotosDeComands/ParteApache/Foto8.png)

<h6>Foto 8</h6>

Creamos una base de datos

	Create database ProyecTri Default Character set utf8 COLLATE  utf8_unicode_ci;

![Foto 11](/Proyecto/FotosDeComands/ParteApache/Foto11.png)

<h6>Foto 11</h6>

Creamos un usuario para que pueda usar la base de datos

	Grant all ON ProyecTri.* to ‘Usuario’@’localhost’ identified by 'Hola123%'

![Foto 12](/Proyecto/FotosDeComands/ParteApache/Foto12.png)
<h6>Foto 12</h6>


Salimos de la base

	mysql> exit

![Foto 13](/Proyecto/FotosDeComands/ParteApache/Foto13.png)

<h6>Foto 13</h6>

Añadimos estas líneas en:

	sudo cp /etc/apache2/sities-available/000-default.conf /etc/apache2/sities-available/WordPress.conf

![Foto 14](/Proyecto/FotosDeComands/ParteApache/Foto14.png)

<h6>Foto 14</h6>

	<Directory /var/www/html/centro.intranet>
		AllowOverride All
	</Directory>

![Foto 17](/Proyecto/FotosDeComands/ParteApache/Foto17.png)
<h6>Foto 17</h6>

Activamos el módulo rewrite y reiniciamos apache 

	sudo a2enmod rewrite

![Foto 15](/Proyecto/FotosDeComands/ParteApache/Foto15.png)

<h6>Foto 15</h6>

Modificamos el archivo de configuración de apache
	
	sudo nano /etc/apache2/apache2.conf

![Foto 16](/Proyecto/FotosDeComands/ParteApache/Foto16.png)
<h6>Foto 16</h6>

Preguntamos la ip

	ip a

![Foto 18](/Proyecto/FotosDeComands/ParteApache/Foto18.png)

<h6>Foto 18</h6>

Instalamos WordPress con wget

	wget https://wordpress.org/latest.zip

![Foto 19](/Proyecto/FotosDeComands/ParteApache/Foto19.png)

<h6>Foto 19</h6>

Movemos zip que se ha descargado a la carpeta /etc/www/html 

	sudo mv latest.zip /var/www/html

![Foto 20](/Proyecto/FotosDeComands/ParteApache/Foto20.png)

<h6>Foto 20</h6>

Nos movemos al archivo

	cd /var/www/html/

Vemos si hemos movido todo bien

	ls

 ![Foto 21](/Proyecto/FotosDeComands/ParteApache/Foto21.png)
 
<h6>Foto 21</h6>

Tras comprobar que está ahí lo vamos a descomprimir

	sudo unzip latest.zip

![Foto 22](/Proyecto/FotosDeComands/ParteApache/Foto22.png)

<h6>Foto 22</h6>

Movemos todo lo de la carpeta "wordpress" a la carpeta

	sudo mv -f wordpress/* centro.intranet/

Ahora  para acceder introducimos la IP/centro.intranet

![Foto 23](/Proyecto/FotosDeComands/ParteApache/Foto23.png)

<h6>Foto 23</h6>

<br><br>

<h2>PYTHON</h2>


Activamos el ‘wsgi’

	sudo apt-get install libapache2-mod-wsgi-py3

![Foto 1](/Proyecto/FotosDeComands/PartePython/Foto1.png)

<h6>Foto 1</h6>

Creamos las carpetas necesarias para la estructura de python

	sudo mkdir /var/www/html/departamentos.centro.intranet/appython
	sudo mkdir /var/www/html/departamentos.centro.intranet/appython/logs
	sudo mkdir /var/www/html/departamentos.centro.intranet/public-html

 ![Foto 2](/Proyecto/FotosDeComands/PartePython/Foto2.png)

<h6>Foto 2</h6>

Creamos un archivo dentro de aptpython que será el controlador añadiendole lo escrito en el comando y entramos dentro de la carpeta:

	cd /var/www/html
 ![Foto 3](/Proyecto/FotosDeComands/PartePython/Foto3.png)
<h6>Foto 3</h6>

	sudo su

![Foto 4](/Proyecto/FotosDeComands/PartePython/Foto4.png)

<h6>Foto 4</h6>

<h6>Estan separado porque erre de comando y puse “sdo su” pero lo arregle</h6>

Creamos el archivo del controlador
	
 	sudo nano /var/www/html/departamentos.centro.intranet/appython/app.py
  
![Foto 6](/Proyecto/FotosDeComands/PartePython/Foto6.png)
<h6>Foto 6</h6>

Dentro del archivo añadimos

	def application(environ, start_response):
	    output = "<p>Hola</p>"
	    start_response('200 OK', [('Content-Type', 'text/html; charset=utf-8')])
	    return [output.encode('utf-8')]

Hacemos ctrl+O (guardar), enter ( confirmar) y ctrl+X (salir del editor)

 ![Foto 5](/Proyecto/FotosDeComands/PartePython/Foto5.png)
 
<h6>Foto 5</h6>
     
Editamos un nuevo archivo en la ruta especificada, le añadimos lo que se ve en el archivo
	  
    sudo nano /etc/apache2/sites-available/python-web.conf

![Foto 7](/Proyecto/FotosDeComands/PartePython/Foto7.png)

<h6>Foto 7</h6>

Añadimos dentro del archivo:

![Foto 8](/Proyecto/FotosDeComands/PartePython/Foto8.png)
 
<h6>Foto 8</h6>

Hacemos ctrl+O (guardar), enter ( confirmar) y ctrl+X (salir del editor)


Me aseguro los permisos

	sudo chmod 755 /var/www/html/departamentos.centro.intranet/appython/app.py

![Foto 9](/Proyecto/FotosDeComands/PartePython/Foto9.png)
 
<h6>Foto 9</h6>

Activamos el sitio web 

    sudo a2ensite python-web

![Foto 10](/Proyecto/FotosDeComands/PartePython/Foto10.png)

<h6>Foto 10</h6>
    
Reiniciamos apache	

	sudo a2ensite python-web
	systemctl reload apache2

![Foto 11](/Proyecto/FotosDeComands/PartePython/Foto11.png)

<h6>Foto 11</h6>


Editamos el hosts y le añadimoslas direcciones

	sudo nano /etc/hosts

![Foto 13](/Proyecto/FotosDeComands/PartePython/Foto13.png)

<h6>Foto 13</h6>

![Foto 12](/Proyecto/FotosDeComands/PartePython/Foto12.png)

<h6>Foto 12</h6>

Creamos el script de python que será lo que se verá en la web

	sudo nano /var/www/html/departamentos.centro.intranet/public_html/index.py

![Foto 14](/Proyecto/FotosDeComands/PartePython/Foto14.png)

<h6>Foto 14</h6>
