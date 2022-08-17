# Espressif e RISC-V [Iasmin]

## Introdução sobre a Espressif e adoção do RISC-V

A [Espressif Systems](https://www.espressif.com/en/company/about-espressif) é uma multinacional pública de semicondutores sem fábrica, de acordo com a própria Espressif, que desenvolve soluções seguras, robustas, AIoT (inteligência artificial e Internet das Coisas) e com baixo consumo de energia de comunicação sem fio de ponta desde 2008, sendo a líder no mercado de inteligência AIoT atual. 

Ela foi responsável por criar a série de chips e módulos inteligentes e versáteis ESP8266, ESP32, ESP32-C, ESP32-S e ESP32-H, com tecnologia e [soluções de código aberto](https://en.wikipedia.org/wiki/Open-source_license), o que significa que usuários são capazes de alterar o código-fonte ou o projeto de acordo com suas necessidades de maneira gratuita. Assim, é possível perceber que a Espressif produz chips com necessidades específicas, ao invés de produzir um modelo único responsável por atender a uma ampla gama de demandas. 

Na família do ESP32-C, temos o ESP32-C3, uma série que foi desenvolvida para atender a aplicações com requisitos simples, com otimização do uso de memória. Ele permite o desenvolvimento de aplicativos sem a necessidade de um host MCU e possui um nível de segurança de proteção contra riscos de um ambiente conectado elevado, impedindo que ocorram ataques ao dispositivo. 

O ESP32-C3 possui WiFi 2.4GHz e Bluetooth LE (low energy) 5.0 de longo alcance integrados, objetivando aprimorar tanto a experiência do usuário com o chip, quanto os diagnósticos de campo. Por esse motivo, também optou-se por baseá-lo em [RISC-V](https://riscv.org/wp-content/uploads/2017/05/riscv-spec-v2.2.pdf), uma [arquitetura](https://en.wikipedia.org/wiki/RISC-V#Rationale),  de conjunto de instruções (ISA) de carga-armazenamento – que separa as instruções em acesso à memória e operações ALU – de padrão aberto e totalmente virtualizável, desenvolvida na Universidade da Califórnia, Berkeley, com o intuito de utilização acadêmica e implantação eficiente para vários estilos de microarquitetura e tecnologia de implementação sem cobrança de royalties, até mesmo para indústrias, diferenciando-se de ISAs pré-existentes.

## Processador ESP32-C3 com RISC-V

#### [Principais características](https://www.espressif.com/sites/default/files/documentation/esp32-c3_datasheet_en.pdf)

É um microprocessador de núcleo único, baseado em RISC-V, de 32 bits com pipeline de quatro estágios que opera em até 160 MHz (frequência de clock), RV32IMC ISA, operadores de multiplicação e divisão de 32 bits, 32 interrupções vetorizadas de acordo com 7 categorias de prioridade, 8 pontos de interrupção e observação de hardware, 16 áreas PMP e JTAG para depuração. 

 Também conta com um rico [conjunto de interfaces periféricas]( https://www.youtube.com/watch?v=eprycXXUmo4) ( SPI, Dual SPI, Quad SPI e QPI, possibilitando a conexão com interfaces externas como o flash, e com 22 pinos GPIOs programáveis com suporte pra ADC, UART, I2C, I2S, SPI, RMT, TWAI e PWM, tornando-o aplicável em vários cenários, como em eletrônicos de consumo e automação industrial. 
 
Além disso, ele porta SRAM de 400 KB para dados e comandos – 16 KB para cache (somente para leitura) e 384 KB de ROM no chip, para inicialização e tarefas principais – responsável por manter seu funcionamento gastando menos energia e possibilitar que o chip lide com uma ou duas conexões TLS com Bluetooth ativo integralmente e com aplicação razoável. Somado a isso, tem uma divisão para a memória de instrução e dados, maximizando de maneira efetiva a memória utilizável (8 KB para memória RTC FAST e 4 Kbit de eFuse). 

Por meio de um desempenho de RF de última geração, que inclui interruptor de antena, balun de RF, amplificador de potência, amplificador de baixo ruído (LNA), filtro, unidade de gerenciamento de energia e circuitos de calibração, o ESP32-C3 integra a implementação de tecnologias e se ajusta a mudanças externas ou remove imperfeições de um circuito externo.

#### [Recursos de segurança](https://www.filipeflop.com/blog/apresentando-novo-mcu-esp32-c3-da-familia-espressif/)

O chip conta com o secure boot, que permite somente a utilização de aplicações confiáveis, de acordo com o padrão RSA-3072, que se completa em 100ms, protegendo até mesmo dispositivos ligados de modo imediato. Portanto, o chip foi desenvolvido para ter a capacidade de suprir as necessidades de aparelhos conectados tais como segurança, disponibilidade de Bluetooth de baixa energia e memória suficiente.

Somado a isso, esse chip possui encriptação de flash, baseada em AES-128-XTS. Na flash, são encriptados firmware e dados de configuração, que depois são suportados pelo seu controlador, protegendo os dados do ESP32-C3. Ainda, porta assinatura digital e HMAC periférico, responsáveis por garantir que a identidade do chip seja protegida, mesmo em casos de explorações de vulnerabilidade de software, e um world controller, permitindo que haja a separação de dois ambientes, destinados a uma execução confiável (TEE) por meio de um isolamento.

#### [Encapsulamento e pinos](https://www.espressif.com/sites/default/files/documentation/esp32-c3_datasheet_en.pdf) 

O ESP32-C3 porta 33 pins, que ordenados numericamente, com suas respectivas funções são: 1, entrada e saída RF; 2 e 3, fontes de alimentação analógica; 4, GPIO0; 5, GPIO1; 6, GPIO2; 7, habilitar (nível alto) ou desligar (nível baixo) o chip; 8, GPIO3; 9, GPIO4; 10, GPIO5; 11, fonte alimentação para RTC; 12, GPIO6; 13, GPIO7; 14, GPIO8; 15, GPIO9; 16, GPIO10; 17, fonte de alimentação para CPU IO; 18, GPIO11; 19, GPIO12; 20, GPIO13; 21, GPIO14; 22, GPIO15; 23, GPIO16; 24, GPIO17; 25, GPIO18 (USB); 26, GPIO19 (USB); 27, GPIO20; 28, GPIO21; 29, saída do cristal externo; 30, entrada do cristal interno; 31 e 32, fontes de alimentação analógica; e, por fim, 33, o terra.

![Pins ESP32-C3](https://techoverflow.net/wp-content/uploads/2022/02/ESP32-C3-Pinout.svg)

#### [Flexibilidade de configuração de pinos](https://www.espressif.com/sites/default/files/documentation/esp32-c3_datasheet_en.pdf)

A depender de configurações fixas, os pinos podem ter suas funções alteradas, de acordo com a tabela abaixo, em que as funções padrão no modo de inicialização SPI estão indicadas em negrito:

![flex](https://user-images.githubusercontent.com/42560173/185243467-44e38e0e-ac40-410c-bbbe-a581a03d9200.png)
![flex2](https://user-images.githubusercontent.com/42560173/185243489-115ec504-7a0c-4dae-8a6f-95d52453d311.png)

#### Características de comunicação

###### Wifi

O chip possui um [subsistema integrado completo de Wifi](https://www.espressif.com/sites/default/files/documentation/esp32-c3_datasheet_en.pdf) de 2.4GHz, capaz de suportar modo Estação, modo SoftAP, uma combinação desses dois modos e, ainda, modo promíscuo. Esse subsistema tem compatibilidade com IEEE 802.11 b/g/n, suporta uma largura de banda de 20 MHz e 40 MHz, tem fluxo espacial único RX STBC, taxa de dados de no máximo 150 Mbps, potência de transmissão regulável e uma diversidade de antenas com um interruptor RF externo (controlado por GPIOs), que faz a seleção da antena visando reduzir os impactos das imperfeições do canal.

Além disso, o chip implementa o protocolo MAC Wi-Fi 802.11 b/g/n completo, que suporta um conjunto de serviços básicos (BSS) STA e operações SoftAP sob a Função de Controle Distribuído (DCF). Visando minimizar o período de serviço ativo, é realizado um gerenciamento de energia automático, garantindo que a interação com o host seja mínima. Algumas funções de baixo nível são aplicadas também de maneira automática, como a infraestrutura BSS nos modos Station, SoftAP, Station + SoftAP e promíscuo, a multimídia Wifi (WMM), a oportunidade de transmissão (TXOP) e o monitoramento automático de beacons (hardware TSF).

###### BLE

Um [subsistema Bluetooth](https://www.filipeflop.com/blog/apresentando-novo-mcu-esp32-c3-da-familia-espressif/) LE 5.0 de longo alcance, uma das características mais importantes do chip, permite ao ESP32-C3 maior simplicidade de reconhecimento, controle de dispositivos no ambiente local e de integração à rede em comparação a quando existe somente o Wifi como um mecanismo de comunicação com servidores, que não é capaz de entregar um feedback confiável ao integrar-se à rede, além da complexidade de integrações iOS e Android. 

Essa versão de longo alcance, melhorando-o em quase 100 metros, torna o dispositivo capaz de realizar aplicações em ambientes de grande porte, diferenciando-se das versões anteriores, que possuíam alcance menor. O chip também suporta recursos do protocolo de Bluetooth LE Mesh, facilitando o controle e comunicação com outros dispositivos BLE em uma rede local e integra, um controlador de camada de link de hardware, um bloco RF/modem e uma vasta pilha de protocolos de software. 

#### [Principais periféricos](https://www.espressif.com/sites/default/files/documentation/esp32-c3_datasheet_en.pdf) 

###### Periféricos analógicos

Os principais periféricos analógicos são dois conversores ADC (analógico-digital) SAR de 12 bits, em que o ADC1 mede até 5 canais e o ADC2 somente 1 e um sensor de temperatura na faixa de -40 a 125 ºC, que detecta mudanças de temperaturas internas ao chip, normalmente maior que a de ambiente operacional.

###### Periféricos digitais

- Interfaces de entrada e saída de uso geral (GPIOs)

Por sua vez, os principais periféricos digitais são 22 pinos GPIOs bidirecionais, não inversores e com 3 estados, sendo multiplexáveis com funções como UART, que podem ser usados para funções que configuram registros ou analógicas, como ADC. Eles possuem pull-up ou down elegíveis e podem ser configurados como entrada, realizando a leitura do valor de entrada por meio do registrador do software ou gerando interrupções de CPU ativadas por nível. Um outro modo de configuração para os GPIOs é em operações de baixa potência, mantendo o estado do mesmo. 

Ainda, esses periféricos digitais utilizam um MUX de entrada e saída e uma matriz GPIO de modo a permitir que as entradas e saídas tenham capacidade de configuração elevada, podendo ser configurados por meio de qualquer pino, para o caso das entradas ou para qualquer pino, para saídas.

- Interfaces periféricas seriais (SPIs)

O chip possui 3 SPIs, a SPI0, SPI1 e SPI2, onde há transferência de dados em unidade de byte, em que as duas primeiras podem operar em modo de memória, com leitura ou gravação STR de até 4 linhas (frequência de clock no máximo de 120MHz) e a última em modo de uso geral, podendo se conectar ao GDMA e operar como mestre ou escravo, com comunicação de duas linhas full-duplex e de uma, duas ou quatro linhas half-duplex, e frequência, polaridade e fase de clock configuráveis.  Operando como mestre, a frequência máxima de clock é 80 MHz. Operando como escravo, ela é de 60 MHz.

- Interface I2C

O chip tem uma interface de barramento I2C flexível, controlada pelos registradores de instrução, que também opera como mestre e escravo, suportando 100 Kbit/s no modo padrão e 400 Kbit/s no modo rápido, chegando a 800 Kbit/s com restrição pela pull-up SCL e SDA. Essa interface tem modo de endereçamento de 7 e 10 bits, que pode ser duplo. 

- Interface I2S

Além disso, o ESP32-C3 conta com uma interface I2S padrão (mestre/escravo), que se conecta ao controlador GDMA, operando em full-duplex ou half-duplex, configurável para comunicação serial de 8, 16, 24 ou 32 bits, suportando um intervalo de 10 KHz a 40 MHz para frequência de clock, TDM PCM, alinhamento TDM MSB, TDM padrão e interface PDM TX. 

- Transmissor receptor assíncrono universal (UART)

O chip comporta duas interfaces UART, a UART0 e UART1, com suporte para comunicação assíncrona (RS232 e RS485), com velocidade de no máximo 5 Mbps, e suporte IrDA. Os controladores UART permitem que seja realizado o controle do fluxo de hardware (sinais CTS e RTS) e de software (XON e XOFF). Essas interfaces se conectam ao GDMA através do UHCI0.

- Periférico de controle remoto (RMT)

Ademais, o chip possui um RMT, cuja capacidade de suporte é de dois canais de transmissão remota infravermelha e dois de recepção da mesma, controlando a forma de onda de pulso através do software. Os canais dividem um bloco de memória de 192 x 32 bits, responsável por fazer o armazenamento, transmissão ou recepção da forma de onda.

- Controlador PWM LED

É um controlador capaz de gerar formas de ondas digitais e independentes em 6 canais, com fontes de clocks diversificadas, como clock APB e clock principal de cristal externo e com períodos e ciclos de trabalho (precisão de no máximo 18 bits) configuráveis. O ciclo de trabalho pode ter um aumento ou redução gradual, sendo usado no gerador do gradiente de cores do LED RGB. Esse controlador é capaz, também, de operar enquanto a CPU está no modo de suspensão leve.

- Controlador DMA geral (GDMA)

O GDMA possui 3 canais de transmissão e 3 canais de recepção, todos independentes, com capacidade de acesso à RAM interna, compartilhados por periféricos (SPI2, UHCI0, I2S, AES, SHA e ADC) por meio do recurso DMA. Ele realiza a implementação de acordo com níveis de prioridade entre esses canais, que pode ser configurados. Então, com o auxílio de listas associadas, ele faz o controle da transferência de dados, que ocorre em um sentido bidirecional entre periféricos e memória, a uma velocidade elevada. 

- Controlador USB Serial/JTAG

	Tem como característica uma porta serial virtual CDC-ACM, funcionalidade do adaptador JTAG, que dá instruções para que seja realizada a ***depuração da CPU***, e programação flash, que pode ser interna ou externa. Ele é compatível com USB 2.0 de velocidade total, tendo como velocidade de transferência máxima 12 Mbit/s, que não é de alta velocidade (480 Mbit/ s) e contém um USB PHY integrado.
  
- Controlador TWAI®

Por fim, o chip porta um controlador TWAI®, cuja compatibilidade é com o protocolo ISO 11898-1 (Especificação CAN 2.0). Esse controlador tem formato de quadro padrão (ID com 11 bits) e estendido (29 bits), taxas de bits que podem alternar entre 1 Kbit/s e 1 Mbit/s e 3 modos de operação: normal, escuta e auto teste (sem que seja necessária uma confirmação). Além disso, ele possui FIFO de recepção de 64 bytes, filtro de aceitação com modo simples e duplo e a capacidade de detectar e tratar erros, por meio de contadores de erros, da configuração do limite de interrupção de erro e da captura de erro de código e de arbitragem perdida.

#### Características elétricas: consumo em diversos modos, tensão de operação, latências, etc

#### Hardware mínimo com ESP32-C3

https://espressif.com/sites/default/files/documentation/esp32-c3_hardware_design_guidelines_en.pdf

#### Módulos baseados em ESP32-C3

A espressif lançou diferentes [módulos baseados em ESP32-C3](https://espressif.com/en/products/modules), todos com 15 GPIOs, 4MB de flash e para uso geral, sendo indicados para residências inteligentes e assistência médica, por exemplo.  Um deles é o [ESP32-C3-MINI-1](https://www.espressif.com/sites/default/files/documentation/esp32-c3-mini-1_datasheet_en.pdf), que possui tamanho reduzido (13,2×16,6×2,4 mm), 53 pinos, antena PCB e os chips ESP32-C3FH4 e ESP32-C3FN4 incorporados. Os termos ‘H’ e ‘N’ simbolizam, respectivamente, temperatura alta e normal, o que indica que eles suportam uma temperatura ambiental operacional máxima de 105º C e 85ºC, respectivamente. Por sua vez, o termo ‘F’ indica flash. 

Concomitante a ele, temos o ESP32-C3-MINI-1U, com 53 pinos, diferenciando-se por ter um tamanho ainda mais reduzido (13,2×12,5×2,4 mm), um conector U.FL para antena externa (IPEX) e os chips ESP32-C3-MINI-1U-H4 e ESP32-C3-MINI-1U-N4, que também suportam uma temperatura ambiental máxima, de 105º C e 85ºC, respectivamente. 

Além disso, existe o [ESP32-C3-WROOM-02](https://www.espressif.com/sites/default/files/documentation/esp32-c3-wroom-02_datasheet_en.pdf), cujas dimensões são 18.0 × 20.0 × 3.2 mm, dispõe de 19 pinos, antena PCB e dos chips ESP32-C3-WROOM-02-H4 e ESP32-C3-WROOM-02-N4 (105º C e 85ºC). Por fim, o ESP32-C3-WROOM-02U, também com 19 pinos, possui 18.0 × 14.3 × 3.2 mm, um conector U.FL para antena externa (IPEX) e os chips ESP32-C3-WROOM-02U-H4 e ESP32-C3-WROOM-02U-N4 (105º C e 85ºC).
  
#### Kits de desenvolvimento oficiais da Espressif

#### Outros kits
