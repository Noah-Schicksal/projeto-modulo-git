# [Início](./readme.md)

# IPv4, IPv6 e NAT

A comunicação na internet depende de endereços IP. Esses endereços identificam dispositivos e permitem que dados trafeguem entre computadores, servidores e redes.  
Atualmente convivemos com **IPv4**, **IPv6** e **NAT**, cada um com um papel importante.

---

# IPv4

O **IPv4 (Internet Protocol version 4)** é a 4ª versão do protocolo IP e o mais utilizado no mundo.

## Características
- Endereços de **32 bits**
- Formato: `x.x.x.x` (ex: `192.168.0.15`)
- Total de endereços possíveis: **4,29 bilhões**
- Criado em 1981

## Problema: falta de endereços
Com smartphones, PCs, smart TVs, IoT etc, o IPv4 **acabou**.  
Isso gerou a necessidade de soluções temporárias — como o **NAT** — e a criação do IPv6.

---

# IPv6

O **IPv6 (Internet Protocol version 6)** é a evolução do IPv4, criado para substituir o protocolo antigo.

## Características
- Endereços de **128 bits**
- Formato: hexadecimal, separado por “:”  
  Ex: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
- Total de endereços: **340 undecilhões**  
  (número absurdamente maior que o IPv4)
- Suporte nativo a:
  - Autoconfiguração
  - Segurança (IPsec)
  - Roteamento mais eficiente

## Por que ainda não é totalmente usado?
- Equipamentos antigos
- ISPs demorando para migrar
- Infraestruturas legadas
- Custo de atualização

Hoje vivemos numa internet **dual-stack**: IPv4 e IPv6 juntos.

---

# NAT (Network Address Translation)

O **NAT** é uma técnica usada para “estender” o IPv4.  
Ele permite que vários dispositivos **compartilhem um único IP público**.

Exemplo típico:  
No seu roteador:

- Dispositivos da sua casa usam IPs privados:
  - `192.168.0.10`
  - `192.168.0.11`
  - `192.168.0.20`

- Todos saem para a internet usando **um único IP público** do seu provedor:
  - `187.55.xxx.xxx`

## ✦ Por que o NAT existe?
Porque o IPv4 não tinha endereços suficientes para todos os dispositivos.

## ✦ Como o NAT funciona?
1. Seu dispositivo envia um pacote para a internet usando seu IP privado.  
2. O roteador substitui o IP privado por **seu IP público**.  
3. Quando a resposta chega, o roteador sabe qual dispositivo interno pediu e redireciona o pacote.

Isso é chamado de **mascaramento**.

## Tipos de NAT
- **NAT estático** → um IP privado mapeado para 1 IP público.
- **NAT dinâmico** → um IP privado pega qualquer IP público livre.
- **PAT (Port Address Translation)** → várias máquinas compartilham 1 IP público (o mais comum).

---

# Relação entre IPv4, IPv6 e NAT

### IPv4
- Poucos endereços → esgotou

### NAT
- Solução paliativa para prolongar a vida do IPv4  
- Permite compartilhar 1 IP público entre vários dispositivos

### IPv6
- Solução definitiva para o problema  
- Todos podem ter IP público próprio  
- Elimina a necessidade de NAT (em teoria)

---

# Comparação rápida

| Protocolo | Tamanho IP | Endereços possíveis | Necessita NAT? | Formato |
|----------|------------|---------------------|----------------|---------|
| **IPv4** | 32 bits | 4,29 bilhões | Sim | 192.168.0.1 |
| **IPv6** | 128 bits | 340 undecilhões | Não | 2001:db8::1 |

---


- **IPv4** → protocolo antigo, poucos endereços  
- **NAT** → solução temporária para estender o IPv4  
- **IPv6** → substituto do IPv4, praticamente ilimitado  

> O NAT existe por causa da escassez de IPv4.  
> O IPv6 existe para acabar com a escassez.

# Siga para o próximo tópico -> [Serviços e Aplicações](./serviços_e_aplicações.md)