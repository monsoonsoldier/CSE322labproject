const int led = 3;
const int buzzer = 2;
const int light = A0;
const int sound = A1;
const int temp = A2;
const int B = 3975;
int lightThreshold = 100;
int soundThreshold = 500;

void setup ()
{
     pinMode(led, OUTPUT);
     pinMode(buzzer, OUTPUT);
     Serial.begin(9600);
}

void loop ()
{
     int LightSensorValue = analogRead(light);
     if (LightSensorValue < lightThreshold)
     {
          digitalWrite(led, HIGH);
     }
     else
     {
          digitalWrite(led, LOW);
     }
     
     int SoundSensorValue = analogRead(sound);
     if (SoundSensorValue > soundThreshold)
     {
          digitalWrite(buzzer, HIGH);
          delay(3000);
          digitalWrite(buzzer, LOW);
          delay(300);
     }
     
     int val = analogRead(temp);
     float resistance = (float)(1023-val)*10000/val;
     float temperature = 1/(log(resistance/10000)/B+1/298.15)-273.15;
     Serial.println(temperature);
     if(temperature > 25.00)
     {
          digitalWrite(buzzer, HIGH);
          delay(300);
          digitalWrite(buzzer, LOW);
          delay(300);
     }
     
     delay(1000);
}
