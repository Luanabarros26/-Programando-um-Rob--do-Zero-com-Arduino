# -Programando-um-Rob--do-Zero-com-Arduino
// Inclua a biblioteca do Motor Shield
#include <AFMotor.h>

// Defina os pinos dos botões
const int pinoBotaoEsquerda = 2;
const int pinoBotaoDireita = 3;
const int pinoBotaoFrente = 4;
const int pinoBotaoTras = 5;

// Defina o pino do sensor de distância
const int pinoSensorDistancia = 6;

// Defina o pino do atuador de destruição
const int pinoAtuadorDestruicao = 7;

// Crie uma instância do Motor Shield
AF_DCMotor motorEsquerda(1);
AF_DCMotor motorDireita(2);

// Função para mover o robô para a frente
void moverParaFrente() {
  motorEsquerda.setSpeed(255);
  motorEsquerda.run(FORWARD);
  motorDireita.setSpeed(255);
  motorDireita.run(FORWARD);
}

// Função para mover o robô para trás
void moverParaTras() {
  motorEsquerda.setSpeed(255);
  motorEsquerda.run(BACKWARD);
  motorDireita.setSpeed(255);
  motorDireita.run(BACKWARD);
}

// Função para girar o robô para a esquerda
void girarParaEsquerda() {
  motorEsquerda.setSpeed(255);
  motorEsquerda.run(BACKWARD);
  motorDireita.setSpeed(255);
  motorDireita.run(FORWARD);
}

// Função para girar o robô para a direita
void girarParaDireita() {
  motorEsquerda.setSpeed(255);
  motorEsquerda.run(FORWARD);
  motorDireita.setSpeed(255);
  motorDireita.run(BACKWARD);
}

// Função para parar o movimento do robô
void pararMovimento() {
  motorEsquerda.setSpeed(0);
  motorEsquerda.run(RELEASE);
  motorDireita.setSpeed(0);
  motorDireita.run(RELEASE);
}

void setup() {
  // Configure os pinos dos botões como entrada com pull-up interno
  pinMode(pinoBotaoEsquerda, INPUT_PULLUP);
  pinMode(pinoBotaoDireita, INPUT_PULLUP);
  pinMode(pinoBotaoFrente, INPUT_PULLUP);
  pinMode(pinoBotaoTras, INPUT_PULLUP);

  // Configure o pino do atuador de destruição como saída
  pinMode(pinoAtuadorDestruicao, OUTPUT);
}

void loop() {
  // Verifique se o botão para a esquerda foi pressionado
  if (digitalRead(pinoBotaoEsquerda) == LOW) {
    girarParaEsquerda();
  }
  // Verifique se o botão para a direita foi pressionado
  else if (digitalRead(pinoBotaoDireita) == LOW) {
    girarParaDireita();
  }
  // Verifique se o botão para frente foi pressionado
  else if (digitalRead(pinoBotaoFrente) == LOW) {
    moverParaFrente();
  }
  // Verifique se o botão para trás foi pressionado
  else if (digitalRead(pinoBotaoTras) == LOW) {
    moverParaTras();
  }
  // Se nenhum botão foi pressionado, pare o movimento
  else {
    pararMovimento();
  }
  
  // Verifique a distância do sensor e acione o atuador de destruição se estiver dentro da faixa
  int distancia = medirDistancia();
  if (distancia <= 15) {
    acionarAtuadorDestruicao();
  }
}

// Função para medir a distância com o sensor de distância
int medirDistancia() {
  // Código para medir a distância com o sensor de distância
  // Retorne o valor medido em centímetros
}

// Função para acionar o atuador de destruição (motor da serra elétrica)
void acionarAtuadorDestruicao() {
  digitalWrite(pinoAtuadorDestruicao, HIGH);
  delay(1000); // Tempo de ativação do atuador
  digitalWrite(pinoAtuadorDestruicao, LOW);
}
