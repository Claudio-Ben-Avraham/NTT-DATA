# 🛍️ Sistema de Catálogo de Produtos e Simulação de Pedidos com Microsserviços

Este projeto implementa um sistema simples de **catálogo de produtos** e **simulação de pedidos**, utilizando arquitetura de microsserviços com **Spring Boot** e **Spring Cloud**. A comunicação entre os microsserviços é feita por HTTP, com suporte a **Service Discovery** e **API Gateway**.

## 📌 Visão Geral

O sistema é composto por dois microsserviços principais:

- **product-service**: Gerencia os produtos disponíveis no catálogo.
- **order-service**: Permite simular pedidos a partir dos produtos cadastrados.

Além disso, há dois componentes de infraestrutura:

- **eureka-server**: Serviço de descoberta para registrar e localizar microsserviços.
- **api-gateway**: Roteador central que expõe uma única URL pública e redireciona as requisições aos serviços apropriados.

## 🧱 Arquitetura

[Client] --> [API Gateway] --> [Eureka Service Discovery]
↙ ↘
[Product Service] [Order Service]


## ⚙️ Tecnologias Utilizadas

- Java 17
- Spring Boot
- Spring Cloud (Eureka, Gateway)
- Maven
- RESTful APIs
- Lombok
- OpenFeign (opcional)
- H2 Database (para testes locais)

## 📁 Estrutura dos Microsserviços

### 1. product-service

- Endpoint: `/products`
- Funcionalidades:
  - Cadastrar novo produto
  - Listar produtos
  - Buscar produto por ID

### 2. order-service

- Endpoint: `/orders`
- Funcionalidades:
  - Criar um pedido com base nos IDs de produtos
  - Listar pedidos simulados

> O `order-service` consome o `product-service` via HTTP para obter os detalhes dos produtos durante a criação do pedido.

## 🚀 Como Executar o Projeto

### Pré-requisitos

- JDK 17+
- Maven 3.8+
- Docker (opcional para infraestrutura)

### Passo a Passo

1. **Clone o repositório**:

```bash
git clone https://github.com/seuusuario/catalogo-pedidos-microsservicos.git
cd catalogo-pedidos-microsservicos

    Execute o eureka-server:

cd eureka-server
mvn spring-boot:run

    Execute o product-service e order-service (em terminais separados):

cd ../product-service
mvn spring-boot:run

cd ../order-service
mvn spring-boot:run

    Execute o api-gateway:

cd ../api-gateway
mvn spring-boot:run

    Acesse o sistema:

    Eureka Dashboard: http://localhost:8761

    API Gateway: http://localhost:8080

🔀 Exemplos de Requisições
Criar Produto

POST /products
Content-Type: application/json

{
  "name": "Notebook Lenovo",
  "description": "Intel i7, 16GB RAM",
  "price": 4200.00
}

Criar Pedido

POST /orders
Content-Type: application/json

{
  "productIds": [1, 2]
}

📦 API Gateway - Roteamento

O api-gateway encaminha:

    /api/products/** → product-service

    /api/orders/** → order-service

Exemplo:

GET http://localhost:8080/api/products

🔍 Service Discovery (Eureka)

Todos os microsserviços se registram no eureka-server, permitindo a localização dinâmica dos serviços.
✅ Melhorias Futuras

    Integração com banco de dados PostgreSQL ou MySQL

    Persistência de pedidos

    Autenticação com OAuth2 ou JWT

    Documentação Swagger/OpenAPI
