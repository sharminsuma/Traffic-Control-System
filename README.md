//# Traffic-Control-System
 //Traffic Control System with Sonar Sensor and Servo Motor


#include <Servo.h>

#define SENSOR1_TRIGGER_PIN 9 // Ultrasonic sensor 1 trigger pin
#define SENSOR1_ECHO_PIN 10    // Ultrasonic sensor 1 echo pin
#define SENSOR2_TRIGGER_PIN 12 // Ultrasonic sensor 2 trigger pin
#define SENSOR2_ECHO_PIN 13    // Ultrasonic sensor 2 echo pin

#define SERVO_PIN 14 // Pin connected to the servo motor

#define LED_RED_1 2     // Red LED for road 1
#define LED_YELLOW_1 4  // Yellow LED for road 1
#define LED_GREEN_1 3   // Green LED for road 1
#define LED_RED_2 5     // Red LED for road 2
#define LED_YELLOW_2 7 // Yellow LED for road 2
#define LED_GREEN_2 6  // Green LED for road 2

Servo servo; // Create a servo object

long duration; // Variable to store time taken to the pulse
int distance; // Variable to store distance calculated using

void setup() {
  Serial.begin(9600);

  pinMode(SENSOR1_TRIGGER_PIN, OUTPUT);
  pinMode(SENSOR1_ECHO_PIN, INPUT);
  pinMode(SENSOR2_TRIGGER_PIN, OUTPUT);
  pinMode(SENSOR2_ECHO_PIN, INPUT);
  
  pinMode(LED_RED_1, OUTPUT);
  pinMode(LED_YELLOW_1, OUTPUT);
  pinMode(LED_GREEN_1, OUTPUT);
  pinMode(LED_RED_2, OUTPUT);
  pinMode(LED_YELLOW_2, OUTPUT);
  pinMode(LED_GREEN_2, OUTPUT);

  servo.attach(SERVO_PIN); // Attach the servo to the specified pin

}

void loop() {
  float distance1 = measureDistance(SENSOR1_TRIGGER_PIN, SENSOR1_ECHO_PIN);    //Distance calculation for senror 1
  float distance2 = measureDistance(SENSOR2_TRIGGER_PIN,SENSOR2_ECHO_PIN);  //Distance calculation for senror 2

  Serial.print("Distance from sensor 1: ");
  Serial.print(distance1);
  Serial.println(" cm");

  Serial.print("Distance from sensor 2: ");
  Serial.print(distance2);
  Serial.println(" cm");

  delay(1000);

  if (distance1<=10 && distance2<=10)
    normalControl(); // Perform normal traffic control

  else if (distance1>10 && distance2>10)
    normalControl(); // Perform normal traffic control

  else if (distance1<=10 && distance2>10)
    priorityControlNorthSouth(); //perform priority control on North South

  else if (distance1>10 && distance2<=10)
    priorityControlEastWest(); //perform priority control on East West

  else
    normalControl(); // Perform normal traffic control

}

void normalControl() {

  Serial.println("Normal traffic control");

  digitalWrite(LED_RED_1, HIGH);  // Red LED for road 1
  digitalWrite(LED_YELLOW_1, LOW);// Yellow LED for road 1
  digitalWrite(LED_GREEN_1, LOW);// Green LED for road 1
  digitalWrite(LED_RED_2, LOW);// Red LED for road 2
  digitalWrite(LED_YELLOW_2, LOW);// Yellow LED for road 2
  digitalWrite(LED_GREEN_2, HIGH);// Green LED for road 2

  servo.write(90); // Set servo position
  delay(15000);
  
  digitalWrite(LED_RED_1, LOW);  // Red LED for road 1
  digitalWrite(LED_YELLOW_1, HIGH);// Yellow LED for road 1
  digitalWrite(LED_GREEN_1, LOW);// Green LED for road 1
  digitalWrite(LED_RED_2, LOW);// Red LED for road 2
  digitalWrite(LED_YELLOW_2, HIGH);// Yellow LED for road 2
  digitalWrite(LED_GREEN_2, LOW);// Green LED for road 2
  delay(2500);
  
  servo.write(0); // Set servo position
  delay(2500);
  
  digitalWrite(LED_RED_1, LOW);  // Red LED for road 1
  digitalWrite(LED_YELLOW_1, LOW);// Yellow LED for road 1
  digitalWrite(LED_GREEN_1, HIGH);// Green LED for road 1
  digitalWrite(LED_RED_2, HIGH);// Red LED for road 2
  digitalWrite(LED_YELLOW_2, LOW);// Yellow LED for road 2
  digitalWrite(LED_GREEN_2, LOW);// Green LED for road 2

  servo.write(0); // Set servo position
  delay(15000);

  digitalWrite(LED_RED_1, LOW);  // Red LED for road 1
  digitalWrite(LED_YELLOW_1, HIGH);// Yellow LED for road 1
  digitalWrite(LED_GREEN_1, LOW);// Green LED for road 1
  digitalWrite(LED_RED_2, LOW);// Red LED for road 2
  digitalWrite(LED_YELLOW_2, HIGH);// Yellow LED for road 2
  digitalWrite(LED_GREEN_2, LOW);// Green LED for road 2
  delay(2500);
  
  servo.write(90); // Set servo position
  delay(2500);
}

void priorityControlNorthSouth() {

  Serial.println("Priority control on North South");
  
  digitalWrite(LED_RED_1, HIGH);  // Red LED for road 1
  digitalWrite(LED_YELLOW_1, LOW);// Yellow LED for road 1
  digitalWrite(LED_GREEN_1, LOW);// Green LED for road 1
  digitalWrite(LED_RED_2, LOW);// Red LED for road 2
  digitalWrite(LED_YELLOW_2, LOW);// Yellow LED for road 2
  digitalWrite(LED_GREEN_2, HIGH);// Green LED for road 2
  
  servo.write(90); // Set servo position
  delay(20000);

  digitalWrite(LED_RED_1, LOW);  // Red LED for road 1
  digitalWrite(LED_YELLOW_1, HIGH);// Yellow LED for road 1
  digitalWrite(LED_GREEN_1, LOW);// Green LED for road 1
  digitalWrite(LED_RED_2, LOW);// Red LED for road 2
  digitalWrite(LED_YELLOW_2, HIGH);// Yellow LED for road 2
  digitalWrite(LED_GREEN_2, LOW);// Green LED for road 2
  delay(1500);
  
  servo.write(0); // Set servo position
  delay(1500);
  
  digitalWrite(LED_RED_1, LOW);  // Red LED for road 1
  digitalWrite(LED_YELLOW_1, LOW);// Yellow LED for road 1
  digitalWrite(LED_GREEN_1, HIGH);// Green LED for road 1
  digitalWrite(LED_RED_2, HIGH);// Red LED for road 2
  digitalWrite(LED_YELLOW_2, LOW);// Yellow LED for road 2
  digitalWrite(LED_GREEN_2, LOW);// Green LED for road 2
  
  servo.write(0); // Set servo position
  delay(10000);
  
  digitalWrite(LED_RED_1, LOW);  // Red LED for road 1
  digitalWrite(LED_YELLOW_1, HIGH);// Yellow LED for road 1
  digitalWrite(LED_GREEN_1, LOW);// Green LED for road 1
  digitalWrite(LED_RED_2, LOW);// Red LED for road 2
  digitalWrite(LED_YELLOW_2, HIGH);// Yellow LED for road 2
  digitalWrite(LED_GREEN_2, LOW);// Green LED for road 2
  delay(1500);
  
  servo.write(90); // Set servo position
  delay(1500);
}

void priorityControlEastWest() {

  Serial.println("Priority control on East West");
  
  digitalWrite(LED_RED_1, HIGH);  // Red LED for road 1
  digitalWrite(LED_YELLOW_1, LOW);// Yellow LED for road 1
  digitalWrite(LED_GREEN_1, LOW);// Green LED for road 1
  digitalWrite(LED_RED_2, LOW);// Red LED for road 2
  digitalWrite(LED_YELLOW_2, LOW);// Yellow LED for road 2
  digitalWrite(LED_GREEN_2, HIGH);// Green LED for road 2
  
  servo.write(90); // Set servo position
  delay(10000);
  
  digitalWrite(LED_RED_1, LOW);  // Red LED for road 1
  digitalWrite(LED_YELLOW_1, HIGH);// Yellow LED for road 1
  digitalWrite(LED_GREEN_1, LOW);// Green LED for road 1
  digitalWrite(LED_RED_2, LOW);// Red LED for road 2
  digitalWrite(LED_YELLOW_2, HIGH);// Yellow LED for road 2
  digitalWrite(LED_GREEN_2, LOW);// Green LED for road 2
  delay(1500);

  servo.write(0); // Set servo position
  delay(1500);
  
  digitalWrite(LED_RED_1, LOW);  // Red LED for road 1
  digitalWrite(LED_YELLOW_1, LOW);// Yellow LED for road 1
  digitalWrite(LED_GREEN_1, HIGH);// Green LED for road 1
  digitalWrite(LED_RED_2, HIGH);// Red LED for road 2
  digitalWrite(LED_YELLOW_2, LOW);// Yellow LED for road 2
  digitalWrite(LED_GREEN_2, LOW);// Green LED for road 2
  
  servo.write(0); // Set servo position
  delay(20000);

  digitalWrite(LED_RED_1, LOW);  // Red LED for road 1
  digitalWrite(LED_YELLOW_1, HIGH);// Yellow LED for road 1
  digitalWrite(LED_GREEN_1, LOW);// Green LED for road 1
  digitalWrite(LED_RED_2, LOW);// Red LED for road 2
  digitalWrite(LED_YELLOW_2, HIGH);// Yellow LED for road 2
  digitalWrite(LED_GREEN_2, LOW);// Green LED for road 2
  delay(1500);

  servo.write(90); // Set servo position
  delay(1500);
  
}

float measureDistance(int triggerPin, int echoPin) {
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);

  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);

  long duration = pulseIn(echoPin, HIGH);
  float distance = duration * 0.034 / 2; // Speed of sound in air is approximately 34 cm/ms
  return distance;
}
