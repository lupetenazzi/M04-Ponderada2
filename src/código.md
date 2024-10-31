# Código

Segue demonstração do código utilizado para realizar a atividade ponderada

```
// Definindo os pinos dos LEDs
const int ledVermelho = 9;
const int ledAmarelo = 10;
const int ledVerde = 11;

// Definindo a duração de cada fase (em milissegundos)
const unsigned long duracaoVermelho = 6000;
const unsigned long duracaoAmarelo = 2000;
const unsigned long duracaoVerde = 2000;

// Variáveis para controle do tempo e da fase atual do semáforo
unsigned long tempoUltimaMudanca = 0;
int faseSemaforo = 0; // 0 = vermelho, 1 = amarelo após vermelho, 2 = verde, 3 = amarelo após verde

void setup() {
  // Configura os pinos como saídas para cada LED
  pinMode(ledVermelho, OUTPUT);
  pinMode(ledAmarelo, OUTPUT);
  pinMode(ledVerde, OUTPUT);
}

void loop() {
  unsigned long tempoAtual = millis();

  // Verifica se o tempo necessário para a fase atual já passou
  switch (faseSemaforo) {
    case 0: // Fase Vermelha
      if (tempoAtual - tempoUltimaMudanca >= duracaoVermelho) {
        tempoUltimaMudanca = tempoAtual;
        faseSemaforo = 1; // Muda para fase amarela
      }
      digitalWrite(ledVermelho, HIGH);
      digitalWrite(ledAmarelo, LOW);
      digitalWrite(ledVerde, LOW);
      break;

    case 1: // Fase Amarela após vermelho
      if (tempoAtual - tempoUltimaMudanca >= duracaoAmarelo) {
        tempoUltimaMudanca = tempoAtual;
        faseSemaforo = 2; // Muda para fase verde
      }
      digitalWrite(ledVermelho, LOW);
      digitalWrite(ledAmarelo, HIGH);
      digitalWrite(ledVerde, LOW);
      break;

    case 2: // Fase Verde
      if (tempoAtual - tempoUltimaMudanca >= duracaoVerde) {
        tempoUltimaMudanca = tempoAtual;
        faseSemaforo = 3; // Muda para fase amarela
      }
      digitalWrite(ledVermelho, LOW);
      digitalWrite(ledAmarelo, LOW);
      digitalWrite(ledVerde, HIGH);
      break;

    case 3: // Fase Amarela antes de voltar ao vermelho
      if (tempoAtual - tempoUltimaMudanca >= duracaoAmarelo) {
        tempoUltimaMudanca = tempoAtual;
        faseSemaforo = 0; // Volta para fase vermelha
      }
      digitalWrite(ledVermelho, LOW);
      digitalWrite(ledAmarelo, HIGH);
      digitalWrite(ledVerde, LOW);
      break;
  }
}
```