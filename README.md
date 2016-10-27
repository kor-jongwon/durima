# durima
int sw = 10;       // sw pin set  
int relay = 7;       // Relay pin set
 
int state = LOW;      // Relay state
int reading;          // SW state
int previous = LOW;   // SW before state
 
long time = 0;        // Relay toggles on/off last time
long debounce = 100;  // Debounce time set
 
void setup()
{
  pinMode(sw, INPUT_PULLUP); // SW input set , arduino pull-up resistor use
  pinMode(relay, OUTPUT);    // relay set
}
 
void loop()
{
  reading = digitalRead(sw);  // SW read set
 
  //run greater than 'debounce' times have elapsed time pressed the toggle switch is pressed and sw
  if (reading == HIGH && previous == LOW && millis() - time > debounce) {
    if (state == HIGH)    //if relay high change low
      state = LOW;
    else                 // if relay low change high
      state = HIGH;
 
    time = millis();
  }
 
  digitalWrite(relay, state); //read relay state
 
  previous = reading;   //sw set reading
}
 
