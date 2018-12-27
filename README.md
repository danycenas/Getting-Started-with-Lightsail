La siguiente guia nos permitirá implementar un servidor Linux con tomcat 8.5.37 y mysql para el despliegue de las aplicaciones.

# Requisitos

- Conocimientos básicos en linux
- Una cuenta AWS

# Empezemos

Seleccionar una plataforma Linux/Unix con una distribución Debian 9.5.

![picture](https://danycenas.github.io/getting-started-with-lightsail/img/create-intance.png)

Actualizar la lista de paquetes disponibles a las últimas versiones. (Ojo este comando no instala nada)
```bash
sudo apt-get update
```

**Instalar openjdk 8**, para otras versiones revisar la [documentación](https://openjdk.java.net/install/).
```bash
sudo apt-get install -y openjdk-8-jdk
```

Verificar la versión de openjdk instalada.
```bash
admin@ip-172-26-15-175:~$ java -version
openjdk version "1.8.0_181"
OpenJDK Runtime Environment (build 1.8.0_181-8u181-b13-2~deb9u1-b13)
OpenJDK 64-Bit Server VM (build 25.181-b13, mixed mode)
admin@ip-172-26-15-175:~$ javac -version
javac 1.8.0_181
```

**Instalar tomcat 8.5.37**

Crear usuario tomcat
La ejecución de Tomcat como usuario root es un riesgo de seguridad y no se recomienda.
Para crear un nuevo usuario y grupo del sistema para nuestra instancia de Tomcat con el directorio de inicio de /opt/tomcat, ejecutar el siguiente comando:
```bash
sudo useradd -m -U -d /opt/tomcat -s /bin/false tomcat
```

Descargar  [tomcat-8.5.37](https://archive.apache.org/dist/tomcat/tomcat-8/v8.5.37/bin/).
```bash
cd /tmp
wget http://www-us.apache.org/dist/tomcat/tomcat-8/v8.5.37/bin/apache-tomcat-8.5.37.zip
```

Cuando se complete la descarga, ejecute los siguientes comandos para extraer el archivo zip y mover el contenido al directorio /opt/tomcat:
```bash
unzip apache-tomcat-*.zip
sudo mkdir -p /opt/tomcat
sudo mv apache-tomcat-8.5.37 /opt/tomcat/
```
