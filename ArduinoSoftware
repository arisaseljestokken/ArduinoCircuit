void setup()
{
  Serial.begin(9600);
  pinMode(8, OUTPUT);	//Red LED
  pinMode(9, OUTPUT);	//Yellow LED
  pinMode(13, OUTPUT); 	//Green LED
  
  pinMode(12, INPUT);	//Left button
  pinMode(11, INPUT);	//Right button
}

const int LOCKED = 0;
const int WAITING = 1;
const int UNLOCKED = 2;
int state = LOCKED;
  
  bool motion = false;
  bool leftPushed = false;
  bool rightPushed = false;
  
  int countLeftButton = 0;
  int countRightButton = 0;
  int pushCount = 0;

void blink(){
    	digitalWrite(9, LOW);
        delay(250);
        digitalWrite(9, HIGH);
}

void loop()
{
  
  int PIRSensor = digitalRead(6);
  int leftButton = digitalRead(12);
  int rightButton = digitalRead(11);
  
  if(PIRSensor == HIGH){
  	motion = true;
  }
  
  if(leftButton == HIGH){
  	leftPushed = true;
    countLeftButton += 1;
    pushCount += 1;
  }
  
  if(rightButton == HIGH){
  	rightPushed = true;
    countRightButton += 1;
    pushCount += 1;
  }
  
  switch(state){
    case LOCKED:
    digitalWrite(8, HIGH);  
   		if((motion) && (!leftPushed) && (!rightPushed)){ 
  		state = WAITING;
  		}
    break;
    
    case WAITING:
    digitalWrite(8, LOW);
    digitalWrite(9, HIGH);
    	if((pushCount > 0) && (rightPushed) || (leftPushed)){
          	blink();
        }
    	if((pushCount == 4) && (countRightButton == 2) && (countLeftButton == 2)){
          	state = UNLOCKED;
        }else if((pushCount >= 4) && (countRightButton != 2)){
        	state = LOCKED;
        }
    break;
    
    case UNLOCKED:
    digitalWrite(9, LOW);
    digitalWrite(13, HIGH);
    break;
            
	}
}