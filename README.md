# Proceso de Resolución de la Prueba Técnica de Craftech

## Prueba 1

Para hacer este diagrama acorde a los requisitos solicitados decidí utilizar la plataforma **Cacoo** de Nulabs, que tiene muchos iconos para los servicios de AWS. No sé si serán los más actuales, pero se ven bastante bien.

![Diagrama de Arquitectura](image.png)

Comencé la solución colocando los distintos grupos:

- **AWS Cloud**
- **VPC**
- **Región:** Decidí utilizar solo una región por ahora.
- **Availability Zones:** Utilicé dos para garantizar **alta disponibilidad (HA)**.
- **Subnets:** Seis en total (4 privadas y 2 públicas), replicando una arquitectura de **tres capas** espejada para HA.
- **Servicios Globales:**
  - **CloudFront** como CDN, conectado a S3 dentro de las subredes públicas para servir la aplicación web estática (**Static Web Hosting**).
  - **Route53** como DNS para redirigir tráfico.
- **Balanceo de carga:** Utilicé **ELB**, aunque también consideré **ALB**, pero no encontré el icono.
- **Capa de Aplicaciones:**
  - Instancias **EC2** para el backend.
  - **IAM** para el manejo de usuarios.
  - **Auto-Scaling Group** para garantizar **escalabilidad**.
- **Capa de Persistencia:**
  - **RDS** como base de datos relacional.
  - **MongoDB Atlas** como base de datos NoSQL, conectada a través de **Private Link**.
- **Microservicios Externos:** Añadí dos, aunque no estaban especificados, los conecté a la capa de Aplicación para cumplir con el requisito.

---

## Prueba 2

Para esta prueba, organicé los archivos y configuraciones adecuadamente:

1. **Ubicación de archivos:**
   - `docker-compose.yml` en la raíz del proyecto.
   - `Dockerfile` en cada servicio correspondiente (`frontend/` y `backend/`).
2. **Modificaciones:**
   - **Frontend:** Revisé la configuración y agregué el archivo de configuración de **nginx** para servir la aplicación.
   - **Backend:**
     - Revisé la ubicación de `.env.postgres`.
     - Modifiqué el nombre de `requeriments.txt` (corrección de typo).
     - Añadí **Gunicorn** a los requerimientos para servir Django correctamente.
   - **Base de datos:** Eliminé su `docker-compose` duplicado y consolidé todo en el archivo raíz.

### **Dockerfile - Frontend**

- Utiliza una imagen de **Node.js**.
- Ejecuta el proceso de build de la aplicación React.
- Copia y configura **nginx** para servir la aplicación.

### **Dockerfile - Backend**

- Utiliza una imagen de **Python**.
- Copia el código de la API Django dentro de la imagen.

### **docker-compose.yml (Raíz)**

- **Servicios:**
  - `django_backend` en el puerto `8000:8000`
  - `react_frontend` en el puerto `3000:80` (usando nginx)
  - `postgres_db` en el puerto `5432:5432`

---

## Prueba 3

Para esta prueba, implementé un **pipeline en GitHub Actions**.

### **Pasos Implementados:**

1. **Creación de la carpeta** `.github/workflows/` en la raíz del repositorio.
2. **Configuración del pipeline** en `docker-pipeline.yml`.
3. **Disparador:**
   - Se ejecuta cuando hay modificaciones en `prueba3-craftech/index.html`.
   - Solo corre en la rama `master`.
4. **Fases del pipeline:**
   - **Linting & Code Check**
   - **Build de la imagen Docker**
   - **Login en DockerHub** (usando secrets configurados en GitHub)
   - **Push de la imagen a DockerHub**

Con esto, cada vez que se actualice el `index.html`, el pipeline **compilará la imagen y la subirá a DockerHub automáticamente**.