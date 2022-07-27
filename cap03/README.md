# Ferramentas de desenvolvimento e exemplos

## Uso do debug via USB e da serial para depuração/log de código


A depuração/log de código no ESP32C3 realizada via debug USB pode ser feita devido ao sistema integrado na placa, que permite a sua realização conectando-a em um conector USB-A, como se vê na figura abaixo. A partir disso, pode-se conectar a porta o conector USB na porta do computador.

![usb connection](https://www.visualmicro.com/pics/Debug-Help-ESP32C3-USB-Connections.png)


A depuração ocorre a partir do OpenOCD JTAG (Joint Test Action Group), o diagrama da figura 2 demonstra como o JTAG debugging ocorre. Na sessão “Application Loading and Monitoring” apresenta os principais recursos de software e hardware que permitem a compilação do aplicativo e mensagens de diagnósticos sejam realizados para o ESP32.

![debug diagram](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/_images/jtag-debugging-overview.jpg)

O código para realizar a escrita, compilação, carregamento e debugging pode ser feito diretamente nas linhas de comando, através do Eclipse IDE, um software disponível nas principais plataformas. 
	A forma ideal de iniciar o JTAG debugging é utilizando o ESP-WROVER-KIT, visto que já possui a interface com o JTAG e não há necessidade de utilizar um adaptador externo, basta realizar o stup do OpenOCD e configurar as target do ESP32. 
	Após a configuração das targets, basta rodar o OpenOCD, para isso abra o terminal e digite o seguinte código “openocd -f board/esp32c3-builtin.cfg”, após esse passo, realize o envio da aplicação para o debugging de forma análoga ao corriqueiro. A partir disso, se inicia o depurador, a partir da GNU debugguer (GDB), que pode ser chamado diretamente na linha de comando, ou dentro da IDE, operando de forma indireta com a ajuda da GUI, assim, consegue-se realizar o debugging do ESP32-C3.

## ESP32-C3 com IDE Arduino: instalação, uso e exemplos

Inicialmente deve-se instalar o Arduino IDE, para isso, acesse o link: https://www.arduino.cc/en/software e clique na opção do seu sistema operacional, como pode-se ver na figura abaixo.

![Imagem1.png](https://raw.githubusercontent.com/marcusvims/risc-v/main/cap03/Imagens/Imagem1.png)

Faça o download e quando finalizá-lo, acesse o arquivo executável e execute-o até que o Arduino IDE esteja disponível em sua máquina, através do atalho abaixo.

![Imagem2.png](https://raw.githubusercontent.com/marcusvims/risc-v/main/cap03/Imagens/Imagem2.png)

Ao acessar o Arduino IDE, a seguinte tela irá aparecer e basta incluir a biblioteca do ESP32 para que se consiga programá-lo e executá-lo.

![Imagem3.png](https://raw.githubusercontent.com/marcusvims/risc-v/main/cap03/Imagens/Imagem3.png)

Primeiramente deve-se ir no canto superior da tela, ir em “Arquivo” após isso, em “preferências” e uma tela se abrirá.

![Imagem4.png](https://raw.githubusercontent.com/marcusvims/risc-v/main/cap03/Imagens/Imagem4.png)

Na tela de preferências, deve-se clicar nas janelas ao lado de URLs adicionais para gerenciadores de placas. Após isso, coloque o seguinte código na janela que irá se abrir e clicar em ok. Agora, seu Arduino IDE está configurado para escrever, compilar e carregar códigos no ESP32-C3. 
https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_dev_index.json

![Imagem5.png](https://raw.githubusercontent.com/marcusvims/risc-v/main/cap03/Imagens/Imagem5.png)

![Imagem6.png](https://raw.githubusercontent.com/marcusvims/risc-v/main/cap03/Imagens/Imagem6.png)

Agora que o Arduino IDE está configurado para o ESP32-C3, vamos realizar o primeiro código, que será o piscar do LED que contém na placa. Para isso, vá em “Arquivo”=>”Exemplos”=>”Basics”=>”Blink”, como mostrado na figura abaixo.

![Imagem7.png](https://raw.githubusercontent.com/marcusvims/risc-v/main/cap03/Imagens/Imagem7.png)

O seguinte código irá aparecer, e ele faz com que o led interno na placa ESP32-C3 fique piscando a cada um segundo.

![Imagem8.png](https://raw.githubusercontent.com/marcusvims/risc-v/main/cap03/Imagens/Imagem8.png)

Por fim, para conseguir compilar o código e enviá-lo para o ESP32-C3, basta ir em “Ferramentas”=>”Placa”=>”ESP32 Arduino”=>”ESP32C3 Dev Module”.

![Imagem9.png](https://raw.githubusercontent.com/marcusvims/risc-v/main/cap03/Imagens/Imagem9.png)

Com a placa selecionada, basta clicar no sinal de check no canto esquerdo superior da tela para realizar a compilação e após compilar, basta clicar na seta ao lado, assim o código será enviado para a placa e o led piscará a cada um segundo.
	
## FreeRTOS

O FreeRTOS é um dos RTOS mais utilizados, visto que sua aplicação é livre, é possível implementá-lo sem custos em sistemas comerciais, além de que possui muitos microcontroladores que suportam esse sistema.

O FreeRTOS, semelhante a outros sistemas operacionais, possui a capacidade de executar diversas tarefas quase de forma simultânea, ou seja, há o chaveamento das tarefas a serem executadas, assim há a execução de cada uma dessas tarefas em milissegundos, permitindo que elas sejam executadas de forma rápida, ao ponto, de parecer que estão sendo realizadas ao mesmo tempo, em paralelo.
O Kernel, conhecido como o core do sistema operacional, realiza o gerenciamento do hardware, execução das tarefas e memória, a fim que tudo fique o mais optimizado possível. Ou seja, ele realiza o gerenciamento e a execução de tarefas, formando a parte do software e do hardware do componente. 

A fim de programar software com RTOS, cada funcionalidade do projeto é definida como tarefa, cada tarefa pode ser representada como uma rotina isolada. Um exemplo que se pode entender o funcionamento é um rastreador que capta uma posição GPS, envia ela em uma rede e uma luz é piscada informando sua operação. Com isso, pode-se entender que obter as posições via GPS é uma tarefa, envio dela para a rede é outra e o piscar da luz é uma terceira tarefa, cada uma sendo realizada de forma distinta, mesmo que ambas tenham que se comunicar em algum momento. 

No esp32-C3 a versão utilizada é a Vanilla FreeRTOS v10.4.3, a fim de otimizar a utilização do dual core SMP (traduzido do inglês como multiprocessamento simétrico) do módulo. Essa, é uma arquitetura de computador onde dois ou mais CPUs idênticos são conectados em uma memória compartilhada e controlado por apenas um sistema operacional. As vantagens desse sistema é que ele permite que várias tarefas sejam processadas ao mesmo tempo e isso permite também que mais de uma tarefas seja realizada em um mesmo tempo.

Assim, para utilizar o FreeRTOS no esp32-C3 primeiramente há duas funções para criar as tarefas, essa são xTaskCreate() e a xTaskCreateStatic(), sendo a primeira alocada dinamicamente na memória e a segunda alocada estaticamente. A execução das tarefas é realizada de forma semelhante. Vale ressaltar que para cada tarefa há um nível de prioridade, sendo executado inicialmente o que tem o maior nível de prioridade. 
A execução das tarefas de acordo com as prioridades no FreeRTOS do esp32-C3 é dado por cada core que possui uma “agenda” de prioridades para executar. A partir disso, vê-se que com relação às interrupções, há um sistema periódico e ele é responsável por incrementar a contagem na fila e desbloqueia qualquer tarefa que deu timed out.

Para desabilitar e habilitar as interrupções, há duas funções utilizadas que são a taskDISABLE_INTERRUPTS() e a taskENABLE_INTERRUPTS(), que desabilitam e habilitam a interrupção respectivamente.
