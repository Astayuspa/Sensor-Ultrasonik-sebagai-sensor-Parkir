#define trigPin 9
#define echoPin 10
#define ledPin1 4
#define ledPin2 5
#define ledPin3 6
#define buzzerPin 7

void setup() {
  Serial.begin(9600);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(ledPin1, OUTPUT);
  pinMode(ledPin2, OUTPUT);
  pinMode(ledPin3, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
}

void loop() {
  long duration, distance;

  // Mode 1: Parkir jika jarak kurang dari 3 cm
  distance = getDistance();
  if (distance < 3) {
    digitalWrite(ledPin1, HIGH);
    digitalWrite(ledPin2, LOW);
    digitalWrite(ledPin3, LOW);
    digitalWrite(buzzerPin, HIGH);
    delay (100);
     digitalWrite(buzzerPin, LOW);
     delay(100);
    Serial.println("Mode 1: Parkir");
  
  }

  // Mode 2: Peringatan jika jarak antara 3 cm - 10 cm
  else if (distance >= 3 && distance < 10) {
    digitalWrite(ledPin1, LOW);
    digitalWrite(ledPin2, HIGH);
    digitalWrite(ledPin3, LOW);
    digitalWrite(buzzerPin, HIGH);
    delay (500);
     digitalWrite(buzzerPin, LOW);
     delay(1000);
    Serial.println("Mode 2: Peringatan");
  }

  // Mode 3: Aman jika jarak lebih dari 10 cm
  else {
    digitalWrite(ledPin1, LOW);
    digitalWrite(ledPin2, LOW);
    digitalWrite(ledPin3, HIGH);
    noTone(buzzerPin); // Matikan bunyi buzzer pada mode aman
    Serial.println("Mode 3: Aman");
  }

  delay(500); // Delay untuk membaca ultrasoinik setiap 0.5 detik
}

long getDistance() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  return pulseIn(echoPin, HIGH) * 0.034 / 2;
  }
