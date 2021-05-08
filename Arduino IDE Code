#include <IRremote.h>
int RECV_PIN = 8;
//IR Library stuff
IRrecv irrecv(RECV_PIN);
decode_results results;

int motorRightF = 12;
int motorRightB = 13;
int motorLeftF = 7;
int motorLeftB = 6;

int ledGreen = 5;
int ledBlue = 4;
int ledRed = 3;

int pushButton = 9;
int buzzer = 2;
int bs = 0;

long readUltrasonicDistance(int triggerPin, int echoPin)
{
  pinMode(triggerPin, OUTPUT);  // Clear the trigger
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  // Sets the trigger pin to HIGH state for 10 microseconds
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
  // Reads the echo pin, and returns the sound wave travel time in microseconds
  return pulseIn(echoPin, HIGH);
}

void motorcontrol(){
	if (irrecv.decode(&results)) {      //irrecv.decode(&results) returns true if anything is recieved, and stores info in varible results
    unsigned int value = results.value; //Get the value of results as an unsigned int, so we can use switch case
    // Serial.println(value); value coming from remote
    digitalWrite(ledBlue,HIGH); 
    digitalWrite(ledGreen,LOW);
    digitalWrite(ledRed,LOW);
    delay(100);
    switch (value) {
      case 20655: //forward
      	Serial.println("moving forward");
      	digitalWrite(motorRightF, HIGH);
    	digitalWrite(motorRightB, LOW);
    	digitalWrite(motorLeftF, HIGH);
    	digitalWrite(motorLeftB, LOW);
      	break;
      
      case 4335:  //back
      	Serial.println("moving backwards");
      	digitalWrite(motorRightF, LOW);
    	digitalWrite(motorRightB, HIGH);
    	digitalWrite(motorLeftF, LOW);
    	digitalWrite(motorLeftB, HIGH);
      	break;
      
      case 24735:  //right   => clockwise
      	Serial.println("rotating right");      	
      	digitalWrite(motorRightF, LOW);
    	digitalWrite(motorRightB, HIGH);
    	digitalWrite(motorLeftF, HIGH);
    	digitalWrite(motorLeftB, LOW);
      	break;
      
      case 8415:  //left  => anti-clockwise
      	Serial.println("rotating left");
      	digitalWrite(motorRightF, HIGH);
    	digitalWrite(motorRightB, LOW);
    	digitalWrite(motorLeftF, LOW);
    	digitalWrite(motorLeftB, HIGH);
      	break;
      
      case 16575: //stop
      	Serial.println("stopping ");
      	digitalWrite(motorRightF, LOW);
   	 	digitalWrite(motorRightB, LOW);
    	digitalWrite(motorLeftF, LOW);
    	digitalWrite(motorLeftB, LOW);	
      	break;
    }
    Serial.println("Enter next command....");
 	delay(200);
    irrecv.resume(); // Receive the next value
  }
}

void panicSound(){
	int val = digitalRead(pushButton);
  	if (val == HIGH) {
     //initiate buzzer alarm with Red LED
   	 digitalWrite(buzzer, HIGH);
     digitalWrite(ledRed, HIGH);
     digitalWrite(ledGreen, LOW);
     digitalWrite(ledBlue, LOW);
  	} 
  	else {
    	digitalWrite(buzzer, LOW);
      	digitalWrite(ledRed, LOW);
     	digitalWrite(ledGreen, HIGH);
     	digitalWrite(ledBlue, LOW);
  	}
  	
}

void setup()
{
  pinMode(motorLeftF, OUTPUT);   //forward of left motor
  pinMode(motorLeftB, OUTPUT);   //back of left motor
  pinMode(motorRightF, OUTPUT);   //forward of right motor
  pinMode(motorRightB, OUTPUT);   //back of right motor
  pinMode(ledGreen,OUTPUT);
  pinMode(ledBlue,OUTPUT);
  pinMode(ledRed,OUTPUT);
  pinMode(pushButton,INPUT);
  pinMode(buzzer,OUTPUT);
  Serial.begin(9600);
  irrecv.enableIRIn(); 
  Serial.println("All pins Enabled");      
  Serial.println("Welcome !!");
  Serial.println("Select direction ? ");
}

void loop()
{ 
  digitalWrite(ledGreen,HIGH);   //light will stay on for better vision in darker areas
  panicSound();
  int distance1 = 0.01724137 * readUltrasonicDistance(10,10); //left ultrasonic sensor distance in cm
  int distance2 = 0.01724137 * readUltrasonicDistance(11,11); //right ultrasonic sensor distance in cm
   if (distance1 <= 20 || distance2 <= 20) {
    //Rotate right Wheel Chair if distance less than 20cm in either sensor
    digitalWrite(buzzer, HIGH);
    digitalWrite(ledRed, HIGH);
    digitalWrite(ledGreen, LOW);
    digitalWrite(ledBlue, LOW);
    Serial.println("OBSTACLE ALERT !! STOP.STOP.STOP");
    Serial.print("Distance 1: ");Serial.println(distance1);
    Serial.print("Distance 2: ");Serial.println(distance2);
    Serial.println("Rotating right!");
    digitalWrite(motorRightF, LOW);
    digitalWrite(motorRightB, HIGH);
    digitalWrite(motorLeftF, HIGH);
    digitalWrite(motorLeftB, LOW);
    delay(500);
    //take one rotation then stop and wait to see if obstacle removed otherwise rotate again
    digitalWrite(buzzer,LOW);
    digitalWrite(motorRightF, LOW);
    digitalWrite(motorRightB, LOW);
    digitalWrite(motorLeftF, LOW);
    digitalWrite(motorLeftB, LOW);
    Serial.println("Rotated right!");
  }
  else {
    motorcontrol(); // if no obstacle then ofc user can go anywher
  }
}
