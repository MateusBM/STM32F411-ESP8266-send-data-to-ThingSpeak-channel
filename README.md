# STM32F411-ESP8266-send-data-to-ThingSpeak-channel
Using the STM32F411 board and ESP8266 wi-fi module to send data to a ThingSpeak channel<br/>
This test project was made with the help of professor Marcos Zuccolotto (github.com/Zucco2007).

<h2>Connections:</h2>

The ESP8266* pins are connected in the following way:

<table>
  <th>ESP8266</th><th>STM32</th>
  <tr>
    <td>GPIO15</td>
    <td>GND</td>
  </tr>
    <tr>
    <td>GPIO2</td>
    <td>VCC</td>
  </tr>
    <tr>
    <td>GPIO0</td>
    <td>VCC</td>
  </tr>
    <tr>
    <td>CH_PD</td>
    <td>VCC</td>
  </tr>
    <tr>
    <td>REST</td>
    <td>VCC</td>
  </tr>
    <tr>
    <td>GPIO15</td>
    <td>GND</td>
  </tr>
    <tr>
    <td>TXD</td>
    <td>PA10</td>
  </tr>
    <tr>
    <td>RXD</td>
    <td>PA9</td>
  </tr>
    <tr>
    <td>VCC</td>
    <td>VCC</td>
  </tr>
    <tr>
    <td>GND</td>
    <td>GND</td>
  </tr>
</table>

*<b>Don't EVER connect the ESP8266 to 5V unless you want some wireless silicon toast</b><br/>

<h2>AT commands:</h2>

By now you should have everything working just fine, but just to be sure upload the provided code, open your favorite serial terminal (I recommend Termite, but it's just a personal preference) and type the following AT commands:<br/><br/>

<b>AT</b>      You should see an "OK" as response<br/>
<b>AT+GMR</b>      It should respond with the module's firmware version<br/>

<h2>First setup</h2>

It's very likely that if you try to use any other AT command it won't work, that's because the CWMODE isn't set to 1, to do that simply type <b>AT+CWMODE=1</b> on the serial monitor, it should answer back with an OK.<br/>

<h2>Sending data to ThingSpeak channel:</h2>

To send stuff to your ThingSpeak channel first you must have an accont already set up (it's pretty easy, there's no need for a tutorial) and then simply send through the serial monitor the following commands:<br/><br/>

<b>AT+CWJAP="ssid","password"</b>      Where ssid is your network name and password is the network password<br/>
<b>AT+CIPMUX=1</b>      Enables multiple connections<br/>
<b>AT+CIPSTART=4,"TCP","184.106.153.149",80</b>      Starts the connection to the ThingSpeak server<br/>
<b>AT+CIPSEND=4,44</b>      Starts the send command<br/>
<b>GET /update?key=tskey&fieldx=val</b>      Where tskey is your ThingSpeak channel key, x is the channel field and val is the value you want to send<br/>

To send something else you must start the connection again, so you will need to repeat steps 3, 4 and 5.
