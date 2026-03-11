# LiterAlura - Catálogo de Libros

Este proyecto es una aplicación de consola desarrollada en Java utilizando **Spring Boot** para gestionar un catálogo de libros y autores. La aplicación consume datos de la **API Gutendex**, procesa información en formato JSON mediante la biblioteca **Jackson** y persiste los datos en una base de datos **PostgreSQL** a través de **Spring Data JPA**.

---

## 🛠️ Tecnologías y Versiones

* **Java JDK:** 17 o superior.
* **Maven:** 4.0.0+.
* **Spring Boot:** 3.2.3.
* **PostgreSQL:** 16+.
* **Dependencias principales:**
* Spring Data JPA
* PostgreSQL Driver
* Jackson Databind



---

## 🚀 Funcionalidades Principales

1. **Búsqueda de libros por título:** Consulta la API de Gutendex, recupera el primer resultado y lo guarda en la base de datos junto con su autor.
2. **Listado de libros registrados:** Muestra todos los libros almacenados localmente.
3. **Listado de autores registrados:** Muestra los autores guardados y las obras asociadas a cada uno.
4. **Filtro de autores vivos:** Permite consultar qué autores estaban vivos en un año específico ingresado por el usuario.
5. **Filtro por idioma:** Lista los libros registrados según su código de idioma (ej. `es`, `en`, `fr`, `pt`).
6. **Estadísticas:** Uso de Java Streams para el conteo y filtrado eficiente de datos.

---

## ⚙️ Configuración del Entorno

### 1. Base de Datos

Es necesario tener una instancia de PostgreSQL activa. Crea una base de datos llamada `literalura` (o el nombre de tu preferencia).

### 2. Variables de Entorno / application.properties

Configura el archivo `src/main/resources/application.properties` con tus credenciales:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/literalura
spring.datasource.username=tu_usuario
spring.datasource.password=tu_contrasena
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=false
spring.jpa.properties.hibernate.format_sql=true

```

---

## 📖 Estructura del Proyecto

* **`model`**: Contiene las entidades JPA (`Libro`, `Autor`) y los *Records* para el mapeo de la API (`DatosLibro`, `DatosAutor`).
* **`repository`**: Interfaces que heredan de `JpaRepository` para la persistencia y consultas personalizadas (*Derived Queries*).
* **`service`**: Clases para el consumo de la API (`HttpClient`) y la transformación de JSON a objetos Java.
* **`principal`**: Clase con la lógica del menú interactivo y la captura de datos por consola (`Scanner`).

---

## 💻 Ejecución

Para iniciar la aplicación, ejecuta la clase `LiteraluraApplication`. El programa iniciará un bucle en consola con el siguiente menú:

```text
1 - Buscar libro por titulo
2 - Listar libros registrados
3 - Listar autores registrados
4 - Listar autores vivos en un determinado año
5 - Listar libros por idioma
0 - Salir

```

---

## 📝 Notas de Implementación

* El proyecto utiliza **CommandLineRunner** para ejecutar la lógica de consola inmediatamente después del arranque de Spring.
* Se implementaron relaciones `@ManyToOne` y `@OneToMany` entre `Libro` y `Autor` para garantizar la integridad referencial.
* Se incluyeron validaciones para evitar la inserción de libros duplicados basados en su título.
