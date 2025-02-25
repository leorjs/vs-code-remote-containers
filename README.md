# Proyecto de Microservicio Flask con Docker y Docker Compose

Este proyecto implementa un entorno de desarrollo seguro y reproducible utilizando Docker, Docker Compose y VS Code Remote Containers. El entorno incluye:

- **Microservicio Flask:** Una aplicación desarrollada en Flask.
- **Base de Datos PostgreSQL:** Para almacenamiento persistente.
- **Entorno de Desarrollo Remoto:** Configurado con VS Code y Remote Containers.

---

## Tabla de Contenidos

1. [Estructura del Proyecto](#estructura-del-proyecto)
2. [Implementación Paso a Paso](#implementación-paso-a-paso)
   - [Configuración Inicial](#configuración-inicial)
   - [Creación del Dockerfile Seguro](#creación-del-dockerfile-seguro)
   - [Configuración de VS Code Remote Containers](#configuración-de-vs-code-remote-containers)
   - [Configuración con Docker Compose](#configuración-con-docker-compose)
   - [Ejecución y Verificación](#ejecución-y-verificación)
3. [Flujo de Incorporación y Consumo del Entorno](#flujo-de-incorporación-y-consumo-del-entorno)
   - [Clonación del Repositorio](#clonación-del-repositorio)
   - [Instalación de Herramientas Requeridas](#instalación-de-herramientas-requeridas)
   - [Carga del Entorno de Desarrollo](#carga-del-entorno-de-desarrollo)
   - [Consumo del Ambiente de Desarrollo](#consumo-del-ambiente-de-desarrollo)
4. [Flujo Resumido del Proceso de Implementación](#flujo-resumido-del-proceso-de-implementación)

---

## Estructura del Proyecto

El entorno se compone de:

- **Contenedor de Desarrollo:** Configurado a partir de un `Dockerfile` optimizado y seguro.
- **VS Code Remote Containers:** Usa el archivo `.devcontainer/devcontainer.json` para definir el entorno remoto.
- **Microservicios:** Se pueden levantar múltiples contenedores (por ejemplo, Microservicio 1, Microservicio 2 y la Base de Datos), orquestados con Docker Compose.
- **Seguridad de Red:** Los contenedores exponen únicamente los puertos necesarios y operan en redes aisladas.

---

## Implementación Paso a Paso

### Configuración Inicial

1. **Instalar Docker y Docker Compose:**

   - **Guía de instalación de Docker**
   - Verifica la instalación:
     ```bash
     docker --version
     docker-compose --version
     ```

2. **Instalar Visual Studio Code y la Extensión Remote - Containers:**

   - Descarga VS Code en [Visual Studio Code](https://code.visualstudio.com/).
   - Instala la extensión **Remote - Containers** desde el Marketplace de VS Code.

---

### Creación del Dockerfile Seguro (Ya se encuentra en este repo creado)

Crea un archivo llamado `Dockerfile` en la raíz del proyecto con el contenido adecuado para definir tu imagen base y las configuraciones de seguridad necesarias.

---

### Configuración de VS Code Remote Containers (Ya se encuentra en este repo creado)

Crea el archivo `.devcontainer/devcontainer.json` en el directorio raíz del proyecto. Este archivo define cómo se configura el entorno remoto en VS Code.

---

### Configuración con Docker Compose (Ya se encuentra en este repo creado)

Si el entorno requiere múltiples contenedores para simular una red de microservicios, crea un archivo `docker-compose.yml` en la raíz del proyecto para orquestar la comunicación entre ellos.

---

#### Abrir el Proyecto en VS Code

- Abre VS Code y selecciona la opción **"Reopen in Container"** para cargar el entorno definido.
- Verifica la sesión dentro del contenedor:
  
  ```bash
  whoami
  ```

#### Validar Conexiones entre Microservicios

- Desde el contenedor, realiza peticiones HTTP o utiliza herramientas como `curl` para confirmar la comunicación entre microservicios y la base de datos.

---

## Flujo de Incorporación y Consumo del Entorno

La implementación permite que un nuevo desarrollador se integre rápidamente al entorno de desarrollo. A continuación se detalla el proceso:

### Clonación del Repositorio

- **Acción:**  
  Clonar el repositorio que contiene:
  - El código fuente.
  - El `Dockerfile` y, en su caso, el `docker-compose.yml`.
  - La carpeta `.devcontainer` con el archivo `devcontainer.json`.

- **Resultado:**  
  Se obtiene una copia local con todas las configuraciones necesarias.

---

### Carga del Entorno de Desarrollo

1. **Abrir el Proyecto:**
   - Abre el directorio del proyecto en VS Code.
2. **Detección Automática:**
   - VS Code detecta la carpeta `.devcontainer` y su configuración.
3. **Reapertura en Contenedor:**
   - Selecciona “Reopen in Container” para:
     - Construir la imagen a partir del `Dockerfile`.
     - Ejecutar comandos definidos en `postCreateCommand` (por ejemplo, instalación de dependencias con `pip`).
     - Configurar el entorno remoto, montando volúmenes y levantando servicios adicionales mediante Docker Compose si es necesario.

- **Resultado:**  
  El entorno de desarrollo se carga dentro de un contenedor Docker, permitiendo el uso integrado de terminal, depurador y demás herramientas.

---

- **Beneficios:**
  - **Consistencia:**  
    Todos los desarrolladores utilizan el mismo entorno, evitando conflictos de dependencias.
  - **Seguridad:**  
    La configuración del contenedor, con usuario no privilegiado y prácticas de seguridad, minimiza riesgos.
  - **Escalabilidad:**  
    La misma configuración puede replicarse en pipelines CI/CD o en otros entornos (testing, producción).

- **Fuente:**  
  [Documentación de Docker y VS Code Remote Containers](https://docs.docker.com/engine/reference/builder/)

---

## Flujo Resumido del Proceso de Implementación

1. **Clonar el Repositorio:**  
   - Clona el repositorio que contiene la configuración del entorno (Dockerfile, `.devcontainer/devcontainer.json`, `docker-compose.yml`) y el código del microservicio.

2. **Instalar Herramientas Requeridas:**  
   - Asegúrate de tener Docker, Docker Compose y VS Code con la extensión _Remote - Containers_ instalados.

3. **Abrir el Proyecto en VS Code:**  
   - Al abrir el directorio del proyecto, VS Code detectará la carpeta `.devcontainer` y sugerirá “Reopen in Container”.

4. **Construir y Levantar el Entorno:**  
   - VS Code utiliza el `Dockerfile` para construir la imagen base.
   - Si se usa Docker Compose, se orquestan múltiples contenedores (por ejemplo, el microservicio Flask y una base de datos).
   - Se ejecuta el comando `postCreateCommand` para instalar dependencias. (Lo hace de forma automatica)

5. **Ejecución del Microservicio:**  
   - El microservicio Flask se inicia dentro de su contenedor, exponiendo el puerto configurado (por ejemplo, 5000).

6. **Interacción del Desarrollador:**  
   - Utiliza el entorno remoto para ejecutar, depurar y probar el microservicio, asegurando la comunicación correcta entre servicios.
