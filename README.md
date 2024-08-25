# Prisma API

Este projeto é uma API desenvolvida utilizando [NestJS](https://nestjs.com/), um framework Node.js para a construção de aplicações eficientes e escaláveis do lado do servidor. A API está integrada com o Prisma, um ORM moderno para Node.js e TypeScript.

## Índice

- [Instalação](#instalação)
- [Configuração](#configuração)
- [Uso](#uso)
- [Funcionalidades](#funcionalidades)
- [Configuração com Docker](#configuração-com-docker)
- [Principais Tecnologias](#principais-tecnologias)
- [Scripts Disponíveis](#scripts-disponíveis)

## Instalação

1. Clone o repositório:
   ```bash
   git clone https://github.com/AlfredoLSN/prisma-api
   ```
2. Navegue até o diretório do projeto:
   ```bash
   cd prisma-api
   ```
3. (Opcional) Se você não estiver usando Docker, instale as dependências manualmente:
   ```bash
   npm install
   ```

## Configuração

O projeto utiliza variáveis de ambiente para configurar as credenciais e outros parâmetros importantes. As variáveis de ambiente são definidas no arquivo `.env`, que deve ser colocado na raiz do projeto.

Aqui está um exemplo de um arquivo `.env` utilizado neste projeto:

```bash
# Ambiente de Desenvolvimento
NODE_ENV=development

# Porta em que o servidor irá rodar
PORT=3000

# URL de conexão com o banco de dados PostgreSQL
DATABASE_URL="postgresql://postgres:docker@db:5432/prismaapi?schema=public"
```

### Detalhes das Variáveis:

- **NODE_ENV**: Define o ambiente em que a aplicação está rodando. Neste caso, está configurado como `development`.
- **PORT**: Especifica a porta em que a aplicação estará disponível. Está configurada para rodar na porta `3000`.
- **DATABASE_URL**: Contém a string de conexão para o banco de dados PostgreSQL, incluindo as credenciais de acesso, host, porta e o esquema a ser utilizado.

Certifique-se de ajustar essas variáveis de acordo com o ambiente em que você está executando a aplicação (desenvolvimento, produção, etc.).

## Uso

Para iniciar a aplicação em modo de desenvolvimento:

```bash
npm run start:dev
```

Para iniciar a aplicação em modo de produção:

```bash
npm run build
npm start
```

## Funcionalidades

### Users

- **Criação de Usuários:** Permite a criação de novos usuários no sistema com atributos como `email`, `name`, e `admin`.
- **Listagem de Usuários:** Exibe uma lista de todos os usuários cadastrados, incluindo suas informações e posts associados.
- **Detalhes de Usuário:** Visualiza informações detalhadas de um usuário específico, incluindo os posts que ele criou.
- **Atualização de Usuários:** Permite a atualização de atributos dos usuários, como nome, email e status de administrador.
- **Remoção de Usuários:** Permite remover usuários do sistema, juntamente com seus posts associados.

### Posts

- **Criação de Posts:** Usuários podem criar posts com um `título`, `conteúdo` e `email do autor`.
- **Listagem de Posts:** Exibe uma lista de todos os posts criados.
- **Detalhes de Post:** Visualiza informações detalhadas de um post específico.
- **Atualização de Posts:** Permite a atualização dos atributos de um post, como `título` e `conteúdo`.
- **Remoção de Posts:** Permite remover posts do sistema.

### Estrutura do Banco de Dados

- **User:** Representa os usuários do sistema, cada um com um email único, nome, status de administrador, e a data de criação. Um usuário pode ter múltiplos posts.
- **Post:** Representa os posts criados pelos usuários. Cada post possui um título, conteúdo opcional, status de publicação, e timestamps de criação e atualização. Os posts são associados aos usuários, que são seus autores.

## Configuração com Docker

Este projeto utiliza Docker para simplificar o ambiente de desenvolvimento e garantir que todos os desenvolvedores utilizem a mesma configuração. Abaixo estão as instruções para configurar e iniciar o projeto usando Docker e Docker Compose.

### Pré-requisitos

- [Docker](https://www.docker.com/get-started) instalado.
- [Docker Compose](https://docs.docker.com/compose/install/) instalado.

### Instruções

1. **Construir e iniciar os contêineres**:

   Execute o seguinte comando na raiz do projeto para construir as imagens Docker e iniciar os contêineres definidos no `docker-compose.yml`:

   ```bash
   docker-compose up --build
   ```

   Isso irá:

   - Construir a imagem do aplicativo Node.js/NestJS.
   - Iniciar o contêiner da aplicação (`prismaapi-app`) que será acessível na porta `3000`.
   - Iniciar o contêiner do banco de dados PostgreSQL (`prismaapi-db`) que será acessível na porta `5432`.

2. **Acessar a aplicação**:

   Após o comando anterior, a API estará disponível em `http://localhost:3000`.

3. **Parar os contêineres**:

   Para parar os contêineres, execute:

   ```bash
   docker-compose down
   ```

### Notas Adicionais

- O banco de dados PostgreSQL é iniciado com as credenciais definidas nas variáveis de ambiente do contêiner `db`. Certifique-se de que as mesmas credenciais sejam usadas no arquivo `.env` para a variável `DATABASE_URL`.

## Principais Tecnologias

- **[NestJS](https://nestjs.com/)**: Framework para construção de aplicações escaláveis do lado do servidor em Node.js.
- **[Prisma](https://www.prisma.io/)**: ORM para Node.js e TypeScript que simplifica o trabalho com banco de dados.
- **[PostgreSQL](https://www.postgresql.org/)**: Sistema de gerenciamento de banco de dados relacional utilizado para armazenar os dados da aplicação.
- **[Docker](https://www.docker.com/)**: Plataforma para automatizar o desenvolvimento, a distribuição e a execução de aplicações em contêineres.

## Scripts Disponíveis

- `npm run build`: Compila o projeto.
- `npm run format`: Formata o código usando Prettier.
- `npm run start`: Inicia a aplicação.
- `npm run start:dev`: Inicia a aplicação em modo de desenvolvimento com watch.
- `npm run start:prod`: Inicia a aplicação em modo de produção.
- `npm run lint`: Executa o ESLint e corrige problemas encontrados.
- `npm run test`: Executa os testes unitários.
- `npm run test:watch`: Executa os testes em modo de observação.
- `npm run test:cov`: Executa os testes e gera um relatório de cobertura.
- `npm run test:debug`: Inicia a aplicação em modo de depuração e executa os testes.
- `npm run test:e2e`: Executa os testes end-to-end.
