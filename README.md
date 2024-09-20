#include <Servo.h>

Servo myServo;

const int button1Pin = 2; // Button for item 1
const int button2Pin = 3; // Button for item 2
const int button3Pin = 4; // Button for item 3

const int led1Pin = 5;    // LED for item 1
const int led2Pin = 6;    // LED for item 2
const int led3Pin = 7;    // LED for item 3

void setup() {
  pinMode(button1Pin, INPUT_PULLUP);
  pinMode(button2Pin, INPUT_PULLUP);
  pinMode(button3Pin, INPUT_PULLUP);
  
  pinMode(led1Pin, OUTPUT);
  pinMode(led2Pin, OUTPUT);
  pinMode(led3Pin, OUTPUT);
  
  myServo.attach(9); // Attach the servo
  myServo.write(0);  // Start with the servo at 0 degrees
}

void loop() {
  if (digitalRead(button1Pin) == LOW) {
    dispenseItem(1);
  } 
  else if (digitalRead(button2Pin) == LOW) {
    dispenseItem(2);
  } 
  else if (digitalRead(button3Pin) == LOW) {
    dispenseItem(3);
  }
}

void dispenseItem(int item) {
  // Indicate the item selection
  digitalWrite(led1Pin, item == 1 ? HIGH : LOW);
  digitalWrite(led2Pin, item == 2 ? HIGH : LOW);
  digitalWrite(led3Pin, item == 3 ? HIGH : LOW);

  // Simulate dispensing
  myServo.write(90); // Move servo to dispense position
  delay(1000);       // Wait for a second
  myServo.write(0);  // Move servo back to starting position

  // Turn off LEDs after dispensing
  digitalWrite(led1Pin, LOW);
  digitalWrite(led2Pin, LOW);
  digitalWrite(led3Pin, LOW);
  
  delay(2000); // Wait before allowing another selection
}
