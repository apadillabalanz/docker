###
# Informacion sobre la creacion de imagenes para ejecutar passwordapi.jar

# Primero se descarga el archivo passwordapi.jar a la carpeta con el Dockerfile.
# Luego crea una imagen con un JDK proveniente de https://hub.docker.com/_/eclipse-temurin ,
# el Dockerfile correspondiente es el que dice Dockerfile-JDK (habria que quitar el sufijo "-JDK" para usarlo)

# Renombrando "Dockerfile-JDK -> Dockerfile" se crea la imagen
docker build -t passwordapi:1.0 .

# Ejecutando con un bind al puerto 8080 para obtener la api expuesta
docker run -it --rm -p8080:8080 passwordapi:1.0

# La imagen docker se puede descargar con
docker pull apadillaperez/curso:passwordapi_1.0


# Probando una segunda opcion con JRE, siguiendo los pasos indicados en el mismo sitio
# Renombrando "Dockerfile-JRE -> Dockerfile" se crea la imagen
docker build -t passwordapi:2.0 .
# Nuevamente ejecuntando con un bind al mismo puerto, pero se obtiene un error al ejecutar
docker run -it --rm -p8080:8080 passwordapi:2.0

# Asumo hay que instalar dependencias que no estan en el JRE que se crea con jlink segun la configuracion
# que se muestra en el sitio
###
Exception in thread "main" java.lang.reflect.InvocationTargetException
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(Unknown Source)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(Unknown Source)
        at java.base/java.lang.reflect.Method.invoke(Unknown Source)
        at org.springframework.boot.loader.MainMethodRunner.run(MainMethodRunner.java:48)
        at org.springframework.boot.loader.Launcher.launch(Launcher.java:87)
        at org.springframework.boot.loader.Launcher.launch(Launcher.java:50)
        at org.springframework.boot.loader.JarLauncher.main(JarLauncher.java:51)
Caused by: java.lang.IllegalArgumentException: Cannot instantiate interface org.springframework.context.ApplicationContextInitializer : org.springframework.boot.context.ConfigurationWarningsApplicationContextInitializer
        at org.springframework.boot.SpringApplication.createSpringFactoriesInstances(SpringApplication.java:448)
        at org.springframework.boot.SpringApplication.getSpringFactoriesInstances(SpringApplication.java:427)
        at org.springframework.boot.SpringApplication.getSpringFactoriesInstances(SpringApplication.java:418)
        at org.springframework.boot.SpringApplication.<init>(SpringApplication.java:266)
        at org.springframework.boot.SpringApplication.<init>(SpringApplication.java:247)
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:1255)
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:1243)
        at com.nicopaez.passwordapi.Application.main(Application.java:13)
        ... 8 more
Caused by: java.lang.NoClassDefFoundError: java/sql/SQLException
        at org.springframework.beans.BeanUtils.instantiateClass(BeanUtils.java:168)
        at org.springframework.boot.SpringApplication.createSpringFactoriesInstances(SpringApplication.java:444)
        ... 15 more
Caused by: java.lang.ClassNotFoundException: java.sql.SQLException
        at java.base/java.net.URLClassLoader.findClass(Unknown Source)
        at java.base/java.lang.ClassLoader.loadClass(Unknown Source)
        at org.springframework.boot.loader.LaunchedURLClassLoader.loadClass(LaunchedURLClassLoader.java:93)
        at java.base/java.lang.ClassLoader.loadClass(Unknown Source)
        ... 17 more
###
