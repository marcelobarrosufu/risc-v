# Ferramentas de desenvolvimento e exemplos

## Instalação e uso do toolchain via linha de comando, exemplos de uso e ESP-IDF: instalação, uso e exemplos

### Primeiros passos

O ESP-IDF requer que algumas ferramentas de pré-requisito sejam instaladas para que você possa criar firmware para chips compatíveis. As ferramentas de pré-requisito incluem Python, Git, cross-compilers e ferramentas de compilação como o CMake e Ninja. 

Assim, a maneira mais fácil de se instalar os pré-requisitos do EPS-IDF, é ir ao site [Espressif](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/index.html) e entrar na aba do [manual de instalação](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/index.html#manual-installation), dentro dessa aba se encontrará os tutorias para instalar a toolchain e o ESP-IDF para [Windows](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/windows-setup.html) ou [Linux e macOS](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/linux-macos-setup.html), além de alguns exemplos. 

Depois disso, basta seguir os passo a psso da instalação e escolher o diretorio em que todas as ferramentas serão instaladas.

### Preparando o ambiente

Para construir algum projeto basta procurar pelo "ESP-IDF Command Prompt (cmd.exe)" na aba de pesquisa do proprio Windows, esse comando abrirá o prompt de comando, só  que com todo o ambiente da ESP-IDF já preparado. Depois de abrir o cmd, basta escolher onde o projeto será criado, se o interesse for em criar no diretorio do usuario,  basta utilizar o comando: cd %userprofile%.

### Exemplos

Agora, para realizar-se alguns testes, é necessário baixar algum [exemplo](https://github.com/espressif/esp-idf/tree/01d014c42def8d0c19e1ce55c07de6761e092ffa/examples/get-started) 
  
#### Hello_world

Baixado o arquivo "hello_world", utilize o comando "xcopy /e /i %IDF_PATH%\examples\get-started\hello_world hello_world", ou faça isso manualmente, para copiar a pasta "hello_wordl" para o seu diretorio e depois entre na pasta "hello_world" com o comando "cd hello_world". 

Com isso, agora é necessário informar ao compilador que o código dentro desse projeto foi criado para o chip esp32, para realizar tal feito, com um cabo do tipo micro usbO, conecte o seu Esp32 no USB do desktop ou notebook.

Depois de conectado, basta utilizar o seguinte comandos: “idf.py set-target esp32”, dependendo do chip utilizado, coloque "esp32-c3" ou "esp32-s3" no lugar do "esp32". 

Depois disso, use o comando: “idf.py menuconfig”, para acessar o menu de configurações do projeto, ele é utilizado para configurar variáveis específicas do projeto, por exemplo, nome e senha da rede Wi-Fi, velocidade do processador, etc.

Porém, no caso desse exemplo pode-se deixar as configurações padrões. 

Agora é possível compilar o projeto com o comando: “idf.py build”. Este comando compilará a aplicação e todos os componentes do ESP-IDF e, em seguida, gerará o bootloader, a tabela de partições e as aplicações binarias.

#### Blink

O passo a passo inicial do blink é o mesmo do Hello-world. 

### Conecte o seu Esp32

Portanto, depois de todos esses processos, finalmente é possível realizar os primeiros testes, primeiro é necessário achar qual a porta do dispositivo, para fazer isso, vá para o gerenciador de dispositivo e procure pelo dispositivo “Ports (COM & LPT)”, lá estará a sua porta. 

Entretanto, se der algum erro e o dispositivo não estiver aparecendo ou com algum conflito, basta procurar  pelo driver [“cp210x driver”](https://www.driverguide.com/driver/detail.php?driverid=2000471) e baixar a sua última versão.

Com isso feito, segure o botão “Boot” da sua placa e depois aperte o reset, com o “Boot” pressionado, e solte o “Boot”, com isso a placa será resetada.

### Compilando e executando o programa

Bom, realizada as etapas anteriores finalmente será possivel complilar e executar o exemplo escolhido. Assim, escreva o comando “idf.py -p COM5 (porta do meu chip) flash monitor” para compilar e executar o programa.

Feito isso, caso tudo estaja nos conformes, a mensagem “Hello_world” aparecera no seu cmd, ou o seu chip começara a piscar caso o exemplo escolhido seja o "blink".

Para sair do terminal aperte “ctrl” “t” e o “x”.

Desse modo, se todos os passos anteriores forem seguidos corretamente será possivel rodar um primeiro exemplo no esp32-c3.


