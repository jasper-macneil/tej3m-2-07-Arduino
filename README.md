# tej3m-2-07-Arduino

// Jasper MacNeil

#include <Servo.h>

const int TRIG_PIN  = 6;  
const int ECHO_PIN  = 7;  
const int SERVO_PIN = 9; 
const int DISTANCE_THRESHOLD = 50;

Servo servo;
float duration, distance;


void setup() {
  Serial.begin (9600);       
  pinMode(TRIG_PIN, OUTPUT); 
  pinMode(ECHO_PIN, INPUT);  
  servo.attach(SERVO_PIN);   
  servo.write(0);
}

void loop() {
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);                       
  digitalWrite(TRIG_PIN, LOW);
  duration = pulseIn(ECHO_PIN, HIGH);
  distance = 0.017 * duration;

  if (distance < DISTANCE_THRESHOLD) {
    servo.write(180);
  } else {
    servo.write(0);
  }

  Serial.print("Distance: ");
  Serial.println(distance);
  delay(100);

  delay(500);
}
