# Usa Debian Bullseye como imagen base
FROM debian:bullseye

# Actualiza e instala Python y pip
RUN apt-get update && apt-get install -y python3 python3-pip

# Crea un directorio de trabajo
WORKDIR /app

# Copia el archivo de dependencias al contenedor
COPY requirements.txt .

# Instala las dependencias de Python
RUN pip3 install -r requirements.txt

# Comando para ejecutar la aplicación al iniciar el contenedor
CMD ["python3", "app.py"]
