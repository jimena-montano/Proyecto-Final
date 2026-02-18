Especificación Técnica: API REST - Sistema de Gestión de Biblioteca
Este documento describe el diseño de los endpoints para el sistema de biblioteca, utilizando estándares de la industria para arquitecturas RESTful.
1. Configuración GeneralBase URL: https://api.biblioteca-digital.com/v1Formato de datos: JSONAutenticación: Bearer Token (JWT)
2. Endpoints de Recursos
Libros (Books)
Método,Endpoint,Descripción
GET,/books,Obtiene la lista de todos los libros (Soporta paginación y filtros).
GET,/books/{id},Obtiene los detalles de un libro específico por su UUID.
POST,/books,Registra un nuevo libro en el sistema.
PUT,/books/{id},Actualiza la información completa de un libro.
PATCH,/books/{id},Actualiza parcialmente un libro (ej. cambiar disponibilidad).
DELETE,/books/{id},Elimina un libro del catálogo.

Usuarios (Users)
Gestión de miembros de la biblioteca.
Método,Endpoint,Descripción
GET,/users/{id},Perfil del usuario y libros actualmente en su posesión.
POST,/users/register,Registro de nuevos miembros.

Préstamos (Loans)
Control de transacciones de libros.
Método,Endpoint,Descripción
POST,/loans,Crea un nuevo registro de préstamo.
PATCH,/loans/{id}/return,Procesa la devolución de un libro.

3. Códigos de Estado (HTTP Status Codes)
La API utiliza los siguientes códigos para comunicar el resultado de las peticiones:
200 OK: Petición exitosa.
201 Created: Recurso creado exitosamente (ej. tras un POST).
400 Bad Request: La petición tiene errores de validación.
401 Unauthorized: Falta token de autenticación o es inválido.
404 Not Found: El recurso solicitado no existe.
500 Internal Server Error: Error inesperado en el servidor.