
# Imagen Docker personalizada


---
Primero debemos especificar que librerías queremos instalar en nuestra imagen personalizada, para ello debemos crear el fichero [```Dockerfile```](https://github.com/EricBorder/PythonDocker/blob/main/Dockerfile).

```
FROM python:3

WORKDIR /usr/src/app

RUN pip install pytube

COPY ./app /usr/src/app

CMD ["python","miscript.py"]
```
Para crear nuestra propia imagen personalizada de un contenedor de docker debemos ejecutar el comando:


`$ docker build -t youtubeimagen:latest .`

Posteriormente configuramos nuestro [```docker-compose.yml```](https://github.com/EricBorder/PythonDocker/blob/main/docker-compose.yml)

```
services:
  python:
    image: youtubeimagen:latest
    volumes:
      - .:/usr/src/app
    stdin_open: true
    tty: true
    working_dir: /usr/src/app
    command: python main.py 
```
Finalmente para levantar el servicio con nuestra propia imagen:

`$ docker-compose up`


Y ya tendremos nuestro contenedor con el script que hayamos especificado en ejecución en "command: ", en nuestro caso un script de python.

Para subirlo a [DockerHub](https://hub.docker.com/) primeramente debemos ir a nuestro perfil y presionar en "Create repository".

Una vez accedemos al repostiorio, seleccionamos el nombre de nuestro repositorio y presionamos create.

Una vez tenemos todo creado accedemos a nuestro terminal y ejecutamos la sucesión de estos comandos:

`$ docker-login`

`$ docker tag youtubeimagen:latest srmagdalena/youtubeimage:sxe`

`$ docker push srmagdalena/youtubeimage:sxe`

Donde nos autentificamos con nuestra cuenta de docker hub, posteriormente creamos el tag de nuestra imagen y lo vinculamos al repositorio de nuestra cuenta y finalmente realizamos el push del tag creado a nuestra cuenta y con la imagen seleccionada.

Quedando así publicado nuestro repositorio, en mi caso: [```srmagdalena/youtubeimagen```](https://hub.docker.com/repository/docker/srmagdalena/youtubeimage/general)