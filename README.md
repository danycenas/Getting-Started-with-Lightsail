La siguiente guia nos permitirá implementar un servidor Linux con tomcat 8.5.37 y mysql para el despliegue de las aplicaciones.

# Requisitos

- Conocimientos básicos en linux
- Una cuenta AWS

# Empezemos

Seleccionar la plataforma Linux/Unix, asimismo elegir la distribución Debian 9.5.

![picture](https://danycenas.github.io/getting-started-with-lightsail/img/create-intance.png)

Para empezar con la instalación es necesario actualizar la lista de paquetes disponibles a la última versión. (Ojo este comando no instala nada)
```bash
sudo apt-get update
```

**Configurar Zona Horaria**
```bash
sudo timedatectl set-timezone America/Lima
```

**Instalar unzip**, necesario para poder descomprimir.
```bash
sudo apt-get install -y unzip
```

**Instalar openjdk 8**, para otras versiones revisar la [documentación](https://openjdk.java.net/install/).
```bash
sudo apt-get install -y openjdk-8-jdk
```

Verificar la versión de openjdk instalada.
```bash
admin@ip-172-26-16-177:~$ java -version
openjdk version "1.8.0_181"
OpenJDK Runtime Environment (build 1.8.0_181-8u181-b13-2~deb9u1-b13)
OpenJDK 64-Bit Server VM (build 25.181-b13, mixed mode)
admin@ip-172-26-16-177:~$ javac -version
javac 1.8.0_181
```

**Instalar apache-tomcat-8.5.x**

Crear un usuario tomcat
La ejecución de Tomcat como usuario root es un riesgo de seguridad y no se recomienda.  
Para crear un nuevo usuario y grupo del sistema para nuestra instancia de Tomcat con el directorio de inicio de /opt/tomcat, ejecutar el siguiente comando:
```bash
sudo useradd -m -U -d /opt/tomcat -s /bin/false tomcat
```

Descargar [tomcat-8.5.X](https://archive.apache.org/dist/tomcat/tomcat-8/).
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

Para tener más control sobre las versiones y actualizaciones de Tomcat, crear un enlace llamado latest que apunte al directorio de instalación de Tomcat:
```bash
sudo ln -s /opt/tomcat/apache-tomcat-8.5.37 /opt/tomcat/latest
```

Más adelante, cuando vaya a actualizar la versión de Tomcat, puede simplemente descomprimir la versión más reciente y cambiar el enlace para que apunte a la última versión.  
Cambie la propiedad del directorio /opt/tomcat a user y group tomcat para que el usuario pueda tener acceso a la instalación de tomcat:
```bash
sudo chown -R tomcat: /opt/tomcat
```

también es necesario hacer ejecutables los scripts del directorio bin:
```bash
sudo chmod +x /opt/tomcat/latest/bin/*.sh
```

Crear un archivo systemd con el siguiente contenido:

```bash
sudo vim /etc/systemd/system/tomcat.service
```

```bash
[Unit]
Description=Tomcat 8.5 servlet container
After=network.target

[Service]
Type=forking

User=tomcat
Group=tomcat

Environment="JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64"
Environment="JAVA_OPTS=-Djava.security.egd=file:///dev/urandom"

Environment="CATALINA_BASE=/opt/tomcat/latest"
Environment="CATALINA_HOME=/opt/tomcat/latest"
Environment="CATALINA_PID=/opt/tomcat/latest/temp/tomcat.pid"
Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"

ExecStart=/opt/tomcat/latest/bin/startup.sh
ExecStop=/opt/tomcat/latest/bin/shutdown.sh

[Install]
WantedBy=multi-user.target
```

Notifique al systemd de un nuevo archivo de unidad e inicie el servicio Tomcat ejecutando:
```bash
sudo systemctl daemon-reload
sudo systemctl start tomcat
```

Verificar el estado del servicio de Tomcat:
```bash
sudo systemctl status tomcat
```
