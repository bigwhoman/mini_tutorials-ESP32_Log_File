# mini_tutorials-ESP32_Log_File
Code to get log files from ESP32
## Code
The code below is used to open a file using SPIFFS file system and then write 10 lines on it, afterwards the file is opened again for reading and its contents are printed onto the screen.<br>

```ino
#include "SPIFFS.h"

void setup() {
  Serial.begin(9600);

  if(!SPIFFS.begin(true)){
    Serial.println("Error occurred when Begin SPIFFS");
    return; 
  }
  File file2 = SPIFFS.open("/test.txt","w");

  if(!file2){
    Serial.println("Error occurred when Opening File");
    return;
  }

  for(int i=1;i<=10;i++){
    file2.println("THIS IS TEST");  
  }

  file2.close();
  


  File file = SPIFFS.open("/test.txt","r");

  if(!file){
    Serial.println("Error occurred when Opening File");
    return;
  }

  Serial.println("File Content: ");

  while(file.available()){
    Serial.write(file.read());
  }
  
  Serial.println("File Content Finish ");
  file.close();

}

void loop() {

}

```
