# Imagen base mínima de Python
FROM python:3.9-slim

# Crea un usuario y grupo no privilegiado para ejecutar el contenedor
RUN groupadd --gid 1001 devgroup && \
    useradd --uid 1001 --gid devgroup --shell /bin/bash --create-home devuser

# Establece el directorio de trabajo
WORKDIR /workspace

# Copia el archivo de dependencias e instálalo
COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Copia el código del microservicio
COPY . .

# Expone el puerto en el que se ejecuta Flask
EXPOSE 5000

# Cambia al usuario no root para mayor seguridad
USER devuser

# Define el comando de inicio
CMD ["python", "app.py"]

