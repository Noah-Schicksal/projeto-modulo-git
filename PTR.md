# [Início](./readme.md)

# PTR — Registro Pointer em DNS

## O que é  
O **PTR (Pointer Record)** é um tipo de registro DNS usado para **resolução reversa de IP para nome de domínio**.  
Ou seja, ao invés de converter um nome em IP (como A ou AAAA), ele converte um **IP em nome de host**.

Exemplo:  
- A: `www.exemplo.com → 192.0.2.1`  
- PTR: `192.0.2.1 → www.exemplo.com`

---

## Para que serve

1. **Verificação de identidade de servidores**  
   - Usado em servidores de e-mail para confirmar que o IP de envio corresponde a um domínio legítimo.  
   - Evita que e-mails sejam marcados como spam.

2. **Auditoria e troubleshooting**  
   - Administradores podem identificar rapidamente o nome associado a um IP.  
   - Útil em logs de firewall, proxies e servidores.

3. **Segurança**  
   - Confirma que o IP de origem é confiável.  
   - Pode ser usado em conjunto com SPF, DKIM e DMARC para autenticação de e-mail.

---

## Como funciona

1. A consulta começa com o **IP** que precisa ser resolvido.  
2. O IP é **invertido** e concatenado com o domínio especial `.in-addr.arpa` (para IPv4) ou `.ip6.arpa` (para IPv6).  

Exemplo IPv4:  
- IP: `192.0.2.1`  
- Consulta PTR: `1.2.0.192.in-addr.arpa`  

Exemplo IPv6:  
- IP: `2001:db8::567:89ab`  
- Consulta PTR: `b.a.9.8.7.6.0.0.0.0.0.0.0.0.0.0.0.0.0.0.8.b.d.0.1.0.0.2.ip6.arpa`

3. O **servidor autoritativo da zona inversa** retorna o **nome do host** correspondente.

---

## Diferenças entre PTR e A/AAAA

| Tipo de registro | Direção | Uso principal |
|-----------------|---------|---------------|
| A               | Nome → IP | Resolutivo normal de host IPv4 |
| AAAA            | Nome → IP | Resolutivo normal de host IPv6 |
| PTR             | IP → Nome | Resolução reversa, autenticação e auditoria |

---

## Configuração típica

- PTR deve ser configurado no **provedor de IP** (ISP ou bloco de IP público).  
- Domínios internos podem ter PTRs em zonas privadas (`.arpa`) gerenciadas pelo servidor DNS interno.

---

## Observações importantes

- Um PTR **não é obrigatório**, mas é altamente recomendado para e-mail e auditoria.  
- Um IP geralmente deve ter **apenas um PTR** apontando para um domínio principal.  
- Para múltiplos domínios hospedados no mesmo IP, o PTR aponta para o domínio principal e os demais usam A/AAAA normalmente.

# Siga para o próximo tópico -> [Balanceamento de carga](./Balanceamento%20de%20carga.md)
