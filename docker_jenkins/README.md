Instalación de Jenkins

Instalación Standard
Para instalar Jenkins en un contenedor de Docker necesitaremos ejecutar los comandos en consola:

$ docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk11

Instalación Personalizada
Lo recomendable es utilizar el dockerfile y construir la imágen para posteriormente crear el contenedor, ya que para las pruebas de angular necesitaremos una instalación de Chrome y con el dockerfile solucionamos el problema, los comandos son:

$ docker build -t jenkins-chrome .

# Debes agregar el usuario a grupo de docker con el siguiente comando: sudo usermod -aG docker {user}
# Para que los cambios surtan efecto ejecutar el siguiente comando: newgrp docker
# Generalmente se agrega el usuario root como en el ejemplo, pero puedes utilizar otro usuario.

# El primer inicio se ejecuta con la siguiente sentencia para que nos muestre el password de Jenkins
$ docker run -u root -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock --restart unless-stopped jenkins-chrome:latest


$ docker run -u root -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -d --restart unless-stopped jenkins-chrome:latest
