# Proyecto de Microservicio Flask con Docker y Docker Compose

Este proyecto implementa un entorno de desarrollo seguro y reproducible utilizando Docker, Docker Compose y VS Code Remote Containers. Incluye:
- Un microservicio desarrollado en Flask.
- Una base de datos PostgreSQL.
- Configuración para entornos de desarrollo remotos con VS Code.

## Estructura del Proyecto
El entorno se compone de:
- **Contenedor de Desarrollo:** Configurado a partir de un `Dockerfile` optimizado y seguro.
- **VS Code Remote Containers:** Configura el entorno de desarrollo remoto usando el archivo `.devcontainer.json`.
- **Microservicios:** El entorno puede incluir múltiples contenedores para simular la red de microservicios (por ejemplo, Microservicio 1, Microservicio 2 y una Base de Datos), orquestados mediante Docker Compose.
- **Seguridad de Red:** Los contenedores estarán configurados para exponer únicamente los puertos necesarios y trabajar en redes aisladas.

## 5. Implementación Paso a Paso

### 5.1. Configuración Inicial

1. **Instalar Docker y Docker Compose:**
    
    - Guía de instalación de Docker
    - Verifica la instalación:
		docker --version
		docker-compose --version
2. **Instalar Visual Studio Code y la Extensión Remote - Containers:**

	- Descarga VS Code: [Visual Studio Code](https://code.visualstudio.com/)
	- Instala la extensión **Remote - Containers** desde el Marketplace de VS Code.

### 5.2. Creación del Dockerfile Seguro

Crea un archivo llamado `Dockerfile` en la raíz del proyecto con el siguiente contenido:

### 5.3. Configuración de VS Code Remote Containers

Crea el archivo `.devcontainer/devcontainer.json` en el directorio raíz del proyecto:

### Configuración con Docker Compose

Si el entorno requiere múltiples contenedores para simular una red de microservicios, crea un archivo `docker-compose.yml`:

### 5.5. Ejecución y Verificación

### **Construir y Ejecutar el Contenedor de Desarrollo:**
```bash
docker build -t liox-dev .
docker run -d --name liox-dev-container -p 5000:5000 liox-dev
```

### **Abrir el Proyecto en VS Code:**

- Abre VS Code y selecciona la opción **"Reopen in Container"** para cargar el entorno definido.
```bash
whoami
```
### **Validar Conexiones entre Microservicios:**

- Desde el contenedor de desarrollo, realiza peticiones HTTP o utiliza herramientas de línea de comandos (como `curl`) para verificar la comunicación entre microservicios y la base de datos.

# Flujo de Incorporación y Consumo del Entorno de Desarrollo

La implementación presentada permite que un nuevo desarrollador se integre de forma rápida y sin discrepancias en el entorno de desarrollo. A continuación se detalla el flujo y el proceso:

---

## 1. Clonación del Repositorio

- **Acción:**  
  El nuevo desarrollador clona el repositorio del proyecto que contiene:
  - El código fuente.
  - El `Dockerfile` y, si se utiliza, el `docker-compose.yml`.
  - La carpeta `.devcontainer` con el archivo `devcontainer.json`.

- **Resultado:**  
  Se obtiene una copia local con todas las configuraciones necesarias para construir el entorno.

---

## 2. Instalación de Herramientas Requeridas

- **Herramientas a Instalar:**
  - **Docker:** (versión 20.10.x o superior).
  - **Docker Compose:** (si el entorno usa múltiples contenedores).
  - **Visual Studio Code:** Con la extensión **Remote - Containers** instalada.

- **Resultado:**  
  El desarrollador dispone de todas las herramientas necesarias para crear y acceder al entorno de desarrollo remoto.

- **Fuente:**  
  [VS Code Remote Containers](https://code.visualstudio.com/docs/remote/containers) :contentReference[oaicite:0]{index=0}

---

## 3. Carga del Entorno de Desarrollo

- **Acción en VS Code:**
  1. **Abrir el Proyecto:**  
     El desarrollador abre el directorio del proyecto en VS Code.
  2. **Detección del Archivo `.devcontainer`:**  
     VS Code reconoce la carpeta `.devcontainer` y su configuración.
  3. **Reapertura en Contenedor:**  
     VS Code solicita “Reopen in Container” (Reabrir en contenedor). Al aceptarlo:
     - Se construye la imagen utilizando el `Dockerfile` especificado.
     - Se ejecutan comandos definidos en `postCreateCommand` (por ejemplo, la instalación de dependencias mediante `pip`).
     - Se configura el entorno de desarrollo remoto, montando volúmenes y, de ser necesario, levantando servicios adicionales mediante Docker Compose.

- **Resultado:**  
  El entorno de desarrollo se carga dentro de un contenedor Docker. VS Code se conecta a ese contenedor, proporcionando una experiencia integrada en la que el terminal, depurador y demás herramientas funcionan dentro del mismo entorno controlado.

---

## 4. Consumo del Ambiente de Desarrollo

- **Interacción del Desarrollador:**
  - **Terminal y Shell:**  
    El desarrollador utiliza el terminal integrado (configurado para usar Bash) para ejecutar comandos, correr scripts o interactuar con el sistema.
  - **Ejecución y Depuración:**  
    La aplicación se ejecuta dentro del contenedor, lo que permite realizar depuraciones y pruebas en un entorno idéntico al de producción (o testing).
  - **Uso de Extensiones y Herramientas:**  
    Las extensiones preconfiguradas (por ejemplo, para Python, Docker, ESLint y Prettier) están disponibles, asegurando que se sigan los estándares de codificación y buenas prácticas.

- **Beneficios:**
  - **Consistencia:**  
    Todos los desarrolladores trabajan con el mismo entorno, eliminando conflictos de dependencias o configuraciones locales.
  - **Seguridad:**  
    La configuración del contenedor, con usuario no privilegiado y prácticas de seguridad, minimiza riesgos.
  - **Escalabilidad:**  
    La misma configuración se puede replicar en pipelines CI/CD y en otros entornos (como testing o producción).

- **Fuente:**  
  [Documentación de Docker y VS Code Remote Containers](https://docs.docker.com/engine/reference/builder/) :contentReference[oaicite:1]{index=1}

---

# Flujo Resumido del Proceso de Implementación

A continuación se presenta un paso a paso que integra la implementación inicial y la incorporación del nuevo microservicio (en este caso, el microservicio Flask):

1. **Clonar el Repositorio:**  
   El desarrollador clona el repositorio que contiene la configuración del entorno (Dockerfile, `.devcontainer/devcontainer.json`, `docker-compose.yml`) y el código del microservicio.

2. **Instalar Herramientas Requeridas:**  
   Se aseguran tener instalados Docker, Docker Compose y Visual Studio Code con la extensión _Remote - Containers_.

3. **Abrir el Proyecto en VS Code:**  
   Al abrir el directorio del proyecto, VS Code detecta la carpeta `.devcontainer` y propone la opción "Reopen in Container".

4. **Construir y Levantar el Entorno:**  
   - VS Code utiliza el `Dockerfile` para construir la imagen base del entorno.
   - Si se usa Docker Compose, se orquestan múltiples contenedores (por ejemplo, el microservicio Flask y una base de datos).
   - Se ejecuta el comando `postCreateCommand` para instalar las dependencias definidas.

5. **Ejecución del Microservicio:**  
   El microservicio Flask se inicia dentro de su contenedor, exponiendo el puerto configurado (por ejemplo, 5000).

6. **Interacción del Desarrollador:**  
   El desarrollador utiliza el entorno remoto para:
   - Ejecutar y depurar el microservicio.
   - Interactuar con el terminal integrado y utilizar las extensiones preconfiguradas.
   - Realizar pruebas y validar la comunicación entre servicios (si existen otros microservicios o bases de datos).
