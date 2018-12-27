La siguiente guia nos permitirá implementar un servidor Linux con tomcat 8.5.37 y mysql para el despliegue de las aplicaciones.

# Requisitos

- Conocimientos básicos en linux
- Una cuenta AWS

# Empezemos

Seleccionar una plataforma Linux/Unix con una distribución Debian 9.5.

![picture](https://danycenas.github.io/Getting-Started-with-Lightsail/img/create-intance.png)

Actualizamos la lista de paquetes disponibles a las últimas versiones. (Ojo este comando no instala nada)

```bash
sudo apt-get update
```
Instalar JDK 8.
```bash
sudo apt-get install -y openjdk-8-jdk
```
Para otras versiones de openjdk revisar la [documentación](https://openjdk.java.net/install/).

Verificar la versión de JDK instalada.
```bash
admin@ip-172-26-15-175:~$ java -version
openjdk version "1.8.0_181"
OpenJDK Runtime Environment (build 1.8.0_181-8u181-b13-2~deb9u1-b13)
OpenJDK 64-Bit Server VM (build 25.181-b13, mixed mode)
admin@ip-172-26-15-175:~$ javac -version
javac 1.8.0_181
```
