// Mu, O Mais Mais  

#include <Servo.h>

Servo servo;

const int pinoServo = 9;
const int pinoBotao = 2;

int posicao = 0;
bool portaAberta = false;

void setup() {
  servo.attach(pinoServo);
  pinMode(pinoBotao, INPUT_PULLUP);
  servo.write(0);
}

void loop() {

  if (digitalRead(pinoBotao) == LOW) {

   if (!portaAberta) {
      // Abre a porta lentamente
      for (posicao = 0; posicao <= 90; posicao++) {
        servo.write(posicao);
        delay(8);
      }
      portaAberta = true;

  } else {
      // Fecha a porta lentamente
      for (posicao = 90; posicao >= 0; posicao--) {
        servo.write(posicao);
        delay(8);
      }
      portaAberta = false;
    }

   // Espera soltar o botão
    while (digitalRead(pinoBotao) == LOW);
    delay(20); // Evita múltiplos acionamentos
  }
}
