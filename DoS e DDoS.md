# DoS e DDoS — Conceito e Mitigação

## 1. O que é DoS (Denial of Service)

Um **DoS (Denial of Service)** é um ataque em que um atacante tenta **derrubar um serviço**, **impedir acesso** ou **consumir completamente os recursos** de um servidor.

Características:
- Origem **única**
- Simples de identificar
- Fácil de bloquear por IP
- Impacto limitado

Exemplos de ataques:
- Flood de requisições HTTP
- SYN Flood
- UDP Flood
- Exaustão de CPU/memória

---

## 2. O que é DDoS (Distributed Denial of Service)

Um **DDoS** é um ataque de negação de serviço distribuído, vindo de **milhares ou milhões de dispositivos** ao mesmo tempo — normalmente uma **botnet**.

Características:
- Múltiplas origens (dificulta bloqueio)
- Volume muito maior que DoS
- Mais difícil de rastrear
- Pode saturar o link de Internet antes de chegar ao servidor

Tipos comuns:
- **Volumétrico:** saturação de banda  
- **Protocolo / L4:** SYN Flood, ACK Flood, UDP Flood  
- **Aplicação / L7:** HTTP Flood, ataques ao banco, crawlers agressivos  

---

## 3. Tipos de Ataques DDoS

### 3.1 Volumétricos (L3/L4)
Objetivo: saturar banda ou roteadores.  
Exemplos:
- UDP Flood
- ICMP Flood
- Amplification (DNS, NTP, SSDP)

### 3.2 Protocolo (L4)
Exploram falhas em TCP/UDP.  
Exemplos:
- SYN Flood (famoso handshake incompleto)
- ACK Flood
- RST Flood

### 3.3 Aplicação (L7)
Atacam a camada HTTP/HTTPS.  
Exemplos:
- HTTP GET/POST Flood
- Scrapers intensos
- Ataques lentos (Slowloris)

---

## 4. Técnicas de Mitigação

### 4.1 Rate Limiting
Limita a quantidade de requisições por IP, rota, endpoint ou intervalo de tempo.

Exemplos:
- *100 requisições por IP por minuto*
- Limitar conexões simultâneas
- Drop automático em caso de estouro

Ferramentas:
- NGINX `limit_req`
- HAProxy `stick-table`
- Cloudflare Rate Limit

---

### 4.2 Token Bucket e Leaky Bucket
Técnicas usadas em defensores e CDNs:

- **Token Bucket:** controla picos permitindo bursts limitados.  
- **Leaky Bucket:** garante fluxo constante, descartando excesso.  
- **Heavy Bucket:** detecta IPs que repetidamente estouram limites e os coloca em quarentena automática.

---

### 4.3 Firewalls e ACLs
Camada inicial de defesa:
- Bloqueio de portas desnecessárias  
- Filtros por ASN, país, ranges suspeitos  
- Bloqueio de protocolos de amplificação (NTP, SSDP, mDNS)  

---

### 4.4 WAF (Web Application Firewall)
Protege contra ataques de aplicação:
- Bloqueio de floods HTTP  
- Detecção de padrões anormais  
- Captchas  
- Anti-bot  
- Regras personalizadas

Exemplos:
- Cloudflare WAF  
- AWS WAF  
- ModSecurity (NGINX/Apache)

---

### 4.5 CAPTCHAs e Desafios
- Impedem bots de gerar carga excessiva  
- Forçam validação de humanidade  
- Podem ser acionados automaticamente durante picos de tráfego

---

### 4.6 CDNs e Edge Networks
CDNs absorvem tráfego **geograficamente distribuído** e filtram antes de chegar no servidor.

Benefícios:
- Proxy reverso global  
- Cache reduz carga no backend  
- Firewalls e mitigação automática  
- Escudos contra L7

Exemplos:
- Cloudflare  
- Akamai  
- Fastly  

---

### 4.7 Anycast Routing
Usado por CDNs e scrubbing centers.

Funcionamento:
- O mesmo IP é anunciado em vários datacenters  
- O tráfego vai para o **datacenter mais próximo** do atacante  
- Ataque é dividido globalmente, reduzindo impacto

---

### 4.8 Scrubbing Centers (Limpeza de tráfego)
Para ataques massivos (centenas de Gbps a Tbps).

Funcionam assim:
1. O tráfego é redirecionado (por BGP) para centros especializados  
2. Tráfego malicioso é filtrado  
3. Tráfego limpo volta para o servidor

Exemplos:
- Cloudflare Spectrum  
- AWS Shield Advanced  
- Arbor Networks  

---

### 4.9 Proteção por Proxy Reverso
O servidor real fica oculto atrás de um intermediário:
- Exposição do IP real é evitada  
- Ataques vão para o proxy (muito mais robusto)  
- Backend só recebe tráfego seguro

---

### 4.10 Limitação de Conexões TCP
- *Max SYN per IP*
- *Max connections per second*
- *Timeouts agressivos*
- Blacklist temporária de IPs suspeitos

---

### 4.11 Sistemas de Detecção e Anomalias
- IDS/IPS (Snort, Suricata)  
- ML/IA para padrões anormais  
- Alertas automáticos

---

## 5. Boas Práticas de Arquitetura contra DDoS

- Ter **IP escondido** atrás de CDN/proxy  
- Nunca expor portas desnecessárias  
- Usar HTTPS sempre (TLS ajuda a filtrar lixo)  
- Multicloud ou multi-região quando possível  
- Balanceadores redundantes (L4 + L7)  
- Logs centralizados para análise rápida  

---

## 6. Diagrama Simples de Mitigação

```text
                      Ataque DDoS
                           |
                           v
                +-----------------------+
                |   CDN / Anycast Edge  |
                |  Rate limit e WAF L7  |
                +-----------------------+
                           |
                           v
                +-----------------------+
                | Scrubbing Center L3/L4|
                |   (limpeza global)    |
                +-----------------------+
                           |
                           v
                +-----------------------+
                | Balanceador Interno   |
                +-----------------------+
                           |
                           v
                Servidores de Aplicação
```