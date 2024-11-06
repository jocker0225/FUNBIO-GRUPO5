// Definición de pines
-const int AIN1 = 16; // Control de dirección 1
-const int AIN2 = 4;  // Control de dirección 2
-const int PWMA = 17; // Control de velocidad (PWM)
-const int joystickY = 34; // Pin analógico del joystick

// Rango de umbral
-const int threshold = 1000; // Ajusta este valor según sea necesario

void setup() {
  // Inicializa los pines como salidas
  -pinMode(AIN1, OUTPUT);
  -pinMode(AIN2, OUTPUT);
  -pinMode(PWMA, OUTPUT);
  
  // Detener el motor al inicio
  -stopMotor();
}

void loop() {
  int joystickValue = analogRead(joystickY); // Lee el valor del joystick

  // Controlar el motor según el valor del joystick
  if (joystickValue > (2048 + threshold)) { // Mueve hacia arriba
    rotateForward();
  } 
  else if (joystickValue < (2048 - threshold)) { // Mueve hacia abajo
    rotateBackward();
  } 
  else {
    stopMotor(); // Detiene el motor si el joystick está en la posición neutral
  }
}

// Función para girar hacia adelante
void rotateForward() {
  -digitalWrite(AIN1, HIGH); // Activa AIN1
  -digitalWrite(AIN2, LOW);  // Desactiva AIN2
  -analogWrite(PWMA, 200); // Establece la velocidad (ajusta este valor)
}

// Función para girar hacia atrás
void rotateBackward() {
  -digitalWrite(AIN1, LOW);  // Desactiva AIN1
  -digitalWrite(AIN2, HIGH); // Activa AIN2
  -analogWrite(PWMA, 200); // Establece la velocidad (ajusta este valor)
}

// Función para detener el motor
void stopMotor() {
  -digitalWrite(AIN1, LOW);  // Desactiva AIN1
  -digitalWrite(AIN2, LOW);  // Desactiva AIN2
  -analogWrite(PWMA, 0); // Establece la velocidad a 0
}
