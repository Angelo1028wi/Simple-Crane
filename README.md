# 🏗️ Simple Crane Project

This project demonstrates a **basic crane mechanism** using Arduino, two servo motors, and a DC motor controlled by push buttons.  

- **Bottom Servo (xser)** → Handles **rotational movement** of the crane base.  
- **Top Servo (yser)** → Controls the **forward/backward line of the hook**.  
- **DC Motor + Push Buttons** → Raises and lowers the hook using reverse polarity (one button for up, one for down).  

---

## 📜 Code

```cpp
#include <Servo.h>

Servo xser;
Servo yser;

int xpin = A0;
int ypin = A1;

int xangle = 90;
int yangle = 90;

int deadzone = 90;

void setup() {
  xser.attach(2);
  yser.attach(3);

  xser.write(xangle);
  yser.write(yangle);
}

void loop() {
  int xval = analogRead(xpin);
  int yval = analogRead(ypin);

  if (abs(xval - 512) > deadzone) {
    xangle = map(xval, 0, 1023, 0, 180);
    xser.write(xangle);
  }

  if (abs(yval - 512) > deadzone) {
    yangle = map(yval, 0, 1023, 0, 180);
    yser.write(yangle);
  }
}
