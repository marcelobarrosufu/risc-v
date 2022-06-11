# Ferramentas de desenvolvimento e exemplos
## Instalação e uso do toolchain via linha de comando, exemplos de uso
  O primeiro passo e baixar o ESP-IDF, que pode ser encontrado neste link: https://dl.espressif.com/dl/esp-idf/, lembre-se de baixar a versão mais nova de 1 GB.
  Depois disso, basta escolher o diretorio em que todas as ferramentas serão instaladas.
  Para construir algum projeto basta procurar pelo "ESP-IDF Command Prompt (cmd.exe)" na aba de pesquisa do proprio Windows, esse comando abrirá o prompt de comando, só   que com todo o ambiente da ESP-IDF já preparado. Depois de abrir o cmd, basta escolher onde o projeto será criado, se o interesse for em criar no diretorio do usuario,   basta utilizar o comando: cd %userprofile%.
  
  Com isso feito, o proximo passo é baixar um exemplo para teste, acesse o link e baixe o exemplo:https://github.com/espressif/esp-idf/tree/01d014c42def8d0c19e1ce55c07de6761e092ffa. 
  A partir dai, utilize o comando "xcopy /e /i %IDF_PATH%\examples\get-started\hello_world hello_world" para copiar a pasta "hello_wordl" para o seu diretorio e depois entre na pasta "hello_world" com o comando "cd hello_world". Com isso, agora é necessário informar ao compilador que o código dentro desse projeto foi criado para o chip esp32-c3, basta utilizar os seguintes comandos: “idf.py set-target esp32”, dependendo do chip utilizado coloque "esp32-c3" ou "esp32-s3" no lugar do "esp32". Depois disso, use o comando: “idf.py menuconfig”, para acessar o menu de configurações do projeto, a priori deixe as configurações padrões. Agora é possível compilar o projeto com o comando: “idf.py build”.
  
  Portanto, depois de todos esses processos, finalmente é possível realizar os primeiros testes. O primeiro passo e achar qual a porta do seu esp32, para fazer isso, vá para o gerenciador de dispositivo e procure pelo dispositivo “Ports (COM & LPT)”, lá estará a sua porta. Entretanto, se der algum erro e o dispositivo não estiver aparecendo ou com algum conflito, basta procurar no google pelo driver “cp210x driver” e baixar a sua última versão. Com isso feito, segure o botão “Boot” da sua placa e depois aperte o reset, com o “Boot” pressionado, e solte o “Boot”, com isso a placa será resetada. Assim, escreva o comando “idf.py -p COM5 (porta do meu chip) flash monitor” para compilar e executar o programa, feito isso a mensagem “Hello_world” aparecera no seu cmd, para sair do terminal aperte “ctrl” “t” e o “x”. Desse modo, se todos os passos anteriores forem seguidos corretamente será possivel rodar um primeiro exemplo no esp32-c3.
  
  
  
... to be continued !
