# DNS — O que é, para que serve e como funciona

## 1. O que é DNS?

DNS (Domain Name System) é o **sistema que traduz nomes de domínio** (como `google.com`) em **endereços IP** (como `142.250.78.14`).

Ele funciona como a **agenda telefônica da internet**:
- Você lembra o nome do site.
- O DNS descobre o IP verdadeiro.
- Seu navegador usa o IP para se conectar ao servidor.

Sem DNS, você teria que acessar sites usando números IP.

---

## 2. Para que serve o DNS?

### Funções principais do DNS

1. **Resolver nomes em IPs**  
   Exemplo:
google.com → 142.250.78.14

2. **Organizar a hierarquia da internet**  
Cada domínio e subdomínio segue uma estrutura organizada.

3. **Direcionar serviços específicos**  
Através de registros como:
- **A / AAAA** → aponta para IPs
- **MX** → e-mails
- **TXT** → validações
- **CNAME** → alias de nome

4. **Melhorar desempenho**  
DNS é amplamente cacheado:
- no navegador
- no sistema operacional
- no roteador
- no provedor (ISP)
- em servidores globalmente distribuídos

5. **Equilíbrio e redundância**  
DNS distribui tráfego para vários servidores.


# 3. Como funciona o DNS? (Passo a passo)

Vamos resolver:
www.exemplo.com


## Etapa 1 — Verificar o cache

Antes de perguntar na internet, o computador procura:
- cache do navegador
- cache do sistema operacional
- cache do roteador
- cache do provedor

Se encontrado → fim do processo.


## Etapa 2 — Enviar requisição ao DNS recursivo

Se não estiver no cache local, o computador envia a consulta para um **DNS recursivo**, como:

- 8.8.8.8 (Google)
- 1.1.1.1 (Cloudflare)
- 9.9.9.9 (Quad9)
- DNS do provedor

O recursivo pergunta na internet até encontrar a resposta.

PC → DNS Recursivo → Internet

## Etapa 3 — Pergunta ao Root Server

Se o recursivo não sabe, ele consulta os **Root Servers**.

Existem 13 grupos de servidores raiz:
a.root-servers.net
b.root-servers.net
...
m.root-servers.net

yaml
Copiar código

Esses servidores sabem onde encontrar informações sobre TLDs como:
- .com
- .org
- .net
- .br
- etc.


## Etapa 4 — Root responde: “Pergunte ao servidor do TLD”

Para `www.exemplo.com`, o Root Server responde:

"Pergunte ao servidor do .com"


## Etapa 5 — DNS Recursivo pergunta ao servidor .com

O recursivo consulta o DNS do TLD `.com`.

Ele responde algo como:

O domínio exemplo.com é administrado pelo servidor de nomes: ns1.exemplo-dns.net


## Etapa 6 — Recursivo pergunta ao servidor autoritativo

O **servidor de nomes autoritativo** do domínio contém os registros reais.

Ele retorna:

www.exemplo.com → 203.0.113.55


(Aponta o IP real)


## Etapa 7 — Recursivo devolve o IP ao computador

O DNS recursivo envia a resposta final:

203.0.113.55

O computador armazena no cache por alguns minutos ou horas (TTL).


# 4. Diagrama completo do processo DNS

| Etapa | Componente | Ação |
|------|------------|-------|
| 1 | **Navegador** | Solicita resolução de domínio |
| 2 | **Cache local (OS)** | Verifica se já possui o IP armazenado |
| 3 | **DNS Recursivo** | Inicia a busca caso não esteja em cache |
| 4 | **Root Servers** | Informam qual servidor TLD deve ser consultado |
| 5 | **Servidor TLD (.com, .net, .org...)** | Informa quais são os servidores autoritativos do domínio |
| 6 | **Servidor Autoritativo** | Retorna o IP verdadeiro do domínio |
| 7 | **DNS Recursivo** | Devolve a resposta final |
| 8 | **Navegador** | Recebe o IP e realiza a conexão |

# 5. Tipos de registros DNS mais usados

| Registro | Função |
|---------|--------|
| **A** | Mapeia domínio → IPv4 |
| **AAAA** | Mapeia domínio → IPv6 |
| **CNAME** | Alias para outro domínio |
| **MX** | Servidores de e-mail |
| **TXT** | Informações extras (SPF, DKIM, verificações) |
| **NS** | Servidores de nome do domínio |
| **SOA** | Configurações básicas do domínio |
| **SRV** | Serviços (VoIP, jogos, etc.) |


# 6. Resumo geral

- DNS é um sistema que **traduz nomes em IPs**.  
- Ele funciona de forma **hierárquica** e **cacheada**.  
- Envolve root servers, TLDs e servidores autoritativos.  
- É essencial para navegação, e-mail, serviços na web, autenticação e muito mais.

# Siga para o próximo tópico -> [Tipos de ataque](./Tipos%20de%20ataque.md)