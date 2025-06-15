
# JWT Auth API (Spring Boot)

API simples em Spring Boot 3 + Java 17 com autenticação JWT e controle de acesso por **roles** (`USER`, `ADMIN`).

## Requisitos

- JDK 17+
- Maven 3.9+
- MySQL 8

## Passo a Passo para Rodar

1. **Clone o repositório**

```bash
git clone https://github.com/devefrens/atividade-crud-2bim-spring.git
cd jwt-auth-api
```

2. **Configure o banco**

Crie o banco `jwt_db` e ajuste as propriedades `spring.datasource.*` em:

```
src/main/resources/application.properties
```

Exemplo de criação do banco:

```sql
CREATE DATABASE jwt_db;
```

3. **Execute a aplicação**

```bash
./mvnw spring-boot:run
```

A API sobe em:  
`http://localhost:8080`

## Como Testar

### 1. Registro

```bash
curl -X POST http://localhost:8080/auth/register \
-H "Content-Type: application/json" \
-d '{"name":"Admin","email":"admin@email.com","password":"123","role":"ADMIN"}'
```

### 2. Login

```bash
curl -X POST http://localhost:8080/auth/login \
-H "Content-Type: application/json" \
-d '{"email":"admin@email.com","password":"123"}'
```

> O retorno terá um JSON assim:  
`{ "token": "..." }`

### 3. Endpoints protegidos

**Listar usuários (ADMIN):**

```bash
curl -H "Authorization: Bearer <TOKEN>" http://localhost:8080/users
```

**Ver meu perfil (USER ou ADMIN):**

```bash
curl -H "Authorization: Bearer <TOKEN>" http://localhost:8080/users/me
```

## Estrutura de Pastas

```
controller/      # REST controllers
service/         # Regras de negócio
repository/      # Spring Data JPA
security/        # JWT utils + filtros + config
model/           # Entidades JPA
```
