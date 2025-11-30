# Arquitetura de 3 Camadas (Three-Tier Architecture)

A **arquitetura de 3 camadas** é um modelo de organização de sistemas dividindo um software em **três partes independentes**, cada uma com sua função bem definida:

1. **Camada de Apresentação (Front-End)**
2. **Camada de Lógica/Aplicação (Back-End / API)**
3. **Camada de Dados (Banco de Dados)**

Esse modelo melhora escalabilidade, segurança, manutenção e organização do código.

---

## 1. Camada de Apresentação (Front-End)

É a parte que o usuário vê e interage.

Pode ser:
- Aplicação Web (HTML, CSS, JS, React, Vue, Angular…)
- Aplicativo Mobile (Flutter, Android, iOS)
- Aplicação Desktop

### Funções:
- Exibir informações para o usuário  
- Enviar ações do usuário para a API  
- Consumir dados vindos da API  

---

## 2. Camada de Aplicação (Back-End / API)

É o **coração da arquitetura**.  
Aqui ficam as **regras de negócio**, validações, segurança e toda a lógica do sistema.

Pode ser criada com:
- Node.js  
- Python (FastAPI, Django, Flask)  
- Java (Spring)  
- .NET  
- Go, PHP, Ruby etc.

### Funções da API:
- Receber requisições do front-end  
- Processar regras de negócio  
- Validar dados  
- Autenticar usuários (tokens, JWT, sessões…)  
- Consultar/atualizar o banco de dados  
- Retornar respostas no formato JSON  

A API é a **ponte** entre o front-end e o banco de dados.

---

## 3. Camada de Dados (Banco de Dados)

Responsável por armazenar e gerenciar dados.

Pode ser:
- SQL (MySQL, PostgreSQL, SQL Server)
- NoSQL (MongoDB, Redis, Cassandra)

### Funções:
- Guardar informações da aplicação  
- Responder consultas enviadas pela API  
- Garantir integridade e consistência dos dados  

---

# Como as 3 camadas se comunicam?

Fluxo padrão:

1. **Usuário → Front-End**  
   O usuário clica em algo, envia um formulário etc.

2. **Front-End → API (Back-End)**  
   O front-end envia uma requisição, geralmente HTTP/HTTPS.

3. **API → Banco de Dados**  
   A API valida, processa e consulta/atualiza os dados.

4. **Banco de Dados → API**  
   O banco devolve a informação solicitada.

5. **API → Front-End**  
   A API envia a resposta (geralmente JSON).

6. **Front-End → Usuário**  
   O front-end exibe o resultado na tela.

---

# Exemplo simples

### Requisição:
O front-end envia:
- GET /users/10

### API (Back-End):
- Valida o ID
- Busca no banco
- Monta a resposta JSON

### Banco de Dados retorna:
- { id: 10, name: "user", email: "user@example.com"}

Siga para o próximo tópico -> [Monólito x Microserviços](./Monólito%20x%20Microserviços.md)