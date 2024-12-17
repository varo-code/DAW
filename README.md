# DAW

Configurando los dominios, agregando los dominios de epartamentos.centro.intranet y centro.intranet

sudo mkdir /var/www/html/centro.intranet
sudo mkdir /var/www/html/departamentos.centro.intranet

Para hacer el sudo nos pide la contraseña para loguearse como superusuario

APACHE

Instalamos el servidor web apache. 

sudo apt install apache2

Usaremos dos dominios mediante el archivo hosts: centro.intranet y departamentos.centro.intranet. El primero servirá el contenido mediante wordpress y el segundo una aplicación en python

Para instalar Wordpress primero necesitamos instalar php, con el siguiente comando instalamos php y sus extensiones

sudo apt install php libapache2-mod-php php-mysql \
php-curl php-gd php-xml php-mbstring php-zip php-soap php-intl -y
sudo apt install mysql-server -y

creamos un archivo php dentro de una carpeta 

	/var/www/html/centro.intranet/index.php

Ahora instalamos mysql 

sudo apt install mysql-server

Establecemos la contraseña para el usuario root, que será 'Hola123%

	alter user root '@' localhost identified with mysql_native_password by 'Hola123%'

Creamos una base de datos

Create database ProyecTri Default Character set utf8 COLLATE  utf8_unicode_ci;

Creamos un usuario para que pueda usar la base de datos

	Grant all ON ProyecTri.* to ‘Usuario’@’localhost’ identified by 'Hola123%'

Salimos de la base

	mysql> exit
Añadimos estas líneas

<Directory /var/www/html/centro.intranet>
	AllowOverride All
</Directory>

Activamos el módulo rewrite y reiniciamos apache 

sudo a2enmod rewrite

Modificamos el archivo de configuración de apache
	
	sudo nano /etc/apache2/apache2.conf

Preguntamos la ip

ip a

Instalamos WordPress con wget

wget https://wordpress.org/latest.zip

Movemos zip que se ha descargado a la carpeta /etc/www/html 

sudo mv latest.zip /var/www/html

Nos movemos al archivo

cd /var/www/html/

Vemos si hemos movido todo bien

	ls

Tras comprobar que está ahí lo vamos a descomprimir

sudo unzip latest.zip

Movemos todo lo de la carpeta "wordpress" a la carpeta

sudo mv -f wordpress/* centro.intranet/

Ahora  para acceder introducimos la IP/centro.intranet


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
