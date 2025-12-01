# [Início](./readme.md)

# Ataques DNS — Tipos, Funcionamento e Mitigações (Completo e Técnico)

O DNS é um alvo crítico para ataques porque atua como a "agenda telefônica" da internet.  
Comprometê-lo significa controlar para onde o usuário vai.  
Abaixo estão os ataques mais relevantes, sua lógica interna e técnicas modernas de mitigação.

---

# 1. DNS Spoofing (Falsificação de DNS)

## O que é  
Forjamento de respostas DNS para enganar o cliente, substituindo o IP legítimo por um IP malicioso.

## Como funciona  
- O atacante envia uma resposta falsa antes da verdadeira.
- Se o cliente aceitar a resposta falsa, ele acessa um servidor controlado pelo atacante.
- Pode ocorrer em redes inseguras ou roteadores comprometidos.

## Mitigações  
- DNSSEC (garante assinaturas digitais de registros)  
- HTTPS + HSTS  
- DNS over HTTPS (DoH) / DNS over TLS (DoT)  
- Firewall bloqueando tráfego DNS não autorizado  
- Taxação e filtragem de pacotes suspeitos (rate limiting)

---

# 2. DNS Cache Poisoning (Envenenamento de Cache)

## O que é  
Inserção de registros falsos no cache do DNS recursivo.

## Como funciona  
1. O atacante envia requisições repetidas ao recursor.  
2. Em paralelo, envia respostas DNS falsas tentando adivinhar:  
   - Porta origem utilizada  
   - ID de transação  
3. Se acertar, o registro falso é armazenado no cache.  
4. Todos os usuários que usam esse DNS são afetados.

## Mitigações  
- DNSSEC (a única defesa completa)  
- Randomização de porta TCP/UDP  
- Randomização de Query ID  
- TTLs curtos para registros críticos  
- Bloqueio de recursão aberta (Open Resolver)  
- Limitação de taxa de consultas idênticas (Rate Limiting DNS)

---

# 3. Man-in-the-Middle em DNS (MitM)

## O que é  
Interceptação do tráfego DNS entre cliente e servidor.

## Como funciona  
- O atacante está na rede local ou intercepta a rota.  
- Captura e altera requisições/respostas DNS.  
- Pode ser usado para phishing, injeção de anúncios, roubo de dados.

## Mitigações  
- DoH / DoT (criptografam o DNS)  
- VPN  
- Redes Wi-Fi seguras (WPA3)  
- HSTS em sites  
- Monitorar ARP spoofing ou ataques de gateway

---

# 4. DNS Hijacking (Sequestro de DNS)

## O que é  
Alteração do servidor DNS configurado no roteador, SO ou na operadora.

## Como funciona  
- Malware altera configurações locais  
- Roteador vulnerável recebe alteração de DNS  
- Operadoras podem redirecionar consultas por políticas internas

## Mitigações  
- Senha forte no roteador  
- Firmware atualizado  
- Bloquear acesso remoto ao roteador  
- Forçar DNS via firewall (empresas)  
- Usar DoH/DoT para ignorar DNS do provedor

---

# 5. DNS Amplification Attack (Amplificação DNS)

## O que é  
Um ataque DDoS onde o atacante envia requisições pequenas com IP de origem falsificado, gerando respostas muito maiores para a vítima.

Exemplos:  
- Pedido: 60 bytes  
- Resposta: 4.000+ bytes  
- Amplificação enorme

## Vetores comuns  
- ANY records  
- DNSSEC-enabled zones (respostas grandes)  
- Servidores com recursão habilitada  
- Open resolvers

## Mitigações  
- Desabilitar recursão em servidores autoritativos  
- Response Rate Limiting (RRL)  
- BCP 38 (filtrar spoofing na rede)  
- Configuração de limites de banda  
- Uso de IP Anycast para diluir carga global  
- Bloqueio de requisições suspeitas (como excessos de queries ANY)

---

# 6. DNS Tunneling

## O que é  
Uso do DNS para exfiltrar dados ou controlar malwares.

## Como funciona  
- Dados são codificados em subdomínios longos  
- Exemplo:  
  `QmFzZTY0ZGFkb3MuZXhpbGZpbmRvLmNvbQ==.dominioatacante.com`  
- O servidor autoritativo malicioso decodifica tudo

## Mitigações  
- Inspeção profunda (DPI)  
- Bloqueio de domínios suspeitos  
- Limitação de tamanho e frequência de consultas  
- Forçar uso de DNS interno  
- Monitoramento de padrões anômalos de subdomínios

---

# 7. Técnicas Modernas de Mitigação: Rate Limiting e Controle de Abuso

Para defender um servidor DNS moderno, é necessário usar técnicas de contenção contra ataques volumétricos.

A seguir, os principais mecanismos:

---

# 7.1 Rate Limiting (RRL — Response Rate Limiting)

## O que é  
Um mecanismo que bloqueia ou desacelera respostas a clientes que enviam muitas requisições suspeitas.

## Benefícios  
- Reduz impacto em ataques de amplificação  
- Evita abusos por bots/barrages  
- Protege recursão interna

## Como funciona  
- O servidor estabelece um limite como:  
  `5 respostas por segundo por IP por zona`
- Quando excedido, o servidor passa a:  
  - Dropar respostas  
  - Enviar respostas truncadas (TC=1) forçando TCP  
  - Atrasar respostas

### Parâmetros comuns:
- **limite por janela (requests/seg)**  
- **burst** (explosões temporárias permitidas)  
- **whitelists** para IPs confiáveis  
- **blacklists** para IPs maliciosos

---

# 7.2 Token Bucket

## Como funciona  
- Cada IP "ganha" tokens ao longo do tempo.  
- Cada requisição consome um token.  
- Quando acaba, requisições são rejeitadas ou atrasadas.

É ideal para:
- limitar abuso de bots  
- evitar flooding constante

---

# 7.3 Leaky Bucket

## Como funciona  
- Semelhante ao Token Bucket, mas com "vazão fixa".  
- As requisições entram no balde e vazam a uma taxa constante.  
- Se o balde enche, novos pacotes são descartados.

Serve para:
- suavizar picos de tráfego  
- prevenir explosões de requisições abusivas

---

# 7.4 Heavy Hitters / Heavy Bucket

## O que é  
Detecta IPs que excedem um volume significativo (heavy hitters) e aplica penalidades.

Típico em defesas de DDoS:
- IPs que fazem mais que X% das consultas da rede  
- IPs que consultam domínios aleatórios  
- IPs que consultam muitas zonas diferentes

## Mitigações  
- Quarentena temporária  
- Rate limiting específico por IP  
- Retirada da rota (null routing)  
- TTL forçado alto para reduzir volume

---

# 7.5 Query Name Minimization

Reduz o tamanho das consultas enviadas aos servidores DNS, diminuindo vetores de ataque e exposição de dados.

Exemplo de consulta tradicional:  
`www.exemplo.com` → Root

Com Qname Minimization:  
`.com` → Root  
`exemplo.com` → TLD  
`www.exemplo.com` → autoritativo

Isso impede:
- vazamento de consultas internas  
- exploração de dados sensíveis  
- fingerprinting de tráfego DNS

---

# 8. Medidas Gerais de Segurança em Servidores DNS (Resumo Completo)

## Configurações essenciais
- Ativar DNSSEC  
- Desativar recursão em autoritativos  
- Ativar RRL (Response Rate Limiting)  
- Filtrar consultas ANY  
- Usar mínimos TTLs para zonas críticas  
- Qname Minimization  
- Randomizar porta e ID  
- Bloquear DNS externos no firewall  
- Configurar DoH/DoT para usuários internos  
- Monitorar logs com limiares de anomalias  
- Implementar Token Bucket / Leaky Bucket  
- Aplicar Blackhole routing (null route) para IPs abusivos  
- Configurar failover e Anycast

---

# 9. Camadas de Defesa (Modelo Completo)

## Camada 1 — Rede  
- BCP 38  
- Filtrar spoofing  
- Limitar banda por IP

## Camada 2 — Firewall  
- Bloqueio de DNS externo  
- Deep Packet Inspection  
- Rate limiting

## Camada 3 — Servidor DNS  
- DNSSEC  
- RRL  
- Qname Minimization  
- Hardening geral

## Camada 4 — Clientes  
- DoH/DoT  
- Cache local  
- Bloqueio de domínios maliciosos

# Siga para o próximo tópico -> [CDNs](./CDNs.md)