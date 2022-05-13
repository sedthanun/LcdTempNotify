# LCDTempNotify
โครงงานพัฒนาเกี่ยวกับ MicroController ที่เกี่ยวข้องกับ การวัดค่าอุณหภูมิผ่าน Temp Sensor แล้วไปแสดงผลยังจอ LCD โดยใช้บอร์ด UNO ใน Wokwi เพื่อทำ Simulation และเชื่อมต่อเข้ากับ NTC Temp Sensor, LCD และ LED Light เพื่อแจ้งเตือนหากวัดอุณหภูมิได้ 37.5 ขึ้นไป สามารถนำไปประยุกต์ใช้กับการทำ เครื่องมือวัดอุณหภูมิ Covid-19 ได้

![enter image description here](https://github.com/sedthanun/LcdTempNotify/blob/main/pic_project2.jpg?raw=true)

## ผู้จัดทำ
นายเสฏฐนันท์ จงเจตน์ดี รหัสนักศึกษา 62070212
<br>

<img src="https://github.com/sedthanun/LcdTempNotify/blob/main/Me.jpg?raw=true" width="500" height="500">


# Link Wokwi
https://wokwi.com/projects/331560695055254099

# Source Code

    #include  <LiquidCrystal.h>
    
    // LedTempNotify
    
    const  float BETA =  3950;  // should match the Beta Coefficient of the thermistor
    
      
    
    LiquidCrystal lcd(12,  11,  10,  9,  8,  7);
    
      
    
    byte sign[8]  =  {
    
    B11100,
    
    B10100,
    
    B11100,
    
    B00000,
    
    B00111,
    
    B01000,
    
    B01000,
    
    B00111
    
    };
    
      
    
    void  setup()  {
    
    Serial.begin(9600);
    
    lcd.createChar(1, sign);
    
    lcd.begin(16,  2);
    
    lcd.setCursor(0,1);
    
    pinMode(13,  OUTPUT);
    
    }
    
      
    
    void  loop()  {
    
    float analogValue =  analogRead(A0);
    
    float celsius =  1  /  (log(1  /  (1023.  / analogValue -  1))  / BETA +  1.0  /  298.15)  -  273.15;
    
    Serial.print("Temperature: ");
    
    Serial.print(celsius);
    
    Serial.println(" ℃");
    
    if(celsius >  37.5){
    
    digitalWrite(13,  HIGH);
    
    }else{
    
    digitalWrite(13,  LOW);
    
    }
    
      
    
    lcd.setCursor(5,1);
    
    lcd.print(celsius);
    
    lcd.write(1);
    
    delay(500);
    
    lcd.clear();
    
      
    
    }

