# [Início](./readme.md)

# Protocolos de comunicação em redes

## NAT (Network Address Translation) 

### o que é o NAT?

è uma tecnica que permiteque vários dispositivos compartilhem um mesmo endereço de IP público, para lidar com a falta de IPv4, assim vários dispositivos em uma única rede podem se conectar a rede sem a necessidade que cada um tenha seu próprio IP público.

## TCP e UDP

- UDP organiza os dados em datagrama simples, usando apenas campos essenciais, tendo o tamanho fixo de 8bytes com 4 campos de 16 bits,  Source port, Destination Port, Length e Checksum, além disso UDP é Connectionless, o que quer dizer que não estabelece conexões  antes de enviar um pacote.
  - Usamos UDP para aplicações da baixa latência, que pode tolerar perdas, quando a ordem dos dados não é essencial, normalmente usada em jogos online, serviços de streaming ao vivo ou consultas.

- TCP realiza o handshake (SNY, SNY-ACK, ACK) para estabelecer a conexão, tem um cabeçalho mais completo que UDP, com 20bytes, podeno chegar a 60bytes, Source port, Destination port, Sequence number, Acknowledgment Number, Data offset, Reserved, Control flags, Window, Checksum, Urgent pointer, Options e padding.
  - usamos TCP caso seja essencial que os dados cheguem completos e na ordem correta, usada normalmente para carregar páginas, transferir arquivos ou qualquer sistema onde a consistência importa.

- Qual dos dois é usado na WEB?
  - HTTP usa TCP, pois em maioria dos casos é extremamente importante garantir a confiabilidade nos pacotes enviados, e atualmente HTTP3 usa QUIC que é baseada em UDP.

# siga para o Próximo tópico -> [Endereçamento de IP](./EDIP.md)