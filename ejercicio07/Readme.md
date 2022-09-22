Para este ejercicio necesitas docker-compose, si estas usando Docker Desktop ya lo tienes instalado, sino deberás instalarlo aparte.Crea un archivo llamado "docker-compose.yml" y pon dentro el contenido de este link: https://gitlab.com/-/snippets/2376003/raw/main/docker-compose.yml.
A continuación ejecuta este comando en una terminal: docker-compose up.
Espera unos minutos hasta que dejen de aparecer mensaje en la terminal. Luego navega localhost:3000 para verificar que la aplicación levantó correctamente.
Finalmente contesta:
1. ¿Cuántos contenedores se están ejecutando? (pueden verlo en el archivo docker-compose.yml y también ejecutando docker ps)
2. ¿Cuales son las imágenes en las que están basados los mencionados contenedores?
3. ¿Puedes leer el docker-compose.yml y describir lo que hace cada una de sus lineas?
4. Dado que cada contenedor corre en forma aislada ¿Cómo es posible que esos contenedores se vean entre sí?


Escribe tus respuestas ejercicio07/README.md en tu repositorio github y entrega el link directo al archivo.

1. **¿Cuántos contenedores se están ejecutando?**
Se están ejecutando 2 contenedores, que se pueden apreciar cuando se ejecuta "docker ps" y también a partir del .yml, pues hay solo dos services.

2. **¿Cuales son las imágenes en las que están basados los mencionados contenedores?**
La imágenes de dos contenedores están especificadas en el docker-compose y son fácilmente identificables porque se encuentran en la etiqueta "image", por lo tanto son: "nicopaez/jobvacancy-ruby:1.3.0"  y  "postgres:14.4-alpine"

3. **¿Puedes leer el docker-compose.yml y describir lo que hace cada una de sus lineas?**
Descripción del archivo docker-compose-yml

1. Se define la version de docker-compose que se está utilizando
version: '2'

2. Se especifican los servicios que se van a ejecutar, es decir, los contenedores que se van a ejecutar
services:

3. Se define el nombre de cada uno de las aplicaciones que se pueden ver con "docker-compose ps", los nombres toman por prefijo el nombre de la carpeta y sufijo el nombre del proceso
  web:
    4. Se define la imagen a usar para construir el container
    image: nicopaez/jobvacancy-ruby:1.3.0
    
    links:
      - db

    5. Se hace el port bind
    ports:
      - "3000:3000"

    6. Se define la conexion con la db con sus variables de entorno
    environment:
      PORT: "3000"
      RACK_ENV: "production"
      DATABASE_URL: "postgres://postgres:Passw0rd!@db:5432/postgres"
    
    7. Se define la dependencia que tiene la app de la ejecucion del contenedor de db
    depends_on:
      - db

  8. Se crea el contenedor de db, con el nombre y las propiedades especificados, similar al punto 4 y 6
  db:
    image: postgres:14.4-alpine
    environment:
      POSTGRES_PASSWORD: Passw0rd!

4. **Dado que cada contenedor corre en forma aislada ¿Cómo es posible que esos contenedores se vean entre sí?**
Los contenedores se ven entre si porque con docker-compose se crea una red interna que permite comunicarse a los servicios. A partir de un dns server que tiene docker, se le asigna un ip a cada servicio y así estos pueden comunicarse entre ellos.