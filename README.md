# Introdução ao RISC-V

## Objetivo

Apresentar os principais conceitos relaciodos relacionados à quinta geração da arquitetura RISC (RISC-V), com exemplos práticos voltados para o microcontrolador ESP32-C3. 

## Justificativa

A arquitetura RISC-V é moderna e aberta, estando atualmente em franca adoção por diversos fabricantes de microcontroladores e microprocessadores.

Esse trabalho é desenvolvido pelos alunos do curso de Engenharia Biomédica da UFU, com supervisão dos professores, como complementação de carga horária da disciplina de Sistemas Embarcados e possui parte prática e parte teórica, a depender do foco escolhido pelo aluno. 

Na parte teórica, é criada uma documentação abrangente sobre a arquitetura RISC-V, descrevendo os detalhes das versões, conjunto de instruções tratamento de interrupção etc. Na parte prática são abordadas as opções de desenvolvimento disponíveis, passando por toolchains de linha de comando e chegando até IDEs. O uso com sistema operacional de tempo real também é foco do trabalho. 

## Autores

**Discentes**

* Eduarda de Paula Nogueira Soares	
* [Iasmin Martins Cintra](https://github.com/iasminmartins)
* Jéssica Silveira Avila	
* Maria Laura Izidoro Domingues Souza	
* [Marcos Vinícius Meireles Silva](https://github.com/marcusvims)
* [Pedro Paulo Rodrigues Campisi](https://github.com/pedrocampisi)

**Docentes**

* [Daniel Pereira de Carvalho](https://github.com/daniel-p-carvalho)
* [Marcelo Barros de Almeida](https://github.com/marcelobarrosalmeida)

## Conteúdo

* [A arquitetura RISC-V](cap01/README.md)
  * História e origem
    * iniciativa, surgimento, principais pessoas envolvidas, objetivos iniciais do projeto, 
    * Versões (ISA) e extensões (overview)
      * RV32I, RV64I, RV32E, RV128I
      * Extensões (M,A,F,D,G,C,L,J,H,V...)
    * Comparações com outras alternativas como ARM, fundamentos.
    * Implementações existentes
  * Arquitetura
    * Registros, SP, PC, SR, alinhamento, tamanho da palavra, pilha, pipelines
    * Modos de endereçamento
    * Modos de usuário e privilegiado, secure embedded mode
    * Interrupções, salvamento/restauração de contexto (PLIC), delegação
    * Mapa de memória e proteção de memória (PMP)
    * Depuração
    * Conjunto de instruções
      * R format, I format, S format, U format, J format. Detalhes dos conjuntos de instruções.
* [Espressif e RISC-V](cap02/README.md)
  * Introdução sobre a Espressif e adoção do RISCV-V
  * Hardware mínimo com ESP32-C3
  * Módulos baseados em ESP32-C3
  * Processador ESP32-C3 com RISC-V
    * Principais características: modelos, encapsulamento, pinos, características de comunicação, processamento, etc
    * Principais periféricos
    * Tratamento de interrupções
    * Wifi e BLE
    * Depuração
    * Flexibilidade de configuração de pinos
    * Características elétricas: consumo em diversos modos, tensão de operação, latências, etc
* [Ferramentas de desenvolvimento e exemplos](cap03/README.md)
  * Instalação e uso do toolchain via linha de comando, exemplos de uso
  * Uso do debug via USB e da serial para depuração/log de código
  * ESP-IDF: instalação, uso e exemplos
  * ESP32-C3 com IDE Arduino: instalação uso e exemplos
  * Utilização com sistemas operacionais de tempo real (FreeRTOS) ou Nuttx. Exemplos de uso.
