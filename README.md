# Designing an electronic circuit for the sensor using the relay
## :black_circle: *Concept the relay* :bulb::arrow_down::
##### :heavy_minus_sign: The relay is the device that open or closes the contacts to cause the operation of the other electric control. It detects the intolerable or undesirable condition with an assigned area and gives the commands to the circuit breaker to disconnect the affected area. Thus protects the system from damage

## :black_circle: *Concept the relay with arduino*:bulb::arrow_down::
##### :heavy_minus_sign:  A relay is a programmable electrical switch, which can be controlled by Arduino or any micro-controller. It is used to programmatically control on/off the devices, which use the high voltage and/or high current. It is a bridge between Arduino and high voltage devices

## :black_circle: *Working Principle of Relay* :loud_sound::
##### :heavy_minus_sign: It works on the principle of an electromagnetic attraction. When the circuit of the relay senses the fault current, it energises the electromagnetic field which produces the temporary magnetic field :hammer_and_wrench:

## :black_circle: *Working Principle of Relay with arduino*:loud_sound::
##### :heavy_minus_sign: A relay accomplishes this by using the 5V outputted from an Arduino pin to energize the electromagnet which in turn closes an internal, physical switch to turn on or off a higher power circuit. The switching contacts of a relay are completely isolated from the coil, and hence from the Arduino:hammer_and_wrench:

## :black_circle: *electronic circuit* :point_down::
![Grand Blad-Amur](https://user-images.githubusercontent.com/107880209/182004458-75886786-4f0c-466f-8a42-0e8957ef58ac.png)

## :black_circle: *code* :receipt::computer::
```

int relayPin = 9;     // the number of the relay pin
int buttonPin = 12;   // the number of the push button pin

int buttonState = HIGH;     // Record button state, and initial the state to high level
int relayState = LOW;       // Record relay state, and initial the state to low level
int lastButtonState = HIGH; // Record the button state of last detection
long lastChangeTime = 0;    // Record the time point for button state change

void setup() {
  pinMode(buttonPin, INPUT);  // Set push button pin into input mode
  pinMode(relayPin, OUTPUT);  // Set relay pin into output mode
  digitalWrite(relayPin, relayState); // Set the initial state of relay into "off"
  Serial.begin(9600);                 // Initialize serial port,and set baud rate to 9600
}

void loop() {
  int nowButtonState = digitalRead(buttonPin); // Read current state of button pin
  // If button pin state has changed, record the time point
  if (nowButtonState != lastButtonState) {
    lastChangeTime = millis();
  }
  // If button state changes, and stays stable for a while, then it should have skipped the bounce area
  if (millis() - lastChangeTime > 10) {
    if (buttonState != nowButtonState) {  // Confirm button state has changed
      buttonState = nowButtonState;
      if (buttonState == LOW) {     // Low level indicates the button is pressed
        relayState = !relayState;           // Reverse relay state
        digitalWrite(relayPin, relayState); // Update relay state
        Serial.println("Button is Pressed!");
      }
      else {                        // High level indicates the button is released
        Serial.println("Button is Released!");
      }
    }
  }
  lastButtonState = nowButtonState; // Save the state of last button
}
```
