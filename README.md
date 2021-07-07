# ESP8266-Caixa-dagua

### Resumo

Nesse projeto vamos implementar um Sensor de Nível de agua de uma caixa-dágua remoto usando ESP8266 na forma ESP01. 
Vamos usar dois sensores de nível dágua discretos, um posicionado no fundo da caixa, que detectará se a caixa está vazia e um outro no topo da caixa para detectar se ela estará cheia.

Esses sensores serão conectados ai ESP8266, que transmitirá esses dados usando BLE (Bluetooth Low Energy) para um ESP32 que será a central de comando da casa e que usará
os dados provenientes dos sensores para ligar e desligar a bomba-d'agua que enche a caixa.

Para alimentação do ESP8266 da caixa-d'agua, usaremos um esquema com um pequeno painel solar, uma bateria, e os devidos CIs para controlar o painel solar, a bateria e 
a fonte de alimentação do ESP. Cujo hardware foi projetado usando o software Altium Designer.

No ESP8266- ESP01, temos 8 pinos disponíveis, como podemos ver no esquema abaixo.
Precisamos de 2 pinos para serem usados como INPUTS para os sensores, os pinos GPIO0 e GPIO2 são usados para seleção do modo de boot do ESP, então usar esses pinos
é uma tarefa complicada, pois teríamos que garantir nível lógico ALTO nesses pinos na inicialização do ESP. Ao invés deles, vamos usar os pinos RX e TX,
sabendo que eles podem ser configurados para serem usados como INPUTS, já que só precisamos deles para a programação inicial do ESP, e não para o funcionamento a 
longo prazo.

Nesse projeto temos preocupações a mais com o uso de energia do ESP, pois a noite e em dias mal-ensolarados, ficaremos totalmente dependentes de uma boa carga na bateria para
a operação do sistema. Assim, Além de escolher o BLE para transmissão dos dados, vamos usar a função DeepSleep para colocar o ESP em um estado de baixíssimo consumo de energia
quando não estivermos coletando ou transmitindo os dados. Na placa ESP-01, precisamos de fazer uma adaptação de Hardware para conseguir usar a função DeepSleep.
É necessário conectar o GPIO16 do CI no RESET da placa, como mostrado na figura abaixo. 

Projetar Sistemas Embarcados que são Alimentados por baterias trazem um desafio a mais no projeto, pois todo o Hardware e Software do sistema foi projetado pensando em 
consumir o mínimo de energia possível.
