
# ESP8266 Window Shades

An Arduino code for ESP8266 module which controls your motorized window shade into wireless motorized one.

# Why

I have motorized window shades in my house controlled by 2 switches for up and down. Few weeks ago I started with a homebridge on a Pi for apple homekit, working quite nicely.
So I was looking for a possibility to control my shades via homekit and found the sketch of psled, which is quit nice, but I have the motors already installed and wanted to control up to 2 shades per ESP8266.
So I used from psled only his HTTP part and wrote the controller part new using the Arduino IDE.
To improve accuracy I used tasks. Position is controlled by moving time. I call the moving/controll task every total-move-time divided by 100. So I have to add or subtract only 1 of the current position.


# Requirements

- ESP8266 module (I used WeMos D1 mini)
- double relay for Arduino (try to use the ones working with 3.3V)
- switches were already mounted in the wall
- 5V power supply (cheap mobile charger is working fine, but be aware that here you may have high voltage poweron the 5V side!!!!!!!!!!!!!!!!!  )

Keep in mind that the relays are switching high voltage of your window shades!!!!

My shades have an automatic stop at the end, but I can not read this.


# Installation



First, download and install [ESP8266 Arduino](https://github.com/esp8266/Arduino) if you haven't done this before.

Connect the components, but be aware the high voltage!!! So don t do if you are not a professional.

Finally, upload code from this repository to your ESP8266 module.

Do not forget to change the password for the AP in the ino file and the standard SSID and password in the settings.h file.

Check out the [Homebridge plugin](https://github.com/Uweklaus/homebridge-esp-windowshades). It was created to allows you to integrate your ESP8266 module with Apple HomeKit platform and Siri.

# Usage

- Current position
```
GET /window/0/currentPosition HTTP/1.1
```

- Position state
```
GET /window/0/positionState HTTP/1.1
```

- Target position
```
GET /window/0/targetPosition HTTP/1.1
```


```
POST /window/1/targetSetPosition HTTP/1.1
Content-Type: application/json

value=78
```
# DONE
V 0.0.9 stable
- running, but no targetPosition GET HttpMethod
- Up and Down with same timing 

V 0.1.0
- read targetPosition by GET HttpMethod
- Up and Down have different timings, to achieve differences in moving speed

V0.2.0
- Added a AP webserver, if no WiFi is available to change the SSID and password
- SSID, Password and data are stored directly in the EEPROM
- Webserver added to change the timings, pin asignment and read the current and targetPosition
- Standard data can be loaded

V0.2.1
- switched off second wifi (AP) when connected to network

# TODO
- out of position after changing target position several times in a short time, e.g. by the homekit slider. 

# License

ISC
