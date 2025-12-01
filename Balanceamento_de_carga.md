# [Início](./readme.md)

# Balanceamento de Carga (Load Balancing)

O **balanceamento de carga** é a técnica de distribuir requisições de clientes entre múltiplos servidores, garantindo desempenho, escalabilidade e alta disponibilidade.

---

## 1. Objetivos do Balanceamento de Carga

- Evitar sobrecarga em um único servidor  
- Reduzir **latência** e melhorar desempenho  
- Garantir **alta disponibilidade** (failover)  
- Permitir **escalabilidade horizontal**  
- Integrar com **CDNs** e caches  

---

## 2. Tipos de Balanceamento

### 2.1 Camada de Transporte (L4)

- Opera na camada TCP/UDP  
- Baseia-se em IP de origem/destino e portas  
- Rápido e eficiente, mas não entende conteúdo HTTP/HTTPS  
- Exemplo: LVS (Linux Virtual Server), HAProxy TCP

### 2.2 Camada de Aplicação (L7)

- Opera na camada HTTP/HTTPS  
- Pode analisar URL, cabeçalhos, cookies, sessão  
- Permite **roteamento avançado**  
- Exemplo: NGINX, Traefik, Envoy

---

## 3. Algoritmos de Distribuição de Requisições

### 3.1 Round Robin

- Distribui requisições **circularmente** entre todos os servidores ativos  
- Cada servidor recebe a mesma quantidade de requisições ao longo do tempo  
- Simples e eficiente quando todos os servidores têm **capacidade similar**  

Exemplo:
Requisição 1 → Servidor 1
Requisição 2 → Servidor 2
Requisição 3 → Servidor 3
Requisição 4 → Servidor 1

---

### 3.2 Least Connections (Menos Conexões)

- Direciona a requisição para o servidor que **tem menos conexões ativas**  
- Ideal quando os servidores têm **carga variável por requisição**  
- Garante que servidores menos ocupados recebam mais requisições, equilibrando melhor o tráfego

Exemplo:
Servidor 1 → 5 conexões
Servidor 2 → 2 conexões
Servidor 3 → 3 conexões

Nova requisição → Servidor 2 (menos conexões)

---

### 3.3 IP Hash

- Calcula um **hash do IP do cliente** para decidir qual servidor atenderá a requisição  
- Mantém a **persistência de sessão**: o mesmo cliente vai sempre para o mesmo servidor  
- Útil em aplicações sem backend compartilhado ou sem cache centralizado

Exemplo:
IP do cliente 192.168.1.10 → Hash → Servidor 2
IP do cliente 192.168.1.11 → Hash → Servidor 3

---

### 3.4 Weighted Round Robin / Weighted Least Connections

- Permite **atribuir pesos** aos servidores de acordo com sua capacidade  
- Servidores mais potentes recebem mais requisições  
- Funciona com Round Robin ou Least Connections

---

### 3.5 Random / Other

- Distribuição **aleatória**, útil para testes ou tráfego uniforme  
- Menos eficiente em ambientes com servidores de capacidades diferentes

---

## 4. Estratégias de Alta Disponibilidade

- **Health Checks:** balanceador verifica periodicamente a saúde dos servidores  
- **Failover automático:** servidores que falham são removidos temporariamente  
- **Sticky Sessions:** mantém cliente em um mesmo servidor, necessário para sessões não compartilhadas  
- **Escalabilidade horizontal:** adicionar ou remover servidores sem downtime

---

## 5. Implementações

- **Hardware:** F5, Citrix NetScaler  
- **Software:** NGINX, HAProxy, Traefik, Envoy  
- **Cloud / Gerenciado:** AWS ELB/ALB, GCP Load Balancer, Azure Load Balancer

---

## 6. Considerações Técnicas

- **TLS Termination:** balanceador pode tratar TLS para reduzir carga nos servidores  
- **Rate Limiting:** limita requisições por IP ou sessão  
- **Caching / CDN Integration:** reduz carga no backend  
- **Monitoramento:** métricas de CPU, memória, conexões e latência  
- **Token Bucket / Leaky Bucket / Heavy Bucket:** técnicas para controlar picos de requisições e evitar flooding

---

## 7. Diagrama Conceitual

```text
                   +-------------------+
                   |    Balanceador    |
                   +-------------------+
                 /          |           \
        +------------+ +------------+ +------------+
        | Servidor 1 | | Servidor 2 | | Servidor 3 |
        +------------+ +------------+ +------------+
``` 

# Siga para o próximo tópico -> [DoS e DDoS](./DoS_e_DDoS.md)