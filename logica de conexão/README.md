# Lógica de conexão OBD-II

Esta pasta é destinada à comunicação com adaptadores OBD-II, à leitura de parâmetros do veículo e ao tratamento de desconexões e erros de comunicação.

## Estado atual

O protótipo de conexão existente no projeto usa a biblioteca `python-OBD` (`obd==0.7.3`). No estado atual deste repositório, o código do conector ainda não está versionado nesta pasta e não envia leituras ao dashboard. A interface continua usando dados de demonstração.

## Fluxo do protótipo

1. Verifica se o Bluetooth parece estar ativo. O script tenta consultar ferramentas do Windows ou do Linux; essa verificação é um indício, não prova que o adaptador OBD esteja conectado.
2. No Linux, procura algumas portas seriais comuns, como `/dev/rfcomm0` e `/dev/ttyUSB0`, e tenta abrir a conexão por elas. Se não encontrar uma porta, deixa a biblioteca tentar a conexão padrão.
3. Faz até cinco tentativas de conexão, com intervalo de cinco segundos entre tentativas sem sucesso.
4. Se conectar, mostra o identificador e o nome do protocolo detectado, quando disponíveis.
5. Encerra a conexão ao terminar.

O adaptador precisa ser compatível com OBD-II e estar pareado/disponível no sistema; a ignição também deve estar na condição necessária para o veículo responder. A implementação pode se comportar de forma diferente conforme adaptador, sistema operacional e veículo.

## Próximas etapas de integração

- Isolar a conexão e o ciclo de vida do adaptador num módulo testável.
- Consultar apenas comandos suportados pelo veículo e validar os valores retornados.
- Encaminhar leituras estruturadas (parâmetro, valor, unidade, horário e estado de validade) para a camada de aplicação.
- Definir como o dashboard receberá os dados, por exemplo, por uma API local ou serviço intermediário. O navegador não deve tentar acessar diretamente uma porta Bluetooth/serial sem uma arquitetura compatível.
- Tratar desconexões, tempos limite, reconexão e encerramento sem bloquear a interface.
- Guardar logs técnicos sem registrar dados pessoais desnecessários.

## Limitações importantes

Nem todo veículo oferece os mesmos parâmetros, e nem todo adaptador fornece os mesmos dados. Itens como pressão individual dos pneus ou estado detalhado da bateria podem exigir TPMS, sensores ou ferramentas específicas. A ausência de uma leitura não deve ser interpretada como falha.

O conector não deve apagar códigos, comandar sistemas do veículo ou apresentar uma leitura como diagnóstico confirmado. O foco inicial é leitura e apresentação informativa; inspeção profissional continua necessária para confirmar problemas.