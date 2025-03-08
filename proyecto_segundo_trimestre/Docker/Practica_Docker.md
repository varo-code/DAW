<h1>Instalación de Docker en Ubuntu</h1>

El primer paso es eliminar cualquier versión anterior de Docker. Como estamos trabajando en una máquina recién creada, es probable que no haya ninguna instalación previa, pero ejecutamos el siguiente comando para asegurarnos:

    sudo apt-get remove docker docker-engine docker.io containerd runc

![Foto 1](Docker_ADP/foto_1.png)

<h3>Actualización del sistema</h3>

Ejecutamos el siguiente comando para actualizar la máquina:

    sudo apt-get update

![Foto 2](Docker_ADP/foto_2.png)

<h3>Instalación de Docker</h3>

Ejecutamos los siguientes comandos para instalar Docker:

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu (lsb_release -cs) stable"

![Foto 3](Docker_ADP/foto_3.png)

Ahora instalamos la última versión de Docker CE:

    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io

![Foto 4](Docker_ADP/foto_4.png)

![Foto 5](Docker_ADP/foto_5.png)

El servicio de Docker se inicia automáticamente después de la instalación y se ejecutará en cada reinicio del sistema. Para comprobar su estado, usamos:

    sudo systemctl status docker 

![Foto 6](Docker_ADP/foto_6.png)


Con esto, Docker está correctamente instalado en Ubuntu.

<h2>Pruebas iniciales con Docker</h2>

<h3>Ejecutar la imagen "hello-world"</h3>

Para verificar que Docker funciona correctamente, ejecutamos:

    sudo docker run hello-world

![Foto 7](Docker_ADP/foto_7.png)

<h3>Mostrar las imágenes de Docker instaladas</h3>

Ejecutamos el siguiente comando para listar las imágenes instaladas:

    sudo docker images

![Foto 8](Docker_ADP/foto_8.png)

<h3>Listar los contenedores de Docker</h3>

Para ver los contenedores en nuestro sistema, incluyendo los detenidos, usamos:

    sudo docker ps -a

![Foto 9](Docker_ADP/foto_9.png)

