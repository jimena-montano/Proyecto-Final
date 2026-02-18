GraphQL

"""
Representa un producto dentro del catálogo del sistema.
Proveniente del microservicio de Inventario.
"""
type Product {
  id: ID!
  name: String!
  price: Float!
  stock: Int!
}

"""
Representa una orden de compra realizada por un usuario.
Proveniente del microservicio de Órdenes.
"""
type Order {
  id: ID!
  createdAt: String!
  status: OrderStatus!
  items: [Product!]!
  totalAmount: Float!
}

enum OrderStatus {
  PENDING
  SHIPPED
  DELIVERED
  CANCELLED
}

# --- Consultas (Queries) ---

type Query {
  # Obtiene el detalle de un pedido incluyendo los productos relacionados
  getOrderDetails(orderId: ID!): Order
  
  # Lista todos los productos disponibles con filtro opcional
  getProducts(limit: Int): [Product!]!
}

# --- Mutaciones (Mutations) ---

type Mutation {
  # Permite actualizar el stock tras una devolución o ajuste manual
  updateProductStock(productId: ID!, newQuantity: Int!): Product
  
  # Crea un nuevo pedido en el sistema
  createOrder(productIds: [ID!]!): Order
}