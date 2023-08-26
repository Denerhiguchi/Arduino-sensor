# Arduino-sensor
// vou passar os codigos que eu utilizei no arduino para um sensor de movimento no Led's
// lembre-se de utilizar a Biblioteca "Ultrasonic.h 
// só preste atenção nos Pin que voces estão inserindo.
_______________________________________________________________________________________
#include "Ultrasonic.h"
Ultrasonic ultrasonic(10, 9); // Trigger na porta 3 e Echo na porta 2

//Declarando os LED como constantes em seus respectivos pinos
const int ledVerde = 3;
const int ledAmarelo = 11;

long microsec = 0; // variaveis de controle
float distanciaCM = 0;

void setup() {
  Serial.begin(9600); //Inicializando o serial monitor
  pinMode(ledVerde, OUTPUT); //declarando os LEDs como saida
  pinMode(ledAmarelo, OUTPUT);
 
}

void loop() {
  //Lendo o valor do sensor
  microsec = ultrasonic.timing();

  //Convertendo a distância em CM
  distanciaCM = ultrasonic.convert(microsec, Ultrasonic::CM);

  ledDistancia();
  Serial.print(distanciaCM);// mostrar a distancia na porta serial
  Serial.println(" cm");// colocar unidade de medida
  delay(500);// espera de 500 milissegundos
}

void ledDistancia() {

  //Desliga todos os LEDs
  digitalWrite(ledVerde, LOW);
  digitalWrite(ledAmarelo, LOW);
 

  // criando as condicoes se a distancia for entre 30 cm e 20 cm
  if (distanciaCM <= 30 and distanciaCM >= 20) {
    digitalWrite(ledVerde, HIGH); //liga o LED verde
  }
  // se a distancia for 10 cm e 20 cm
  if (distanciaCM <= 20 and distanciaCM >= 10) {
    digitalWrite(ledAmarelo, HIGH); //liga LED amarelo
  }}


