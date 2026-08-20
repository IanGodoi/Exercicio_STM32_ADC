Exercício STM32 ADC — Controle de LEDs com Potenciômetro



Projeto desenvolvido com a placa NUCLEO-H755ZI-Q para praticar a utilização do conversor analógico-digital (ADC) do STM32.



OBJETIVO



Ler a posição de um potenciômetro através do ADC e controlar os LEDs da placa de acordo com o valor obtido.



O ADC está configurado com resolução de \*\*16 bits\*\*, portanto a leitura pode variar teoricamente entre:





0 até 65535





Neste exercício foi utilizado o valor \*\*32768\*\*, aproximadamente a metade da faixa, como ponto de decisão.



Hardware utilizado



\* STM32 NUCLEO-H755ZI-Q

\* Potenciômetro

\* Protoboard

\* Jumpers



Ligação do potenciômetro



O potenciômetro possui três terminais:





3V3  → terminal lateral

D12  → terminal central

GND  → terminal lateral



Na NUCLEO-H755ZI-Q, o pino D12 corresponde ao PA6, utilizado como entrada do ADC.



Funcionamento



O programa realiza continuamente os seguintes passos:



1\. Inicia a conversão do ADC.

2\. Espera a conversão terminar.

3\. Armazena o valor lido na variável `readValue`.

4\. Para o ADC.

5\. Compara o valor com `32768`.

6\. Controla os LEDs de acordo com a posição do potenciômetro.



Quando:

readValue > 32768





\* LED verde: ligado

\* LED amarelo: ligado

\* LED vermelho: desligado



Quando:





readValue <= 32768





LED verde: desligado

LED amarelo: desligado

LED vermelho: ligado



Trecho principal do código





while (1)

{

&#x20;   // Inicia a conversão do ADC

&#x20;   HAL\_ADC\_Start(\&hadc1);



&#x20;   // Espera terminar a conversão

&#x20;   HAL\_ADC\_PollForConversion(\&hadc1, 1000);



&#x20;   // Guarda o valor do potenciômetro

&#x20;   readValue = HAL\_ADC\_GetValue(\&hadc1);



&#x20;   // Para o ADC

&#x20;   HAL\_ADC\_Stop(\&hadc1);



&#x20;   // Verifica a posição do potenciômetro

&#x20;   if (readValue > 32768)

&#x20;   {

&#x20;       BSP\_LED\_On(LED\_GREEN);

&#x20;       BSP\_LED\_Off(LED\_RED);

&#x20;       BSP\_LED\_On(LED\_YELLOW);

&#x20;   }

&#x20;   else

&#x20;   {

&#x20;       BSP\_LED\_Off(LED\_GREEN);

&#x20;       BSP\_LED\_On(LED\_RED);

&#x20;       BSP\_LED\_Off(LED\_YELLOW);

&#x20;   }



&#x20;   HAL\_Delay(50);

}







