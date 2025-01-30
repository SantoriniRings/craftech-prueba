# Deploy Local de una Aplicación Django-React con Docker

Este documento explica cómo instalar y ejecutar en local un entorno dockerizado que incluye un backend en Django y un frontend en React.

## Requisitos previos

Antes de comenzar, asegúrate de tener instalados los siguientes programas:

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

 Opcional
 
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) 

## Instalación y ejecución

### 1. Clonar el repositorio

```bash
   git clone https://github.com/SantoriniRings/craftech-prueba.git
   cd craftech-prueba
```

### 2. Configurar variables de entorno

Obten las variales de entorno (a fines de simplificar el ejemplo la env.postgres no fueron ignoradas en git a propósito)

### 3. Construir y levantar los contenedores

Ejecuta el siguiente comando para construir y levantar los contenedores:

```bash
docker-compose up --build
```

Esto iniciará los siguientes servicios:
- **PostgreSQL** (Base de datos)
- **Django Backend** (API REST)
- **React Frontend** (Interfaz de usuario)

### 4. Acceder a la aplicación

Una vez que los contenedores estén en ejecución, puedes acceder a:
- **Backend Django (API):** [http://localhost:8000](http://localhost:8000)
- **Frontend React:** [http://localhost:3000](http://localhost:3000)

## Comandos útiles

### Detener los contenedores
```bash
docker-compose down
```

### Ver logs de un servicio en tiempo real
```bash
docker-compose logs -f django_backend
```

### Reconstruir los contenedores
```bash
docker-compose up --build --force-recreate
```

## Resolución de problemas

Si encuentras problemas al iniciar los contenedores, intenta lo siguiente:
- Asegúrate de que Docker y Docker Compose están instalados correctamente.
- Verifica que las variables de entorno estén configuradas correctamente.
- Revisa los logs con `docker-compose logs -f` para encontrar posibles errores.

Si el problema persiste, crea un issue en el repositorio con la descripción del error.

---



