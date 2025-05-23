# Ejercicio Docker PPS JGA


Este proyecto consiste en la creación de una arquitectura web usando Docker, Docker Compose y Dockerfile. Desenvolviendose en un sistema de tres servicios principales:
	-> Un frontend (HTML servido con Nginx), 
	-> Un backend (API Flask en Python) 
	-> Una base de datos (PostgreSQL) con persistencia

Lo primero es decir como tengo montada la arquitectura de este proyecto

├── docker-compose.yml
├── frontend/
│ └── index.html
├── backend/
│ ├── app.py
│ ├── Dockerfile
│ └── requirements.txt
├── db/
│ └── init.sql
├── README.md
└── url.txt

Primeros pasos del ejercicio:


Parte 1: Git e GitHub

	1. Inicializa un repositorio Git local (git init).
		Comando-> git init 

	2. Crea un repositorio remoto en GitHub e vincúlao.
		Comando-> git remote add origin https://github.com/usuario/nombre-del-repo.git

		En este apartado yo lo hice a través de claves ssh así no tengo que poner credenciales. 
		
		Primero genero claves con ssh-keygen luego en /root/.ssh/ copio la clave pública id_rsa.pub 
		y la pego en el repositorio de Github (Setting / Deploy Keys / y pongo ahí mi clave pública)
	
	3. Crea ramas separadas (frontend, backend) para traballar de forma organizada.

		Comandos:
			git branch frontend-> rama llamada frontend
			git branch backend-> rama llamda backend
			git branch main-> rama llamada main
	
	4. Fai commit dos cambios e realiza merge cara á rama principal.
		Frontent
			1º git checkout frontend

			2º Edito el archivo index.html de frontend para hacerle una pequeña modificación
			
			3º Hago el commit para que guarde los cambios que realicé
		
		Backend
			1º git checkout backend
		
			2º Editamos la appy.py para que tenga un pequeño texto añadido por nosotros

			3º Volvemos hacer el commit para guardar los cambios

		
	5. Sube o proxecto completo a GitHub

	
		1º git push origin frontend 
			
		2º git push origin backend

	


Parte 2: Estrutura do despregue

	Frontend:
		Archivo docker compose donde:
			  No requiere de un Dockerfile propio.
			  Uso directamente la imagen nginx:alpine.
			  Servirá la página index.html mediante un bind mount dende el host.

	Backend
		Archivo docker compose donde.
			Usa un Dockerfile basado en debian:bullseye.
			Instala Python 3 e pip.
			Instala las dependencias de requirements.txt.   
			Lanza la aplicación app.py.
			El código de la app será cargado dinámicamente con un bind mount, sin recompilar la image tras cada cambio.

	BBDD
		Archivo docker compose donde.
			Usa la imagen postgres:15.
			Ejecuta un script SQL de inicialización.
			Usa un volumen para conservar los datos entre sesións.


Parte 3: docker-compose.yml

	Aquí en el directorio principal del ejericio creo un docker compose donde:
		   Defina los tres servicios (frontend, backend, db).
		   Usa bind mounts para montar los directorios ./frontend y ./backend en los contenedores.   
		   Usa un volumen llamado db_data para /var/lib/postgresql/data.
	
	Todo está en el archivo docker compose de la rama main

Parte 4: Execución e probas

	Hacemos un docker compose -f docker-compose.yml up -d para levantar el contenedor principal
	
	y ya podremos acceder a:
		
		http://localhost:8080 → frontend.
		http://localhost:5000 → backend 

