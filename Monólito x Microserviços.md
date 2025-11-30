# Monólito vs Microserviços

A arquitetura de software pode ser organizada de formas diferentes, e duas das mais comuns são **Monólito** e **Microserviços**. Cada uma tem vantagens, desvantagens e usos ideais.

---

# Arquitetura Monolítica

Na arquitetura **monolítica**, toda a aplicação é construída como **um único bloco**, contendo:

- Front-end (opcionalmente)
- Lógica de negócio
- Autenticação
- Processamento
- Integrações
- Banco de dados
- Todos os módulos e funcionalidades dentro do mesmo projeto

## Características:
- Um único código-fonte
- Uma única aplicação para rodar e escalar
- Tudo é empacotado junto

## Vantagens:
- Simples de desenvolver e começar
- Menos complexidade inicial
- Deploy mais fácil (uma aplicação só)
- Debug e testes simples

## Desvantagens:
- Conforme cresce, fica difícil de manter
- Escalabilidade limitada (tudo escala junto, mesmo o que não precisa)
- Uma falha pode derrubar o sistema inteiro
- Equipes grandes podem se atrapalhar no mesmo código-base
- Atualizações exigem deploy da aplicação inteira

---

# Arquitetura de Microserviços

Na arquitetura de **microserviços**, a aplicação é dividida em **vários serviços independentes**, cada um responsável por uma função específica.

Exemplos:
- Serviço de usuários
- Serviço de pagamentos
- Serviço de pedidos
- Serviço de notificações

Cada serviço tem:
- Seu próprio código
- Suas próprias regras
- Seu próprio banco (ou schema)
- Seu ciclo de deploy
- Sua escalabilidade independente

## Características:
- Serviços pequenos, isolados e independentes
- Comunicação via API (REST, gRPC, mensageria etc.)
- Cada serviço pode usar linguagens e bancos diferentes

## Vantagens:
- Escalabilidade individual (escala só quem precisa)
- Resiliência maior: falha de um serviço não derruba tudo
- Atualizações independentes
- Equipes podem trabalhar em serviços diferentes
- Melhor para sistemas grandes e complexos

## Desvantagens:
- Muito mais complexidade
- DevOps obrigatório (CI/CD, monitoramento, logs distribuídos…)
- Comunicação entre serviços pode gerar latência
- Dificuldade de testar o sistema inteiro
- Gerenciamento de versão entre serviços

---

# Quando usar Monólito?

- Projetos pequenos e médios
- Startups no início
- Equipes pequenas
- Quando você quer velocidade para lançar funcionalidades
- Quando a complexidade não justifica microserviços

---

# Quando usar Microserviços?

- Sistemas grandes e distribuídos
- Altíssimo tráfego
- Muitas equipes desenvolvendo ao mesmo tempo
- Necessidade de escalar apenas partes específicas
- Requisitos de alta disponibilidade e resiliência

---

# Resumo geral

| Aspecto | Monólito | Microserviços |
|--------|----------|----------------|
| Estrutura | Uma aplicação | Várias aplicações independentes |
| Escalabilidade | Do sistema inteiro | Por serviço |
| Complexidade | Baixa | Alta |
| Deploy | Único | Vários, independentes |
| Equipes | Pequenas | Muitas equipes trabalhando separadamente |
| Falhas | Pode derrubar tudo | Isoladas por serviço |
| Uso ideal | Projetos simples/médios | Sistemas grandes/complexos |

---

# Conclusão

> Monólito é simples e rápido para começar.  
> Microserviços são mais poderosos e escaláveis, mas muito mais complexos.

# Siga para o próximo tópico -> [DNS](./DNS.md)