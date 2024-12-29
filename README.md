# Projeto: SpringBoot - API de Cadastro de Médicos e Pacientes
Este projeto é uma API REST construída com **Spring Boot**. O objetivo do projeto é gerenciar o cadastro de médicos e pacientes de uma clínica médica fictícia, além de fornecer endpoints para manipular essas informações.
## Funcionalidades
A aplicação conta com diversas funcionalidades que permitem:
1. **Gerenciamento de Médicos**:
    - Cadastro de médicos.
    - Listagem de médicos com paginação.
    - Atualização de informações de médicos.
    - Exclusão lógica de médicos (soft delete).

2. **Gerenciamento de Pacientes**:
    - Cadastro de pacientes.
    - Listagem de pacientes com paginação.

3. **Validações e Tratamento de Erros**:
    - Validação de dados como e-mail, telefone, CRM, CEP, entre outros.
    - Respostas apropriadas para erros, retornando HTTP 400 ou 404 quando necessário.

4. **Autenticação e Segurança**:
    - Autenticação utilizando JWT (JSON Web Token).
    - Controle de acesso aos endpoints.

## Principais Tecnologias Utilizadas
- **Java 17**: Linguagem utilizada no desenvolvimento.
- **Spring Boot**: Base para desenvolvimento ágil da aplicação.
- **Spring Data JPA**: Para abstração e manipulação do banco de dados.
- **Bean Validation**: Validação de dados diretamente via anotações.
- **Spring Security**: Para autenticação e segurança da API.
- **Lombok**: Para reduzir o boilerplate de código.
- **H2 Database**: Banco de dados em memória para desenvolvimento e testes.
- **JUnit e Mockito**: Para testes automatizados.

## Estrutura do Projeto
O projeto segue uma estrutura de camadas bem definida:
1. **`controller`**:
    - Camada que gerencia os endpoints da API.
    - Contém os métodos para manipular médicos, pacientes e autenticação.

2. **`domain`**:
    - Contém as entidades principais do sistema, como `Medico`, `Paciente`, e `Endereco`.
    - Inclui também os repositórios (interfaces que estendem `JpaRepository`) e classes DTO para comunicação entre cliente e servidor.

3. **`infra`**:
    - Configurações da API.
    - Implementações para segurança e autenticação com JWT.
    - Tratamento global de erros.

## Endpoints Disponíveis
### Autenticação
#### **POST /login**
Endpoint para autenticação de usuários no sistema.
- **Requisição**:
``` json
  {
    "login": "exemplousuario",
    "senha": "exemplosenha"
  }
```
- **Resposta**:
    - HTTP 200 (OK):
``` json
    {
      "token": "jwt-gerado-pela-api"
    }
```
- HTTP 401 (Unauthorized): Se as credenciais estiverem incorretas.

### Médicos
#### **POST /medicos**
Cadastra um novo médico no sistema.
- **Requisição**:
``` json
  {
    "nome": "exemplo",
    "email": "exemplo@voll.med",
    "crm": "exemplo",
    "telefone": "exemplo",
    "especialidade": "exemplo",
    "endereco": {
      "logradouro": "exemplo",
      "bairro": "exemplo",
      "cep": "exemplo",
      "cidade": "exemplo",
      "uf": "exemplo",
      "numero": "exemplo",
      "complemento": "exemplo"
    }
  }
```
- **Respostas**:
    - **201 (Created)**: Médico cadastrado com sucesso.
    - **400 (Bad Request)**: Quando os dados fornecidos são inválidos.

#### **GET /medicos**
Lista todos os médicos cadastrados com paginação.
- **Parâmetros de URL** (opcionais):
    - `page`: Número da página (default: 0).
    - `size`: Tamanho da página (default: 10).
    - `sort`: Campo de ordenação (ex.: nome, email).

- **Resposta**:
``` json
  {
    "content": [
      {
        "id": 1,
        "nome": "exemplo",
        "email": "exemplo@voll.med",
        "crm": "exemplo",
        "telefone": "exemplo",
        "especialidade": "exemplo"
      },
      {
        "id": 2,
        "nome": "exemplo",
        "email": "exemplo@voll.med",
        "crm": "exemplo",
        "telefone": "exemplo",
        "especialidade": "exemplo"
      }
    ],
    "totalElements": 2,
    "totalPages": 1,
    "number": 0,
    "size": 10
  }
```
#### **PUT /medicos/{id}**
Atualiza as informações de um médico cadastrado.
- **Requisição**:
``` json
  {
    "nome": "exemplo",
    "telefone": "exemplo"
  }
```
- **Resposta**:
    - **200 (OK)**: Dados do médico atualizados com sucesso.
    - **404 (Not Found)**: Quando o médico não é encontrado.

#### **DELETE /medicos/{id}**
Exclui um médico do sistema (soft delete).
- **Resposta**:
    - **204 (No Content)**: Exclusão realizada com sucesso.
    - **404 (Not Found)**: Quando o médico não é encontrado.

### Pacientes
#### **POST /pacientes**
Cadastra um novo paciente no sistema.
- **Requisição**:
``` json
  {
    "nome": "Exemplo de Nome",
    "email": "exemplodeemail@gmail.com",
    "telefone": "exemplo",
    "cpf": "exemplo",
    "endereco": {
      "logradouro": "exemplo",
      "bairro": "exemplo",
      "cep": "exemplo",
      "cidade": "exemplo",
      "uf": "exemplo",
      "numero": "exemplo",
      "complemento": "exemplo"
    }
  }
```
- **Respostas**:
    - **201 (Created)**: Paciente cadastrado com sucesso.
    - **400 (Bad Request)**: Quando os dados fornecidos são inválidos.

#### **GET /pacientes**
Lista todos os pacientes cadastrados com paginação.
- **Parâmetros de URL** (opcionais):
    - `page`: Número da página (default: 0).
    - `size`: Tamanho da página (default: 10).

## Configuração do Ambiente
1. **Pré-requisitos**:
    - Java 17 instalado.
    - Maven instalado.

2. **Passos**:
    1. Clone o repositório:
``` bash
      git@github.com:GiovanneSilva/Consulta-Medico-API-SpringBoot.git
```
1. Execute o projeto:
``` bash
      ./mvnw spring-boot:run
```
1. O servidor estará disponível em:
``` 
   http://localhost:8080
```
## Testes Automatizados
O projeto implementa testes de integração com JUnit 5 e MockMvc para validar os endpoints.
- Para rodar os testes, execute:
``` bash
  ./mvnw test
```

## Licença
Este projeto está licenciado sob a [Licença MIT]().
