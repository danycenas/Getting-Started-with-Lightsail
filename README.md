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
Verificamos si tenemos instalado el JDK.
```bash
java -version
javac -version
```

De no tener instalado, procedemos a instalar con el siguiente comando
```bash
sudo apt-get install -y openjdk-8-jdk
```

Volvemos a validar la versión de JDK instalada
```bash
java -version
javac -version
```
