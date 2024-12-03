Documentação do Sistema de Gerenciamento de Livros e Usuários

1. Introdução

Este sistema implementa uma aplicação Node.js utilizando o framework Express para gerenciar usuários e livros, com autenticação básica e persistência de dados em um banco PostgreSQL. O projeto segue uma arquitetura organizada em camadas para separar responsabilidades e garantir maior manutenibilidade.
2. Estrutura do Projeto

O projeto está dividido nas seguintes camadas:

    Controllers: Gerencia as requisições HTTP e chama os serviços correspondentes.
    Routes: Define as rotas da API, conectando requisições aos controllers.
    Models: Representa as entidades do banco de dados.
    Repositories: Realiza a comunicação direta com o banco de dados.
    Services: Contém a lógica de negócios e validações.
    Helpers: Inclui funções auxiliares para hashing, validação e gerenciamento de sessões.
    Migrations: Scripts para criação e manutenção de tabelas no banco de dados.

3. Dependências

    Node.js: Ambiente de execução.
    Express: Framework para criação do servidor.
    PostgreSQL: Banco de dados relacional.
    pg: Cliente PostgreSQL para Node.js.
    crypto: Para hashing de senhas.
    cors: Para configurar políticas de segurança.

4. Arquivos Principais
4.1. Configuração do Banco de Dados

database.ts

    Configura uma conexão segura ao banco PostgreSQL usando a biblioteca pg.

4.2. Controllers

Gerenciam requisições HTTP e chamam os métodos de serviço.

    authController.ts:
        register: Registra um novo usuário.
        login: Autentica um usuário existente.

    bookController.ts:
        getAllBooks: Retorna todos os livros.
        addBook: Adiciona um novo livro.

    userController.ts:
        getUsers: Retorna todos os usuários.
        addUser: Cria um novo usuário.

4.3. Rotas

Define os endpoints da aplicação e conecta com os controllers:

    authRoutes.ts:
        POST /register: Cadastrar usuário.
        POST /login: Login de usuário.

    bookRoutes.ts:
        GET /livros: Obter lista de livros.
        POST /livros: Adicionar livro.

    userRoutes.ts:
        GET /users: Obter lista de usuários.
        POST /users: Criar usuário.

4.4. Models

Define a estrutura dos dados representados no banco:

    userModel.ts:
        Campos: id, name, email, passwordhash.

    bookModel.ts:
        Campos: id, title, author, price.

4.5. Repositories

Executam operações de banco de dados usando SQL parametrizado:

    userRepository.ts:
        Métodos: getUserByEmail, addUser, getAllUsers.

    bookRepository.ts:
        Métodos: getAllBooks, addBook.

4.6. Services

Executam lógica de negócios e validações:

    authService.ts:
        Registra usuários e autentica login.
        Usa helpers para hashing e gerenciamento de sessão.

    bookService.ts:
        Valida e adiciona livros, lista todos os livros.

    userService.ts:
        Valida e cria usuários, lista todos os usuários.

4.7. Helpers

Auxiliam em operações reutilizáveis:

    hashHelper.ts:
        hashPassword: Cria hash para senha.
        comparePassword: Verifica senhas.

    sessionHelper.ts:
        Gerencia sessões do usuário (simulado em memória).

    validationHelper.ts:
        Valida dados como email, nome, preço, título.

4.8. Migrations

Scripts para criação de tabelas no banco:

    migrations.ts:
        Cria tabela users.

    migrationsLivros.ts:
        Cria tabela books.

4.9. Servidor

server.ts:

    Inicializa o servidor Express.
    Configura middlewares (JSON, CORS).
    Define rotas e escuta na porta especificada.

5. Funcionalidades

    Registro e autenticação de usuários.
    Gerenciamento de livros (CRUD básico).
    Validações robustas para entrada de dados.
    Uso de hashing seguro para senhas.

6. Fluxo de Operação

    Usuário registra-se via /register.
    Autentica-se via /login.
    Gerencia livros via /livros endpoints.
    Consulta usuários via /users.

7. Melhorias Futuros

    Implementar autenticação via JWT para maior segurança.
    Adicionar paginação para listar livros e usuários.
    Integrar cache para melhorar desempenho em buscas frequentes.
    Conectar sistema a um serviço de emails para notificações.