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

![Imagem1.png]("cap03/Imagens/Imagem1.png")

Faça o download e quando finalizá-lo, acesse o arquivo executável e execute-o até que o Arduino IDE esteja disponível em sua máquina, através do atalho abaixo.

![Imagem2.png]("cap03/Imagens/Imagem2.png")

Ao acessar o Arduino IDE, a seguinte tela irá aparecer e basta incluir a biblioteca do ESP32 para que se consiga programá-lo e executá-lo.

![Imagem3.png]("cap03/Imagens/Imagem3.png")

Primeiramente deve-se ir no canto superior da tela, ir em “Arquivo” após isso, em “preferências” e uma tela se abrirá.

![Imagem4.png]("cap03/Imagens/Imagem4.png")

Na tela de preferências, deve-se clicar nas janelas ao lado de URLs adicionais para gerenciadores de placas. Após isso, coloque o seguinte código na janela que irá se abrir e clicar em ok. Agora, seu Arduino IDE está configurado para escrever, compilar e carregar códigos no ESP32-C3. 
https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_dev_index.json

![Imagem5.png]("cap03/Imagens/Imagem5.png")

![Imagem6.png]("cap03/Imagens/Imagem6.png")

Agora que o Arduino IDE está configurado para o ESP32-C3, vamos realizar o primeiro código, que será o piscar do LED que contém na placa. Para isso, vá em “Arquivo”=>”Exemplos”=>”Basics”=>”Blink”, como mostrado na figura abaixo.

![Imagem7.png]("cap03/Imagens/Imagem7.png")

O seguinte código irá aparecer, e ele faz com que o led interno na placa ESP32-C3 fique piscando a cada um segundo.

![Imagem8.png]("cap03/Imagens/Imagem8.png")

Por fim, para conseguir compilar o código e enviá-lo para o ESP32-C3, basta ir em “Ferramentas”=>”Placa”=>”ESP32 Arduino”=>”ESP32C3 Dev Module”.

![Imagem9.png]("cap03/Imagens/Imagem9.png")

Com a placa selecionada, basta clicar no sinal de check no canto esquerdo superior da tela para realizar a compilação e após compilar, basta clicar na seta ao lado, assim o código será enviado para a placa e o led piscará a cada um segundo.
	
