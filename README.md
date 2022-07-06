- 👋 Hi, I’m @nikhil3395
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
nikhil3395/nikhil3395 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
1st experiment BLINKING LED
int carRed = 12; // To assign the car lights
int carYellow = 11;
int carGreen = 10;
int pedRed = 9; // To assign the pedestrian lights
int pedGreen = 8;
int button = 2; // Tactile button pin
int crossTime = 5000; // time allowed to cross
unsigned long changeTime; // time since button pressed
void setup()
{
pinMode(carRed, OUTPUT);
pinMode(carYellow, OUTPUT);
pinMode(carGreen, OUTPUT);
pinMode(pedRed, OUTPUT);
pinMode(pedGreen, OUTPUT);
pinMode(button, INPUT); // button on pin 2
// turn on the green light
digitalWrite(carGreen, HIGH);
digitalWrite(pedRed, HIGH);
}
void loop()
{
int state = digitalRead(button);
/* check if button is pressed and it is
over 5 seconds since last button press */
if (state == HIGH && (millis() - changeTime) > 5000)
{
// Call the function to change the lights
changeLights();
}
}
void changeLights() {
digitalWrite(carGreen, LOW); // green off
digitalWrite(carYellow, HIGH); // yellow on
delay(2000); // wait 2 seconds
digitalWrite(carYellow, LOW); // yellow off
digitalWrite(carRed, HIGH); // red on
delay(1000); // wait 1 second till its safe
digitalWrite(pedRed, LOW); // ped red off
digitalWrite(pedGreen, HIGH); // ped green on
delay(crossTime); // wait for preset time period
// flash the ped green
for (int x=0; x<10; x++) {
digitalWrite(pedGreen, HIGH);
delay(250);
digitalWrite(pedGreen, LOW);
delay(250);
}
// turn ped red on
digitalWrite(pedRed, HIGH);
delay(500);
digitalWrite(carYellow, HIGH); // Yellow will switch on
digitalWrite(carRed, LOW); // red will switch off
delay(1000);
digitalWrite(carGreen, HIGH);
digitalWrite(carYellow, LOW); // Yellow will switch off
// record the time since last change of lights
changeTime = millis();
// Retun / Loop
}

2ND EXPERIMENT------------------------SERVO MOTOR USING POTENTIO MOTOR
#include <Servo.h>
Servo myservo; // create servo object to control a servo
int potpin = 0; // analog pin used to connect the potentiometer
int val; // variable to read the value from the analog pin
void setup() 
{
 myservo.attach(9); // attaches the servo on pin 9 to the servo object
}
void loop() 
{
val = analogRead(potpin); // reads the value of the potentiometer (value between 0 and 
1023)
val = map(val, 0, 1023, 0, 180);// scale it to use it with the servo (value between 0 and 180)
myservo.write(val); // sets the servo position according to the scaled value
delay(15); 
}

4TH EXPERIMENT----------------------IR SENSOR MODULE
void setup() {
 // put your setup code here, to run once:
pinMode(8,INPUT);
pinMode(12,OUTPUT);//LED
}
void loop() {
 // put your main code here, to run repeatedly:
if(digitalRead(8)==LOW){
 digitalWrite(12,HIGH);
}
25 | P a g e
else{
 digitalWrite(12,LOW);
}
}
5TH EX-------------------PIR
int led = 13; // the pin that the LED is atteched to
int sensor = 2; // the pin that the sensor is atteched to
int state = LOW; // by default, no motion detected
int val = 0; // variable to store the sensor status (value)
void setup() {
 pinMode(led, OUTPUT); // initalize LED as an output
 pinMode(sensor, INPUT); // initialize sensor as an input
 Serial.begin(9600); // initialize serial
}
void loop(){
 val = digitalRead(sensor); // read sensor value
 if (val == HIGH) { // check if the sensor is HIGH
 digitalWrite(led, HIGH); // turn LED ON
 delay(500); // delay 100 milliseconds 
 
 if (state == LOW) {
 Serial.println("Motion detected!"); 
 state = HIGH; // update variable state to HIGH
 }
 } 
 else {
 digitalWrite(led, LOW); // turn LED OFF
 delay(500); // delay 200 milliseconds 
 
 if (state == HIGH){
 Serial.println("Motion stopped!");
 state = LOW; // update variable state to LOW
 }
 }
}

6TH EX-------------------------------RFID
#include <SPI.h>
#include <MFRC522.h>
#define SS_PIN 10
#define RST_PIN 9
MFRC522 mfrc522(SS_PIN, RST_PIN); // Create MFRC522 instance.
void setup() 
{
 Serial.begin(9600); // Initiate a serial communication
 SPI.begin(); // Initiate SPI bus
 mfrc522.PCD_Init(); // Initiate MFRC522
32 | P a g e
 Serial.println("Approximate your card to the reader...");
 Serial.println();
}
void loop() 
{
 // Look for new cards
 if ( ! mfrc522.PICC_IsNewCardPresent()) 
 {
 return;
 }
 // Select one of the cards
 if ( ! mfrc522.PICC_ReadCardSerial()) 
 {
 return;
 }
 //Show UID on serial monitor
 Serial.print("UID tag :");
 String content= "";
 byte letter;
 for (byte i = 0; i < mfrc522.uid.size; i++) 
 {
 Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
 Serial.print(mfrc522.uid.uidByte[i], HEX);
 content.concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " "));
 content.concat(String(mfrc522.uid.uidByte[i], HEX));
 }
 Serial.println();
 Serial.print("Message : ");
 content.toUpperCase();
 if (content.substring(1) == "BD 31 15 2B") //change here the UID of the 
card/cards that you want to give access
 {
 Serial.println("Authorized access");
 Serial.println();
 delay(3000);
 }
else {
 Serial.println(" Access denied");
 delay(3000);
 }
} 


