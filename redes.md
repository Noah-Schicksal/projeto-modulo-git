## Redes

[Início](./readme.md)

### Topologias

existem vários tipos de topologias, entre elas

- Topologia de estrela
  - normalmente utilizadas por ISPs para conectar residencias a internet, todos os dispositivos estão conectados a um hub
    se um nó falhar o sistema pode continuar funcionando normalmente, porém se o hub falhar, todo o sistema é comprometido.
- Topologia de malha
  - nessa topologia cada dispositivo é conectado diretamente a todos os outros dispositivos, assim cada nó tem um caminho
    dedicado completamente ou pacialmente aos outros nós, é altamente confiavel, pois se um nó falha, os dados podem ter dezenas ou até centenas decaminhos alternativos para seguir, é majoritariamente usada pelos backbones de internet.
- topologia de anel
  - cada dispositivo é conectado no dispositivo seguinte e assim consecutivamente, até que o ultimo dispositivo se conecta
    no primeiro não oferece alta confiabilidade, porém tem um custo bem mais baixo em relação a outros tipos de topologia, se um nó falhar, as informações podem seguir o caminho contrário.
- topologia de barra
  - pode se imaginar como vários dispositivos com uma unica conexão através de uma unica barra, se um dos dispositivos falha
    não é um problema geral, porém esse dispositivo não consegue enviar ou receber dados da rede, já se o caminhi principal a qual todos os dispostivos falhar, toda a rede falha.

### Internet, Intranet e Extranet

- A interne é pública, acessivel para qualquer um desde que exista conexão.
- A intrenet é uma rede interna privada, sendo normalmente utilizada por empresas e usada para compartilhas informações
somente entre a equipe.
- A extranet é uma rede privada que permite acesso a usuários externos.

### AJax

Ajax revolucionou a forma como as páginas eram vistas na internet, permitindo atualizar conteúdo sem a necessidade de carregar uma página inteira.

## Siga pra o Próximo tópico -> [Protocolos de comunicação em redes](./PCR.md)