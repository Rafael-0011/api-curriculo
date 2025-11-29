# Cadastro de Currículos e Dashboard de Candidatos

Descrição
---------
Projeto backend em Java com Spring Boot para cadastro de currículos e dashboard de candidatos. Oferece endpoints para cadastrar, consultar e atualizar currículos, além de funcionalidades de autenticação e dashboard (gráficos/dados agregados). Suporta controle de acesso por roles (`USER`, `ADMIN`) e permissões (ex.: `admin:update`) usando JWT.

Tecnologias
----------
- Java 17+
- Spring Boot
- Spring Security (JWT)
- Maven
- Docker / Docker Compose
- ModelMapper
- JUnit (testes)
- Estrutura de profiles: `dev`, `prod`, `test`

Estrutura do projeto (resumo)
-----------------------------
- `src/main/java/com/example/backend`
  - `controller` — controllers REST (ex.: `CurriculoCotroller`, `UserController`, `LoginController`, `GraficoController`)
  - `service` — lógica de negócio
  - `repository` — interfaces JPA
  - `model` / `dto` — entidades e objetos de transferência
  - `security` — configurações de autenticação e filtros
  - `config` — configurações adicionais (ModelMapper, tratamento de exceções, etc.)
- `src/main/resources`
  - arquivos de propriedades por profile: `application-dev.properties`, `application-prod.properties`, `application-test.properties`
  - chaves: `mykey.pem`, `mykey.pub`

Endpoints principais (resumo)
-----------------------------
- Auth / Login: (checar `LoginController`) — endpoint para autenticação e obtenção de token JWT.
- Currículos (`CurriculoCotroller`) — base path: `/form`
  - `POST /form` — cadastrar currículo (roles: `USER`, `ADMIN`)
  - `GET /form` — listar currículos (roles: `USER`, `ADMIN`)
  - `GET /form/{id}` — obter currículo por id (roles: `USER`, `ADMIN`)
  - `PUT /form/admin/{id}` — atualizar status (permissão: `admin:update`)
  - `PUT /form/user` — alterar dados do próprio currículo (roles: `USER`, `ADMIN`)
- Dashboard / Gráficos: (checar `GraficoController`) — endpoints para dados agregados/relatórios
- Usuário: (checar `UserController`) — gerenciamento de usuários e roles

Segurança
--------
- Autenticação baseada em JWT (ver diretório `security` e `token`)
- Roles: `USER`, `ADMIN`
- Permissões finas podem ser configuradas (ex.: `admin:update`)
- Chaves RSA para assinatura verificáveis em `src/main/resources`

Como executar (desenvolvimento)
-------------------------------
1. Build e run com Maven:
   - Linux: `./mvnw spring-boot:run`
2. Ou build e executar jar:
   - `./mvnw clean package`
   - `java -jar target/*.jar`
3. Usando Docker Compose (requer Docker):
   - `docker compose up --build`

Perfis de configuração
----------------------
- Por padrão usa o `application.properties`. Para rodar com profile específico:
  - `./mvnw spring-boot:run -Dspring-boot.run.profiles=dev`
  - ou setar `SPRING_PROFILES_ACTIVE=dev` ao executar o jar

Testes
------
- Executar testes unitários/integrados:
  - `./mvnw test`
