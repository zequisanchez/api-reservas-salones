# 🎉 API de Reservas de Salones de Cumpleaños

API REST para gestionar reservas de salones de cumpleaños: salones, turnos, servicios adicionales, usuarios con roles, informes en PDF/CSV, notificaciones por mail y un dashboard de estadísticas.

Es el **Trabajo Final Integrador de Programación III** (2025, 2.º cuatrimestre) de la Tecnicatura Universitaria en Desarrollo Web (UNER). Lo desarrollé **en equipo** con otros tres compañeros.

> 📌 Esta es una copia en mi cuenta personal del repositorio original del grupo: [PROG3-AL/grupo-AL](https://github.com/PROG3-AL/grupo-AL). El historial de commits completo está incluido.

---

## 🛠️ Tecnologías

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express_5-000000?style=flat&logo=express&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat&logo=mysql&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=flat&logo=jsonwebtokens&logoColor=white)
![Swagger](https://img.shields.io/badge/Swagger-85EA2D?style=flat&logo=swagger&logoColor=black)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)

- **Node.js + Express 5**, con ES Modules
- **MySQL** (`mysql2`) con procedimientos almacenados para las estadísticas
- **Passport + JWT** para la autenticación
- **express-validator** para validar los datos de entrada
- **Swagger** (`swagger-jsdoc` + `swagger-ui-express`) para la documentación
- **Nodemailer** para las notificaciones por correo
- **Puppeteer + Handlebars** para los informes en PDF, y **csv-writer** para los CSV
- **apicache** para el caché de respuestas, **Morgan** para los logs
- **HTML, CSS y JavaScript** para el dashboard de estadísticas

## ✨ Funcionalidades

- **Arquitectura en capas:** rutas → middlewares → controladores → servicios → capa de datos.
- **Autenticación con JWT** y **autorización por roles**:
  - **Administrador:** acceso total, informes y estadísticas.
  - **Empleado:** gestión operativa; ve solo el listado de clientes.
  - **Cliente:** crea y consulta sus propias reservas.
- **CRUD completo** de salones, turnos, servicios, usuarios y reservas, con borrado lógico y reactivación.
- **Contraseñas cifradas** con SHA-2.
- **Notificaciones por mail** al crear una reserva, con copia oculta (CCO) a los administradores.
- **Informes descargables** de reservas en **PDF** y **CSV**.
- **Dashboard de estadísticas**: salones más reservados, servicios más solicitados y turnos más elegidos.
- **API versionada** (`/api/v1`) y documentada con Swagger.

## 🔗 Endpoints principales

| Recurso | Ruta base |
|---|---|
| Usuarios y login | `/api/v1/usuarios` (`POST /login`) |
| Salones | `/api/v1/salones` |
| Turnos | `/api/v1/turnos` |
| Servicios | `/api/v1/servicios` |
| Reservas e informe | `/api/v1/reservas` (`GET /informe`) |
| Estadísticas | `/api/v1/estadisticas` |
| Documentación | `/api-docs` |
| Dashboard | `/dashboard.html` |

## 🙋‍♂️ Mi aporte

Participé en todo el proyecto. Me encargué principalmente de:

- La **documentación Swagger** de la API (usuarios, estadísticas y el resto de los recursos).
- El módulo de **usuarios**: cifrado de contraseñas y permisos por rol.
- El **envío de mails** de confirmación de reservas, con CCO a administradores.
- El **listado de reservas** según el rol del usuario (los clientes solo ven las suyas).
- La implementación del **caché** con apicache y la separación entre `servidor.js` y `reservas.js`.
- Las **pruebas de endpoints** con la colección de **Bruno**, y el **README** del proyecto.

## 👥 Equipo

- **Andrés Labra**
- **Demian Diak**
- **Ezequiel Sánchez**: [GitHub](https://github.com/zequisanchez) · [LinkedIn](https://www.linkedin.com/in/ezequieleduardosanchez)
- **Micaela Ortiz**

---

## 📋 Instalación

### Requisitos
- Node.js 18 o superior
- MySQL 8

### 1. Clonar e instalar dependencias
```bash
git clone https://github.com/zequisanchez/api-reservas-salones.git
cd api-reservas-salones/TFI-GrupoAL
npm install
```

### 2. Base de datos
Crear un usuario de MySQL con permisos sobre la base `reservas`:
```sql
CREATE USER 'tu_usuario_mysql'@'localhost' IDENTIFIED BY 'tu_password_mysql';
GRANT ALL PRIVILEGES ON reservas.* TO 'tu_usuario_mysql'@'localhost';
FLUSH PRIVILEGES;
```
Después, importar los procedimientos almacenados de `TFI-GrupoAL/src/scripts/estadisticasProcedAlma.sql`.

### 3. Variables de entorno
Copiar `.env.example` como `.env` dentro de `TFI-GrupoAL/` y completar los datos:
```env
PORT=3000
DB_HOST=localhost
DB_USER=tu_usuario_mysql
DB_PASSWORD=tu_password_mysql
DB_NAME=reservas
EMAIL_USER=tu_correo@gmail.com
EMAIL_PASS=tu_contraseña_de_aplicacion
CLAVE_JWT=una_clave_secreta_larga
```
> Para `EMAIL_PASS` hay que usar una [contraseña de aplicación de Google](https://myaccount.google.com/apppasswords), no la contraseña común de la cuenta.

### 4. Iniciar el servidor
```bash
npm run dev     # desarrollo, se reinicia solo con cada cambio
npm start       # producción
```

La API queda en `http://localhost:3000`, la documentación en `http://localhost:3000/api-docs` y el dashboard en `http://localhost:3000/dashboard.html`.
