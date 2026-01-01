# ¿Qué Comemos? - Buffet Management System 🍱

Este proyecto es una aplicación backend desarrollada en **Java** con **Spring Boot** para la administración integral del buffet de la Facultad de Informática. El sistema permite la gestión de menús, compras de tickets, buzón de sugerencias y estadísticas detalladas.

---

## 🚀 Tecnologías Utilizadas

- **Java 17**
- **Spring Boot 3.3.4**
- **Spring Data JPA** (Hibernate)
- **Spring Security** + **JWT** (JSON Web Tokens)
- **MySQL** (Base de Datos)
- **Lombok**
- **Maven** (Gestor de dependencias)

---

## 👥 Perfiles de Usuario

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

---

## 🛠️ Instalación y Ejecución

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
