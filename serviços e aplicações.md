# [Início](./readme.md)

# O que é REST?

**REST** (Representational State Transfer) é um **estilo de arquitetura** usado para criar **APIs** que se comunicam usando o protocolo HTTP. Ele define um conjunto de princípios que tornam a comunicação simples, escalável e padronizada.

---

## Ideia principal

No REST, cada **recurso** (ex: usuários, produtos, pedidos) é representado por uma **URL única**, e o cliente interage com esse recurso usando os **verbos HTTP corretos**.

### Exemplos:

| Ação | Método HTTP | URL |
|------|-------------|-----|
| Listar usuários | GET | /users |
| Buscar usuário específico | GET | /users/45 |
| Criar usuário | POST | /users |
| Atualizar usuário | PUT | /users/45 |
| Deletar usuário | DELETE | /users/45 |

---

## Os 6 princípios do REST

1. **Cliente–Servidor**  
   Separação clara entre cliente (frontend) e servidor (backend).

2. **Stateless (sem estado)**  
   O servidor não armazena informações sobre o cliente entre requisições.

3. **Cacheável**  
   As respostas devem informar se podem ou não ser armazenadas em cache.

4. **Interface Uniforme**  
   Uso padronizado de URLs, métodos HTTP e formatos como JSON.

5. **Camadas**  
   A arquitetura pode ter intermediários (proxies, load balancers, gateways).

6. **Code-On-Demand (opcional)**  
   O servidor pode enviar scripts para o cliente executar (pouco usado).

---

## Como uma API REST troca dados?

Normalmente usando **JSON**.

### Exemplo:

**Requisição:**


**Resposta JSON:**
```json
{
  "id": 11,
  "name": "Headset Gamer",
  "price": 299.00
}
``` 

### API RESTful

É uma API que segue os princípios do REST, e não só usa endpoints HTTP.

Princípios estes:

- Client / Server, separar completamente o cliente do servidor.

- Stateless, servidor não guarda 
contexto entre requisições, cada requisição é independente.

-Cacheável, guardar informações para que possa ser acessada mais facilmente sem a necessidade de contatar o servidor.

-Interface uniforme, é o ponto principal que separa o REST das outras arquiteturas, identificação de recursos, mensagens documentadas, HATEOAS -> responses devem ter links que indicam o que pode ser feito.

-Camadas e Gateways.

-Código sob demanda, o servidor pode enviar código executável para o cliente, porém essa é opcional.

# Siga para o próximo bloco -> [Arquitetura de 3 camadas](Arquitetura%203%20camadas.md)