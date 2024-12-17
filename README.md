Configurando los dominios, agregando los dominios de epartamentos.centro.intranet y centro.intranet

sudo mkdir /var/www/html/centro.intranet

Para hacer el sudo nos pide la contraseña para loguearse como superusuario

Foto 1

sudo mkdir /var/www/html/departamentos.centro.intranet

Foto 2






APACHE

Instalamos el servidor web apache. 

sudo apt install apache2
Foto 3

Usaremos dos dominios mediante el archivo hosts: centro.intranet y departamentos.centro.intranet. El primero servirá el contenido mediante wordpress y el segundo una aplicación en python

Para instalar Wordpress primero necesitamos instalar php, con el siguiente comando instalamos php y sus extensiones

sudo apt install php libapache2-mod-php php-mysql \
php-curl php-gd php-xml php-mbstring php-zip php-soap php-intl -y
sudo apt install mysql-server -y

Foto 4

creamos un archivo php dentro de una carpeta 

	nano /var/www/html/centro.intranet/index.php

Foto 5

Ahora instalamos mysql 

sudo apt install mysql-server

Foto 6

Deténemos el servicio de MySQL

sudo service mysql stop

Foto 9

Me conecto a MySQL sin contraseña

	mysql -u root

Foto 10


Accedemos a la configuración de mysql con

	sudo mysql
Foto 7

Establecemos la contraseña para el usuario root, que será 'Hola123%

	alter user root '@' localhost identified with mysql_native_password by 'Hola123%'

Foto 8

Creamos una base de datos

Create database ProyecTri Default Character set utf8 COLLATE  utf8_unicode_ci;

Foto 11

Creamos un usuario para que pueda usar la base de datos

	Grant all ON ProyecTri.* to ‘Usuario’@’localhost’ identified by 'Hola123%'

Foto 12


Salimos de la base

	mysql> exit

Foto 13

Añadimos estas líneas en:

	sudo cp /etc/apache2/sities-available/000-default.conf /etc/apache2/sities-available/WordPress.conf

Foto 14

<Directory /var/www/html/centro.intranet>
	AllowOverride All
</Directory>

Foto 17

Activamos el módulo rewrite y reiniciamos apache 

sudo a2enmod rewrite

Foto 15

Modificamos el archivo de configuración de apache
	
	sudo nano /etc/apache2/apache2.conf

Foto 16

Preguntamos la ip

ip a

Foto 18
Instalamos WordPress con wget

wget https://wordpress.org/latest.zip

Foto 19

Movemos zip que se ha descargado a la carpeta /etc/www/html 

sudo mv latest.zip /var/www/html

Foto 20

Nos movemos al archivo

cd /var/www/html/

Vemos si hemos movido todo bien

	ls
Foto 21

Tras comprobar que está ahí lo vamos a descomprimir

sudo unzip latest.zip

Foto 22

Movemos todo lo de la carpeta "wordpress" a la carpeta

sudo mv -f wordpress/* centro.intranet/

Ahora  para acceder introducimos la IP/centro.intranet
Foto 23

PYTHON

Activamos el ‘wsgi’

sudo apt-get install libapache2-mod-wsgi-py3

Creamos las carpetas necesarias para la estructura de python

sudo mkdir /var/www/html/departamentos.centro.intranet/aptpython
sudo mkdir /var/www/html/departamentos.centro.intranet/
sudo mkdir /var/www/html/departamentos.centro.intranet/public-html

Creamos un archivo dentro de aptpython que será el controlador añadiendole lo escrito en el comando

	sudo su

Además, le añadimos lo siguiente

def application(envieron, start_response):
	output =”<p>Hola</p>
	start_response(‘200 OK’,[(‘Content-Type’, ‘text/html; charset=utf-8’)])
	return output 

Editamos un nuevo archivo en la ruta especificada, le añadimos lo que se ve en el archivo
	sudo nano /etc/apache2/sites-availables/python-web.conf

Activamos el sitio web 

sudo a2ensite python-web

Reiniciamos apache

systemctl reload apache2

Editamos el archivo hosts y le añadimos ambas direcciones

	sudo nano /etc/hosts

Creamos un script de python que será lo que se verá en la web

	sudo nano /var/www/html/departamentos.centro.intranet/public_html/index.py
