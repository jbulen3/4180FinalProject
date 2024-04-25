# Weather System Alert Station
Team Members: Ash Bennett, Jeffrey Bulen, Chris Fitzpatrick, Michael Harrington 

Section: B (11:00 AM - 12:15 PM)

Watch the demonstration video used for our presentation: https://youtu.be/bTrGZVEWVQo?si=XtpuWW9YQfTjSvzG

![image](https://github.com/jbulen3/4180FinalProject/assets/117386228/7ecde1b4-e2d1-4567-ab79-ca30f715a110)

# Table of Contents  
[Project Idea and Implementation](#project-idea-and-implementation)

[Parts List](#parts-list)    

[Schematic and Connection Guide](#schematic-and-connection-guide)

[Software Development Gantt Chart](#software-development-gantt-chart)

[Source Code](#source-code)

[Future-Ideas-for-Improvement](#future-ideas-for-improvement)
<a name="project-idea-and-implementation"/>
<b name="parts-list"/>
<c name="schematic-and-connection-guide"/>
<d name="software-development-gantt-chart"/>
<e name="source-code"/>
<f name="future-ideas-for-improvement"/>
## Project Idea and Implementation
Weather can be uncertain. Knowing the environmental conditions around can tell us how to prepare for hazardous conditions, and that is what this project set out to achieve. 

Our idea for the ECE 4180 (Spring 2024) Final Project was to make a Weather System Alert Station that reads in temperature and humidity and alerts the user to worrisome conditions. It is controlled by a microcontroller and uses threads with a semaphore to complete its operations. When the temperature and humidity sensors read in information, the LCD displays different suggestions on how a user can handle the elements. A microphone is used to pick up loud audio that would be similar to thunder from hazardous storms, and it prompts the user to go inside and plays an audio from a speaker to draw the users attention. The device is able to be active or paused using Bluetooth, and the station plays an audio from a speaker when it is active or paused. The microcontroller is connected to ethernet and is able to use a web server for data output. Additionally, when the user is near the Weather System Alert Station, a sonar will detect their presence and turn on a motor with an umbrella to acknowledge the user.

Each of these features allow for the weather station to act in a way that creates a unique user experience while creating the function of our Weather System Alert Station.

Block Diagram of our project

![image](https://github.com/jbulen3/4180FinalProject/assets/117386228/aa9969fc-fc1f-44cf-980d-6ed67e628334)

## Parts List
Electronics:
* 1 Mbed LPC1768: https://www.sparkfun.com/products/9564
* 1 LCD Display (uLCD-144G2): https://www.sparkfun.com/products/11377
* 1 I2C Humidity and Temperature Sensor (Si7021):
* 1 Speaker: https://www.sparkfun.com/products/11089
* 1 Qwiic DC Motor: https://www.sparkfun.com/products/18625
* 1 HC-SR04 Sonar Sensor: https://www.sparkfun.com/products/15569
* 2 2N3904 Transistors: https://www.digikey.com/en/products/detail/diotec-semiconductor/2N3904/13164701
* 2 1K Ohm Resistors: https://www.amazon.com/California-JOS-Carbon-Resistor-Tolerance/dp/B0BR66ZN6B/
* 1 10K Ohm Resistor: https://www.amazon.com/California-JOS-Carbon-Resistor-Tolerance/dp/B0BR67DJHM/
* 1 1N4148 Diode: https://www.digikey.com/en/products/detail/onsemi/1N4148/458603
* 1 SPDT 250VAC/30VDC 5A Relay: https://www.sparkfun.com/products/100
* 1 Ethernet Interface: https://www.sparkfun.com/products/13021
* 1 Ethernet Cable: https://www.sparkfun.com/products/8915
* 1 Wall Adapter Power Supply: https://www.sparkfun.com/products/8915
* 1 DC Barrel Power Jack/Connector: https://www.sparkfun.com/products/12748
* Assorted Jumper Wires: https://www.sparkfun.com/products/124
* 1 Giant Breadboard: https://www.sparkfun.com/products/12614

Non-electronics:
* 1 Tiny Umbrella: https://www.partycity.com/cocktail-umbrella-picks-20ct-409987.html
* A Creative Mind

## Schematic and Connection Guide
Device Setup:

![image](https://github.com/jbulen3/4180FinalProject/assets/117386228/4efc3b57-4925-4cdb-a055-769d110fa611)

![image](https://github.com/jbulen3/4180FinalProject/assets/117386228/98b32458-3647-420c-a355-947496cb1876)

![image](https://github.com/jbulen3/4180FinalProject/assets/117386228/c04844e7-fe58-4dbd-9b77-641bf0d5ee28)

![image](https://github.com/jbulen3/4180FinalProject/assets/117386228/0083ad55-7804-4f22-905a-61539d84264c)

Connection Table:
| Mbed  | Microphone | DC Motor | Speaker | Bluetooth | Sonar (HC-SR04)| LCD | Si7021 (Temp./Humidity Sensor) | Ethernet | 2N3904 Transistor (Speaker) | 2N3904 Transistor (Motor) | Relay | 1N4148 Diode |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |------------- |------------- | ------------- |------------- |------------- |
| p6    |       | | | | trig | | | | |
| p7  | | | | | echo | | | | | | | |
| p8  | |  | | | | | | | | B | | |
| p9  | | | | | | | sda | | | | |
| p10  | | | | | | | scl | | | | | |
| p13  | | | | | | RX | | | | | | |
| p14  | | | | | | TX | | | | | | |
| p15  | | | | | | Reset | | | | | | |
| p16  | DC | | | | | | | | | | | |
| p26 | | |  | | | | | | B | | | |
| p27  | | | | TXO | | | | | | | | |
| p28  | | | | RXI | | | | | | | | |
|  | | Motor + |  | | | | | | |  | Motor +| |
|  | | |  | | | | | | | E | Coil | |
|  | | |  | | | | | | | E |  | Input | |
|  | | |  | | | | | | |  | RAW| Output | |
|  | | | Speaker '-' | | | | | | E | | | |
| TD+  | | | | | | | | p1 | | | | |
| TD-  | | | | | | | | p2 | | | | |
| RD+  | | | | | | | | p7 | | | | |
| RD-  | | | | | | | | p8 |  | | | |
| Gnd  | gnd | Motor -| | gnd, CTS | gnd | gnd | gnd | | C| C | | |
| Vout| |  | Speaker '+'| | | | Vin | | | | | |
| +5V (External)| Vin | | | Vin (3.3-16V) | Vcc | 5V | | | | | 5V | |
| LED1  | | | | | Sonar Indicator | | | | | | | |
| LED3  | Microphone Indicator | | | | | | | | | | | |
| LED4  | | | | On/Off Status | | | | |  | | | |

*LED 2 is used to show if the Mbed is running properly by flashing every half second.

On/Off Status: Used with the Bluetooth module to indicate whether the Mbed has been active or paused by Bluetooth. On if active, off if paused.

Microphone Indicator: Used to indicate Microphone inputs to determine noise level for thunder. Output varies by microphone but the brighter the LED, the louder the sound input.

Sonar Indicator: Used to indicate whether a user is near the System using Sonar. On if yes, off if no.

## Software Development Gantt Chart

![gantt chart v2](https://github.com/jbulen3/4180FinalProject/assets/123829977/546c5c61-5fd4-4fc2-bc9d-dfc7ed177546)

## Source Code
```c
#include "mbed.h"
#include "rtos.h"
#include "SDFileSystem.h"
#include "uLCD_4DGL.h"
#include "Si7021.h"
#include <stdio.h>
#include "Servo.h"
#include "wave_player.h"
#include "SongPlayer.h"
#include "ultrasonic.h"
#include "EthernetInterface.h"

class microphone
{
public :
    microphone(PinName pin);
    float read();
    operator float ();
private :
    AnalogIn _pin;
};
microphone::microphone (PinName pin):
    _pin(pin)
{
}
float microphone::read()
{
    return _pin.read();
}
inline microphone::operator float ()
{
    return _pin.read();
}

microphone mymicrophone(p16);

DigitalOut Digital(p8);
// wave_player waver(&DACout);

Serial bluemod(p28,p27);

volatile int globalDistance = 0;
volatile double temp = 0;
volatile double humidity = 0;

void dist(int distance) {
    //put code here to execute when the distance has changed
    distance *= 0.00328084;
    // printf("Distance %d ft\r\n", distance);
}

ultrasonic mu(p6, p7, .1, 1, &dist);    //Set the trigger pin to D8 and the echo pin to D9
                                        //have updates every .1 seconds and a timeout after 1
                                        //second, and call dist when the distance changes

Si7021 temp_sensor(p9, p10);

uLCD_4DGL LCD(p13,p14,p15);

Semaphore lcd_s(1); //used to be (2)

DigitalOut led4(LED4);
DigitalOut led1(LED1);
DigitalOut led3(LED3);
DigitalOut led2(LED2);

Serial USB(USBTX,USBRX);
volatile bool song_start = true;
volatile int on_off_status = 1;

volatile float thunder = 0.0;


void on_off_indicator(void const *args) {
    while (true) {
        led4 = on_off_status;
        Thread::wait(1000);
    }
}

void mic_method(void const *args) {
    float sample;
    float average = 0.67/3.3;
    while(1) {
        while(!on_off_status) Thread::yield();
        //read in sample value
        sample = mymicrophone;
        average = 0.9999*average + 0.0001*sample;
        thunder = int(abs((sample - average)*300.0));
        led3 = thunder;
        Thread::wait((1.0/8000.0)*1000.0);
    }
}

void bluetooth_on_off(void const *args) {
    // thread loop
    char bnum;
    char bhit;
    bool song_start = true;
    while(true) {
        Thread::wait(200);
        while(!bluemod.readable()) Thread::yield();
            lcd_s.wait();
            //USB.baud(9600); 
            if (bluemod.getc()=='!'){
                if(bluemod.getc()=='B'){
                    bnum = bluemod.getc();
                    bhit = bluemod.getc();
                    //USB.putc(bluemod.getc());
                    switch(bnum){
                        case '5': //up arrow
                            if(bhit == '1'){
                                on_off_status = 1;
                                USB.putc('1');
                                float note[6] = {196.00, 261.63, 293.66, 329.63, 329.63, 20.0};
                                float delay[6] = {.2, .2,.2, .4, .4, .2};
                                float end_note[1] = {0};
                                float end_delay[1] = {0};
                                song_start = true;
                                while (song_start) {
                                    SongPlayer mySpeaker(p26);
                                    mySpeaker.PlaySong(note,delay);
                                    song_start = false;
                                    Thread::wait(1000);
                                    mySpeaker.PlaySong(end_note, end_delay);
                                        
                                    Thread::wait(1000);
                                }
                            }
                            break;
                        case '6': //down arrow
                            if(bhit == '1'){
                                on_off_status = 0;
                                USB.putc('0');
                                    
                                float note2[6] = {329.63, 329.63, 293.66, 261.63, 196.00, 20.0};
                                float delay2[6] = {.2, .2,.2, .4, .4, .2};
                                    
                                // loops forever while song continues to play to end using interrupts
                                float end_note2[1] = {0};
                                float end_delay2[1] = {0};
                                song_start = true;
                                while (song_start) {
                                    SongPlayer mySpeaker(p26);
                                    // Start song and return once playing starts
                                    mySpeaker.PlaySong(note2,delay2);
                                    song_start = false;
                                    Thread::wait(1000);
                                    mySpeaker.PlaySong(end_note2, end_delay2);
                                        
                                    Thread::wait(1000);
                                }
                            }
                            break;  
                        default:
                            break;
                    }
                }
            }
            lcd_s.release();
            Thread::wait(200);
    }
}

void run_web_server(void const *args) {
    EthernetInterface net;
    const int HTTP_PORT = 80;

    // Show MAC address for secure networks
    char mac[6];
    mbed_mac_address(mac);
    printf("MAC address = %02x:%02x:%02x:%02x:%02x:%02x\n", mac[0], mac[1], mac[2], mac[3], mac[4], mac[5]);

    // Setup network connection
    printf("Setting up network connection...\n");
    net.init();
    net.connect();
    printf("IP address = %s\n", net.getIPAddress());

    // Start TCP web server
    TCPSocketServer server;
    server.bind(HTTP_PORT);
    server.listen();

    // Serve connections
    while (true) {
        printf("Wait for new connection...\n");
        TCPSocketConnection client;
        server.accept(client);
        client.set_blocking(false, 1500); // Timeout after 1.5s
        printf("Connection from: %s\n", client.get_address());
        char response [1400];


        while (true) {
            int n = client.receive(response, sizeof(response));
            if (n <= 0) {
                break;
            }

            // Terminate received message            
            response[n] = '\0';

            // Formulate HTTP response
            snprintf(response, 1400, "HTTP/1.1 200 OK\nConnection: keep-alive\nAccess-Control-Allow-Origin: *\nAccess-Control-Allow-Methods: GET\nAccess-Control-Allow-Headers:accept, content-type\nContent-Length: 1400\nContent-Type: text/html; charset=utf-8\n\n<!doctypehtml><html lang=en><meta charset=UTF-8><meta content=\"width=device-width,initial-scale=1\"name=viewport><meta content=\"ie=edge\"http-equiv=X-UA-Compatible><title>Weather System Alert Station</title><style>*{box-sizing:border-box;margin:0;padding:0}body{font-family:Arial,sans-serif;color:#333e48;background-color:#f5f5f5}.container{width:80%%;margin:0 auto;padding:0 15px}header{background-color:#008fbe;color:#fff;padding:20px 0;margin-bottom:30px}.main{padding:20px 0}section{width:90%%;background-color:#fff;padding:20px;margin-bottom:20px;margin-left:auto;margin-right:auto;border-radius:10px;box-shadow:0 10px 20px rgba(0,0,0,.1)}.separator{margin-top:10px;margin-bottom:10px}</style><header><div class=container><h1>Weather System Alert Station</h1></div></header><main><section><div class=container><h2>Current Weather - <span id=time></span></h2><hr class=separator><div class=current-weather><h3>Temperature: %.2f °F</h3><h3>Humidity: %.2f%%</h3></div></div></section></main><script>function updateTime(){let e=new Date,t=document.getElementById('time');t.textContent=`${e.toLocaleTimeString()}`}setInterval(updateTime,1e3);</script>\n", temp, humidity);

            int sent_num = client.send_all(response, strlen(response));
            printf("Sent response: %s", response);
            if (sent_num <= 0) {
                break;
            }
        }
        client.close();
        printf("Connection Closed\n");
    }
}

void sonar(void const *args) {
    
    while(1)
    {
        //while(!on_off_status) Thread::yield();
        lcd_s.wait();
        mu.startUpdates();//start measuring the distance
        lcd_s.release();
        //Do something else here
        mu.checkDistance();     //call checkDistance() as much as possible, as this is where
                                //the class checks if dist needs to be called.
        globalDistance = mu.getCurrentDistance();
        globalDistance *= 0.00328084;
        if (globalDistance <= 3) {
            //lcd_s.wait();
            led1 = 1; //replace with turning on motor
            Digital = 1;
            //lcd_s.release();
            
        } else {
            //lcd_s.wait();
            led1 = 0; //replace with turning off motor
            Digital = 0;
            //lcd_s.release();
        }
        Thread::wait(1000);
    }
}



void temphum(void const *argument) {
    
    while (1) {
        while(!on_off_status) Thread::yield();
        temp_sensor.measure();
        temp = temp_sensor.get_temperature();

        temp = ((175.72 * temp)/65536) - 46.85;
        temp = (temp * (9.0/5.0)) + 32;
        humidity = temp_sensor.get_humidity();

        humidity = ((125.00 * humidity) / 65536) - 6;
        lcd_s.wait();
        LCD.cls();
        //lcd_s.wait();
        LCD.locate(0,1);
        LCD.textbackground_color(RED);
        LCD.printf("WEATHER STATION");

        //lcd_s.wait();
        LCD.locate(0,2);
        LCD.textbackground_color(BLUE);
        LCD.printf("Temp: %5.2f ",temp);
        LCD.printf("F \n\r");

        LCD.locate(0,3);
        LCD.printf("Humidity: %5.2f ",humidity);
        LCD.printf("% \n\r");
        //lcd_s.release();

        //Thread::wait(0.5 *1000.0);
        LCD.locate(0,6);
        LCD.textbackground_color(BLUE);
        LCD.printf("Thunder: %5.2f \n\r",thunder);
            
        LCD.locate(0,8);
            
        if (thunder >= 1.0) {
            LCD.printf(" GO INSIDE!");
            float note2[6] = {329.63, 196.00, 329.63, 196.00, 329.63, 20.0};
            float delay2[6] = {.2, .2,.2, .4, .4, .2};
            
            // loops forever while song continues to play to end using interrupts
            float end_note2[1] = {0};
            float end_delay2[1] = {0};
            song_start = true;
            while (song_start) {
                SongPlayer mySpeaker(p26);
                // Start song and return once playing starts
                mySpeaker.PlaySong(note2,delay2);
                song_start = false;
                Thread::wait(1000);
                mySpeaker.PlaySong(end_note2, end_delay2);
                
                Thread::wait(1000);
            }
        } else if (temp > 75  && humidity > 100) {
            LCD.locate(0,10);
            LCD.printf("Dress Light and   apply antipersperant!");
        } else if (temp > 75 && humidity < 75) {
             LCD.locate(0,10);
            LCD.printf("Dress Light and   apply chapstick!");
        } else if (temp > 75) {
             LCD.locate(0,10);
            LCD.printf("Dress Light!");
        } else if (temp < 60 && humidity > 100) {
             LCD.locate(0,10);
            LCD.printf("Put on a jacket and apply antipersperant!");
        } else if (temp < 60 && humidity < 75) {
             LCD.locate(0,10);
            LCD.printf("Put on a jacket and apply chapstick!");
        } else if (temp < 60) {
            LCD.locate(0,10);
            LCD.printf("Put on a jacket!");
        }
        lcd_s.release();
        Thread::wait(1000);
    }
}


int main()
{
    Thread t1(temphum);
    Thread t2(mic_method);
    Thread t3(bluetooth_on_off);
    Thread t4(run_web_server);
    // LCD.printf("Weather Station");
    Thread t5(on_off_indicator);
    Thread t6(sonar);
    
    // Testing
    DigitalOut led2(LED2);
    while (1) {
        led2 = !led2;
        led3 = 1;
        Thread::wait(500);
    }
}
```

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Weather System Alert Station</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: Arial, sans-serif;
            color: #333E48;
            background-color: #f5f5f5;
        }

        .container {
            width: 80%;
            margin: 0 auto;
            padding: 0 15px;
        }

        header {
            background-color: #008FBE;
            color: #fff;
            padding: 20px 0;
            margin-bottom: 30px;
        }

        .main {
            padding: 20px 0;
        }

        section {
            width: 90%;
            background-color: #fff;
            padding: 20px;
            margin-bottom: 20px;
            margin-left: auto;
            margin-right: auto;
            border-radius: 10px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, .1);
        }

        .separator {
            margin-top: 10px;
            margin-bottom: 10px;
        }
    </style>
</head>

<body>
    <header>
        <div class=container>
            <h1>Weather System Alert Station</h1>
        </div>
    </header>
    <main>

        <section>
            <div class=container>
                <h2>Current Weather - <span id="time"></span></h2>
                <hr class="separator">
                <div class=current-weather>
                    <h3>Temperature: %d °C</h3>
                    <h3>Humidity: %d%</h3>
                </div>
            </div>
        </section>
    </main>
    <script>
        // Function to update time
        function updateTime() {
            const now = new Date();
            const timeElement = document.getElementById('time');
            timeElement.textContent = `${now.toLocaleTimeString()}`;
        }
        // Update time every second
        setInterval(updateTime, 1000);
    </script>
</body>

</html>
```

## Future Ideas for Improvement
* Additional indicators for snow and other weather patterns for more robustness.
* Additional sensors to show user seismic and additional storm information.
* Include Bluetooth controls for individual components, like speaker audio or motor activation.
* Allow for connections with other weather stations for larger area's weather status.
* Use historic weather data for predictions into the future, using the website output for larger weather analysis and more specific warnings.


