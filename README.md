# ¿Qué Comemos? - Buffet Management System 🍱

Este proyecto es una aplicación backend desarrollada en **Java** con **Spring Boot** para la administración integral del buffet de la Facultad de Informática. El sistema permite la gestión de menús, compras de tickets, buzón de sugerencias y estadísticas detalladas.

---

## 🚀 Tecnologías Utilizadas

- **Java 17**
- **Spring Boot 3.3.4**
- **Spring Data JPA** (Hibernate)
- **Spring Security** + **JWT** (JSON Web Tokens)
- **MySQL** (Base de Datos)
- **Lombok** (Reducción de código boilerplate)
- **Jackson** (Mapeo de JSON a DTOs)
- **Docker & Docker Compose** (Contenerización)
- **Maven** (Gestor de dependencias)

---

## 🏗️ Arquitectura del Proyecto

El sistema sigue una **Arquitectura en Capas**, promoviendo el desacoplamiento y la responsabilidad única:

- **Controllers**: Puerta de entrada de la API. Manejan las solicitudes HTTP y delegan la lógica a los servicios.
- **Services**: El "cerebro" del sistema. Contienen la lógica de negocio y validaciones (ej. reglas del buffet).
- **Repositories**: Capa de acceso a datos utilizando Spring Data JPA.
- **Models**: Entidades que representan las tablas en la DB. Se utiliza la estrategia de herencia `@Inheritance(strategy = InheritanceType.JOINED)` para `Product` y `Menu`, asegurando una base de datos normalizada.
- **DTOs (Requests/Responses)**: Objetos para transferir datos de forma segura entre el cliente y el servidor, evitando exponer las entidades reales de la base de datos.
- **Filters**: Interceptores de seguridad (JWT) que validan el token antes de procesar cualquier solicitud.

El sistema cuenta con tres niveles de acceso definidos mediante roles (`Role.java`):

1.  **Administrador General (ADMIN)**: Gestión total de menús, comidas, usuarios y visualización de estadísticas globales.
2.  **Responsable de Turno (RESPONSABLE_TURNO)**: Supervisión de ventas y pagos en su franja horaria, y gestión del buzón de sugerencias.
3.  **Usuario (USUARIO)**: Compra de tickets, actualización de perfil y envío de sugerencias/comentarios.

---

## 📋 Mapeo de Funcionalidades (Especificación vs. Implementación)

A continuación se detalla cómo se resolvieron los requerimientos solicitados en el trabajo final:

### A. Gestión de Perfiles
- **Implementación**: `UserController.java` y `UserService.java`.
- **Detalle**: El usuario puede actualizar su nombre, apellido, email y foto. Los datos se persisten en la entidad `User`.

### B y C. Gestión de Menús y Carta de Comidas
- **Implementación**: `MenuController.java`, `Menu.java`, `ItemMenu.java`.
- **Detalle**: Se permite el CRUD de menús y sus componentes (entrada, plato principal, postre, bebida). Incluye validaciones para evitar modificaciones en menús con ventas activas. Se contemplan opciones vegetarianas y no vegetarianas.

### D. Compra y Tickets
- **Implementación**: `PurchaseController.java`, `Purchase.java`, `PurchaseService.java`.
- **Detalle**: Flujo completo de selección de menú, cálculo de monto total y generación de registro de compra. Incluye la lógica necesaria para la emisión de confirmaciones.

### E. Buzón de Sugerencias
- **Implementación**: `SuggestionController.java`, `Suggestion.java`.
- **Detalle**: Backend preparado para recibir sugerencias categorizadas (alimentos, infraestructura, atención) vinculadas al usuario que las realiza.

### F. Estadísticas
- **Implementación**: `StatsController.java` y `StatsService.java`.
- **Detalle**: Generación de reportes sobre menús vendidos y recaudación por periodos (diario, semanal, mensual).

---

## 🔐 Seguridad y Configuración

- **Autenticación**: Basada en tokens **JWT**. El sistema utiliza `@Value` para inyectar la clave secreta desde variables de entorno, evitando la exposición de claves en el código fuente.
- **Configuración**: Se encuentra en `src/main/resources/application.properties`. Puedes configurar tu `JWT_SECRET` como variable de entorno.

## 🐳 Ejecución con Docker

El proyecto incluye una configuración de Docker para facilitar el despliegue del entorno:

```bash
docker-compose up --build
```

Esto levantará dos contenedores:
1.  **db**: Base de datos MySQL 8.0 con persistencia de datos en volumen.
2.  **app**: La aplicación Spring Boot lista para recibir peticiones en el puerto `8080`.

---

## 🛠️ Instalación y Ejecución Manual

1.  Clonar el repositorio:
    ```bash
    git clone https://github.com/LucianoWagner/ORM-TTPS.git
    ```
2.  Configurar la base de datos en `application.properties`:
    ```properties
    spring.datasource.url=jdbc:mysql://localhost:3306/nombre_tu_db
    spring.datasource.username=tu_usuario
    spring.datasource.password=tu_password
    ```
3.  Ejecutar con Maven:
    ```bash
    mvn spring-boot:run
    ```

---

## 📄 Licencia
Este proyecto fue realizado como parte del Trabajo Final de la materia **Taller de Tecnologías de Producción de Software (TTPS)** - Opción Java.
