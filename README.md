# Emprego, Capacitação e Empreendedorismo Local - Backend

## 📝 Descrição do Projeto
API REST desenvolvida em Java e Spring Boot com o objetivo de centralizar e conectar talentos locais a oportunidades de trabalho e cursos de aperfeiçoamento profissional, além de fomentar e dar visibilidade ao ecossistema de empreendedorismo regional.

A aplicação conta com uma camada robusta de segurança baseada em autenticação stateless para garantir a integridade dos dados de cidadãos e empresas parceiras.

## 🎯 Objetivo
Resolver a fragmentação de informações no desenvolvimento socioeconômico municipal, oferecendo uma plataforma integrada que unifique a busca por vagas de emprego, a oferta de trilhas de aprendizado qualificadoras e o suporte a pequenos negócios locais em um único ambiente digital seguro.

## 🛠️ Tecnologias Utilizadas
- **Java 17+**
- **Spring Boot 3.x**
- **Spring Security** & **JWT (JSON Web Tokens)** (Autenticação e Autorização)
- **Jakarta Bean Validation** (Validação de Dados)
- **Jackson** (Serialização/Desserialização de Objetos)
- **MySQL / PostgreSQL**
- **Maven** (Gerenciador de Dependências)

---

## 🔒 Segurança e Autenticação
A API utiliza **Spring Security** integrado com **JWT**. 
- As rotas sob o prefixo `/auth` são públicas.
- As demais rotas comerciais requerem que o cliente envie um token válido contido no cabeçalho HTTP da requisição:
  ```http
  Authorization: Bearer <seu_token_jwt_aqui>
Dados sensíveis como senhas de usuários utilizam criptografia BCrypt antes de persistirem no banco e são ocultados nas respostas da API através do filtro @JsonIgnore.

🚀 Como Rodar o Projeto
Clone o repositório:

Bash
git clone [https://github.com/Daniel-dev871/Emprego-Capacita-o-e-Empreendedorismo-Local.git](https://github.com/Daniel-dev871/Emprego-Capacita-o-e-Empreendedorismo-Local.git)
Configure o banco de dados:
Abra o arquivo src/main/resources/application.properties (ou application.yml) e ajuste as credenciais de conexão do seu banco de dados (URL, username e password).

Instale as dependências e execute a aplicação:

Bash
./mvnw spring-boot:run
A API estará disponível por padrão em http://localhost:8080.

🛣️ Endpoints Principais da API
🔐 Autenticação (/auth)
POST /auth/register - Cadastra um novo usuário no sistema (Senha criptografada via BCrypt).

POST /auth/login - Valida credenciais e retorna um Token JWT para acesso às rotas privadas.

💼 Vagas de Emprego (/vagas)
GET /vagas - Lista todas as vagas disponíveis no sistema.

GET /vagas/{id} - Busca os detalhes de uma vaga específica pelo ID (Retorna 404 caso não exista).

POST /vagas - Registra uma nova oportunidade de emprego (Retorna HTTP 201).

PUT /vagas/{id} - Atualiza dados de uma vaga usando validações controladas via DTO.

DELETE /vagas/{id} - Remove uma vaga do portal (Retorna HTTP 204).

🎓 Cursos de Capacitação (/cursos)
GET /cursos - Lista todos os cursos cadastrados na plataforma.

GET /cursos/{id} - Detalha um curso específico utilizando busca segura via Optional.

POST /cursos - Permite a inclusão de novas trilhas de aprendizado no sistema (Retorna HTTP 201).

👥 Usuários e Governança (/usuarios)
GET /usuarios - Lista todos os usuários cadastrados (Rota Privada: Requer token JWT de nível adequado. Omite o hash da senha automaticamente).

🩺 Monitoramento (/status)
GET /status - Rota pública de Health Check para verificar se o backend está online e operando na nuvem.

📊 Diagrama do Banco de Dados
Snippet de código
erDiagram

    USUARIO ||--o{ CANDIDATURA : realiza
    EMPRESA ||--o{ VAGA : publica
    USUARIO ||--o{ INSCRICAO_CURSO : participa
    CURSO ||--o{ INSCRICAO_CURSO : possui
    VAGA ||--o{ CANDIDATURA : recebe
    USUARIO ||--o{ NOTIFICACAO : recebe
    USUARIO ||--o{ EMPREENDEDORISMO : cria

    USUARIO {
        int ID_Usuario PK
        string NomeCompleto
        string CPF
        string Email
        string Senha
        string Telefone
        string TipoUsuario
    }

    EMPRESA {
        int ID_Empresa PK
        string NomeEmpresa
        string CNPJ
        string Email
        string Telefone
        string Endereco
        string Descricao
    }

    VAGA {
        int ID_Vaga PK
        string Titulo
        string Descricao
        string Requisitos
        decimal Salario
        string Localizacao
        string TipoContrato
        string Modalidade
        string StatusVaga
    }

    CANDIDATURA {
        int ID_Candidatura PK
        int ID_Usuario FK
        int ID_Vaga FK
        datetime DataCandidatura
        string StatusCandidatura
    }

    CURSO {
        int ID_Curso PK
        string Titulo
        string Categoria
        int CargaHoraria
        string Nivel
        string Instituicao
    }

    INSCRICAO_CURSO {
        int ID_Inscricao PK
        int ID_Usuario FK
        int ID_Curso FK
        datetime DataInscricao
        string StatusInscricao
    }

    EMPREENDEDORISMO {
        int ID_Projeto PK
        string NomeProjeto
        string Categoria
        string Localizacao
        string Descricao
    }

    NOTIFICACAO {
        int ID_Notificacao PK
        int ID_Usuario FK
        string Titulo
        string Mensagem
        datetime DataEnvio
        boolean StatusLeitura
    }
👥 Integrantes do Projeto
Daniel Duarte (01847432)

Erik Menezes (01848032)

Hélio Tarquino (01548379)

Kilderys Kallayb (01274330)

Wesley gonçalves (01849581)

Thales Tadeu (01857106)
