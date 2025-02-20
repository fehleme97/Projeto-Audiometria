Sistema de AUDIOMETRIA - Utilizando a placa BitDogLab. Projeto proposto para o projeto final do curso de Sistemas Embarcados da instituição de ensino Instituto Hardware BR - Embarcatech. 

Através da placa BitDogLab, que consiste em um microcontrolador Raspberry
Pi Pico W da família de processamento RP2040, e com os periféricos embutidos na placa, utilizaremos os buzzers A e B, botões A e B, Display OLED e dois Leds (RGB) para que em conjunto com o código, torne o projeto idealizado em um sistema preciso que aplica sinais sonoros audíveis para identificar possíveis deficiências auditivas ocasionadas pela sensibilidade audível a determinada frequência e/ou intensidade. O sistema funciona de acordo com o seguinte fluxo:

	Através do microcontrolador RP2040 o Raspberry defini uma sequência de instruções para que se torne possível o teste das frequências e tonalidades de maneira randômica, sendo gerado aleatoriamente aos buzzers A e B para que assim, o usuário consiga pressionar o botão correspondente a cada buzzer. Através do PWM geramos a intensidade do som e o clock para frequência setada para o teste, o usuário será testado em diferentes frequências, obedecendo a sequência das frequências importantes, sendo elas de 250 Hz até 8000 Hz. Além disso, o examinador terá o auxílio de um Display OLED, para inicializar o programa e ao final do teste irá exibir um relatório com os acertos e erros, caso haja. Além de uma sinalização visual através do Led nas cores verde para correta e vermelho para incorreta. O sistema é composto pelos seguintes periféricos:

•	Buzzers A e B: Geram tons em diferentes frequências e intensidades.

•	Botões A e B: Permitem ao usuário responder qual buzzer está emitindo o som.

•	Display OLED: Exibe instruções, resultados e feedback durante o teste.

•	LEDs RGB: Fornecem feedback visual (verde para resposta correta, vermelho para resposta incorreta).

3.1.1	Funcionamento do Sistema

Inicialização: 

•	O sistema inicia com uma mensagem no display OLED instruindo o usuário a pressionar os botões A e B para começar o teste.

•	Após o início, o sistema exibe uma mensagem indicando que o teste começará em 4 segundos.


Execução do Teste:

•	O teste consiste em 10 rodadas, onde em cada rodada:
Uma frequência aleatória (250 Hz, 500 Hz, 1000 Hz, 2000 Hz, 4000 Hz, ou 8000 Hz) e uma intensidade aleatória (10%, 30%, 50%, 70%, ou 90%) são selecionadas.

•	O som é emitido por um dos buzzers (A ou B), escolhido aleatoriamente.

•	O usuário deve pressionar o botão correspondente ao buzzer que está emitindo o som.

•	Se a resposta estiver correta, o LED verde acende. Caso contrário, o LED vermelho acende e o erro é registrado.


Finalização do Teste:

•	Após as 10 rodadas, o sistema exibe no display OLED o número de acertos e erros.

•	Os erros são detalhados no Serial Monitor, mostrando a frequência, intensidade e o buzzer correspondente a cada erro.

•	O usuário pode optar por reiniciar o teste (pressionando o botão A duas vezes) ou sair do programa (pressionando o botão B duas vezes).


	Detalhes Técnicos

PWM (Pulse Width Modulation):

•	O PWM é utilizado para controlar a intensidade do som nos buzzers. A frequência do som é ajustada pelo divisor de clock (pwm_set_clkdiv), enquanto a intensidade é controlada pelo nível do canal PWM (pwm_set_chan_level).


Randomização:

•	As frequências e intensidades são selecionadas aleatoriamente a partir de arrays predefinidos (frequencies[] e intensities[]).

•	A função rand() é utilizada para gerar números aleatórios, e a semente (números aleatórios gerados) é definida com base no tempo (srand(time(NULL)) e srand(to_us_since_boot(get_absolute_time()))).


Feedback Visual:

•	O LED verde acende para respostas corretas, e o LED vermelho acende para respostas incorretas.

•	O display OLED exibe mensagens de instrução e o resultado final.


Interface com o Usuário: 

•	O usuário interage com o sistema através dos botões A e B, que são configurados como entradas com pull-up.

•	O display OLED fornece informações claras sobre o estado do teste e os resultados.

