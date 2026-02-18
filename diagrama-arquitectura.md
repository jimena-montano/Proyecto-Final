1. Diagrama Conceptual de la Arquitectura

El sistema se divide en tres capas principales: Cliente, Orquestación (Gateway) y Servicios de Dominio.

Componentes del Sistema
API Gateway (Nginx/Kong): Punto de entrada único para las aplicaciones cliente (Web/Mobile). Se encarga de la autenticación, ruteo y limitación de tasa (rate limiting).

Auth Service (OAuth2/JWT): Gestiona la identidad de los usuarios y emite tokens de acceso.

Order Service: Microservicio encargado de la lógica de negocio de pedidos. Expone la API REST definida en el Issue #2.

Inventory Service: Gestiona el stock de productos y responde a las consultas de GraphQL del Issue #3.

Message Broker (RabbitMQ/Kafka): Permite la comunicación asíncrona. Por ejemplo, cuando se crea un pedido, se envía un evento para descontar el inventario.

2. Decisiones Arquitectónicas (ADR)

Para darle un nivel de Arquitecto Senior, incluye estas justificaciones en tu documentación:

Persistencia Políglota: Cada microservicio tiene su propia base de datos (PostgreSQL para órdenes, MongoDB para catálogo) para asegurar el aislamiento.

Comunicación Event-Driven: Usamos eventos para mantener la consistencia eventual entre servicios, evitando el acoplamiento fuerte de llamadas HTTP internas.

BFF (Backend for Frontend): Implementamos una capa GraphQL para que el frontend no tenga que consultar 5 servicios distintos para renderizar una sola pantalla.