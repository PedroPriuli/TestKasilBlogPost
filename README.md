# BlogPost API

API simples para gerenciamento de posts e comentários, desenvolvida com .NET 8, Dapper e SQLite, sem uso de migrations ou frameworks adicionais.

Este projeto demonstra uma arquitetura minimalista, organizada e focada em simplicidade, utilizando scripts SQL externos através de arquivos .sql.

# Tecnologias Utilizadas

.NET 8 Web API
Dapper
SQLite (Microsoft.Data.Sqlite)
SQL Scripts como Embedded Resources
Swagger / OpenAPI

# Configuração do Banco de Dados

A aplicação utiliza SQLite como banco de dados local.
A configuração está em:

appsettings.json

{
  "ConnectionStrings": {
    "DefaultConnection": "Data Source=blog.db"
  }
}


O arquivo blog.db será criado automaticamente na pasta raiz da aplicação.

# Endpoints Disponíveis
1. Listar todos os posts
GET /api/posts(Retorna uma lista dos posts cadastrados.)

2. Criar um novo post
POST /api/posts
(Exemplo de corpo da requisição:
{
  "title": "Título",
  "content": "Conteúdo do post"
})

3. Buscar um post por ID
GET /api/posts/{id} (Retorna um post específico e seus comentários associados.)

4. Adicionar comentário a um post
POST /api/posts/{id}/comments
(Corpo da requisição:
{
  "text": "Comentário"
})

# Uso de SQL Externo

Os scripts SQL ficam na pasta SqlScripts/ e são carregados pela classe SqlScripts:
SqlScripts.Read("sel_table_blogpost.sql");

# Exemplo de consulta:

var posts = await connection.QueryAsync(SqlScripts.Read("sel_table_blogpost.sql"));


Isso permite separar completamente SQL e código C#.

Funcionamento Interno do Controller

Cada ação abre uma nova conexão SQLite.

As queries são executadas com Dapper.

SQL é carregado a partir dos arquivos .sql.

Objetos anônimos são usados para retorno.

# Como Executar o Projeto

*Descompactar o arquivo .7z em sua máquina local

Clonar o repositório:

git clone [https://github.com/PedroPriuli/TestKasilBlogPost/tree/main]

Acessar o diretório

cd kasil.blogpost.api


# Executar o projeto

dotnet run


Acessar o Swagger

http://localhost:5000/swagger

https://localhost:5001/swagger

