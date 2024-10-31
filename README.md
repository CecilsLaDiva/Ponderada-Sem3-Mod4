
**MEU CÓDIGO**

``` c++

#define LED_VERMELHO 26
#define LED_AMARELO 27
#define LED_VERDE 25

#define TRIG_PIN 13
#define ECHO_PIN 12
#define BUZZER_PIN 14

const int tempoVermelho = 6000; 
const int tempoAmarelo = 2000; 
const int tempoVerde = 2000;


const int distanciaLimite = 30;

int distancia;

int medirDistancia() {
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  long duracao = pulseIn(ECHO_PIN, HIGH);
  int distancia = duracao * 0.034 / 2;

  return distancia;
}

void setup() {
  pinMode(LED_VERMELHO, OUTPUT);
  pinMode(LED_AMARELO, OUTPUT);
  pinMode(LED_VERDE, OUTPUT);

  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(BUZZER_PIN, OUTPUT);

  Serial.begin(9600);  // Inicializa o monitor serial com baud rate de 9600
}

void loop() {
  // Fase Vermelha
  unsigned long startTime = millis();
  while (millis() - startTime < tempoVermelho) {
    digitalWrite(LED_VERMELHO, HIGH);
    digitalWrite(LED_AMARELO, LOW);
    digitalWrite(LED_VERDE, LOW);

    distancia = medirDistancia();
    Serial.print("Distancia: ");
    Serial.println(distancia);

    if (distancia < distanciaLimite) {
      digitalWrite(BUZZER_PIN, HIGH); // Emite som
    } else {
      digitalWrite(BUZZER_PIN, LOW);  // Para o som
    }
  }

  digitalWrite(BUZZER_PIN, LOW);
  digitalWrite(LED_VERMELHO, LOW); // Desliga o LED vermelho

  // Fase Verde
  startTime = millis();
  while (millis() - startTime < tempoVerde) {
    digitalWrite(LED_VERDE, HIGH);
    digitalWrite(LED_VERMELHO, LOW);
    digitalWrite(LED_AMARELO, LOW);
  }
  digitalWrite(LED_VERDE, LOW); // Desliga o LED verde

    // Fase Amarela
  startTime = millis();
  while (millis() - startTime < tempoAmarelo) {
    digitalWrite(LED_AMARELO, HIGH);
    digitalWrite(LED_VERDE, LOW);
  }
  digitalWrite(LED_AMARELO, LOW); // Desliga o LED amarelo

}

```

**TABELAS**

### Avaliador: Cecília
#### Avaliado: Carolina

|Critério|	Contempla (Pontos)|	Contempla Parcialmente (Pontos)	|Não Contempla (Pontos)	|Observações do Avaliador|
|-|-|-|-|-|
|Montagem física com cores corretas, boa disposição dos fios e uso adequado de resistores	| X	|-	|-   |-   |	
|Temporização adequada conforme tempos medidos com auxílio de algum instrumento externo	| X	|-	| -  | -  |	
|Código implementa corretamente as fases do semáforo e estrutura do código (variáveis representativas e comentários) | X |-	 |-	 |-   |	
|Ir além: Implementou um componente de extra, fez com millis() ao invés do delay() e/ou usou ponteiros no código |	- | X |	- |- |	
| | | | |Pontuação Total: 9,5|



### Avaliador: Carolina
#### Avaliado: Milena

|Critério|	Contempla (Pontos)|	Contempla Parcialmente (Pontos)	|Não Contempla (Pontos)	|Observações do Avaliador|
|-|-|-|-|-|
|Montagem física com cores corretas, boa disposição dos fios e uso adequado de resistores	|X|-|-| 3- O protótipo físico está bem organizado com os fios das cores corretas (laranja e azul) para ligar os positivos e negativos dos leds com a esp32|	
|Temporização adequada conforme tempos medidos com auxílio de algum instrumento externo	|X|-|-|3- O semáforo segue os tempos corretos estabelecidos pelo exercício, utilizando delay de 2 e 6 segundos de acordo com a cor do semáforo |	
|Código implementa corretamente as fases do semáforo e estrutura do código (variáveis representativas e comentários) |X|-|-| 3- Código organizado, variáveis bem estabelecidas e claras e código comentado|	
|Ir além: Implementou um componente de extra, fez com millis() ao invés do delay() e/ou usou ponteiros no código |-|- |	0 | Não implementado|	
| | | | |Pontuação Total: 9|



### Avaliador: Milena
#### Avaliado: Cecília

|Critério|	Contempla (Pontos)|	Contempla Parcialmente (Pontos)	|Não Contempla (Pontos)	|Observações do Avaliador|
|-|-|-|-|-|
|Montagem física com cores corretas, boa disposição dos fios e uso adequado de resistores	| X	| --	| -- | A montagem e o uso de resistores está feito de maneira correta, o uso dos fios está seguindo as conveções dentro das restrições de cabos disponíveis. |	
|Temporização adequada conforme tempos medidos com auxílio de algum instrumento externo	| X	| --	| -- | |	
|Código implementa corretamente as fases do semáforo e estrutura do código (variáveis representativas e comentários) |	X |	-- |	--  | Código organizado e comentado.|	
|Ir além: Implementou um componente de extra, fez com millis() ao invés do delay() e/ou usou ponteiros no código |	X |	-- |	-- |Implementou dois componentes extras (buzzer e sensor ultrassonico), além de também utilizar millis. |	
| | | | |Pontuação Total: 10 |

<div align="center">
<sub>foto</sub><br>
<img src="../assets\foto.jpeg" width="80%" ><br>
<sup>Fonte: Material produzido pelos autores (2024)</sup>
</div>

<div align="center">
<sub>vídeo</sub><br>
<img src="../assets\video.mp4" width="80%" ><br>
<sup>Fonte: Material produzido pelos autores (2024)</sup>
</div>