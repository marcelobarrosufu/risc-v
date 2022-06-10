# Ferramentas de desenvolvimento e exemplos

## Uso do debug via USB e da serial para depuração/log de código


A depuração/log de código no ESP32C3 realizada via debug USB pode ser feita devido ao sistema integrado na placa, que permite a sua realização conectando-a em um conector USB-A, como se vê na figura abaixo. A partir disso, pode-se conectar a porta o conector USB na porta do computador.

![usb connection](https://www.visualmicro.com/pics/Debug-Help-ESP32C3-USB-Connections.png)


A depuração ocorre a partir do OpenOCD JTAG (Joint Test Action Group), o diagrama da figura 2 demonstra como o JTAG debugging ocorre. Na sessão “Application Loading and Monitoring” apresenta os principais recursos de software e hardware que permitem a compilação do aplicativo e mensagens de diagnósticos sejam realizados para o ESP32.

![debug diagram](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/_images/jtag-debugging-overview.jpg)

O código para realizar a escrita, compilação, carregamento e debugging pode ser feito diretamente nas linhas de comando, através do Eclipse IDE, um software disponível nas principais plataformas. 
	A forma ideal de iniciar o JTAG debugging é utilizando o ESP-WROVER-KIT, visto que já possui a interface com o JTAG e não há necessidade de utilizar um adaptador externo, basta realizar o stup do OpenOCD e configurar as target do ESP32. 
	Após a configuração das targets, basta rodar o OpenOCD, para isso abra o terminal e digite o seguinte código “openocd -f board/esp32c3-builtin.cfg”, após esse passo, realize o envio da aplicação para o debugging de forma análoga ao corriqueiro. A partir disso, se inicia o depurador, a partir da GNU debugguer (GDB), que pode ser chamado diretamente na linha de comando, ou dentro da IDE, operando de forma indireta com a ajuda da GUI, assim, consegue-se realizar o debugging do ESP32-C3.
