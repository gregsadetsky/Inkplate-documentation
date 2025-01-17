Inkplate Peripheral Mode
========================
    Peripheral mode for Inkplate by Soldered
    Peripheral mode is uploaded to each Inkplate. It enables you to use the board
    without reprogramming. You just need to send commands via UART and it will
    show contents on its screen. 
    You can send commands via USB port or by directly connecting to ESP32 TX and RX pins.

    Here is an `example <https://github.com/SolderedElectronics/Inkplate-Peripheral-Mode-Raspberry-Pi-Example>`_ on how to use peripheral mode to drive Inkplate with a Raspberry Pi.
    And `here <https://github.com/SolderedElectronics/Inkplate-Peripheral-Mode-STM32-Example>`_ is one for driving Inkplate with STM32.

    Don't forget you need to send #L(1)* after each command to show it on the display (equal to display.display()). 
    Peripheral mode Arduino code for all inkplates can be found under examples/Diagnostics if needed to be installed again.
     
    Settings are:
    115200 baud, standard parity, ending with \\n\\r

echo: #?*
---------
    | Check if the Inkplate receives commands on UART
    | Response:  OK

drawPixel: #0(XXX,YYY,CC)*
--------------------------
    | XXX - X coordinate (with leading zeros)
    | YYY - Y coordinate (with leading zeros)
    | CC - Color (with leading zeros)
    | example:
    
.. code-block:: c

    #0(001,005,04)*

drawLine: #1(XXX,YYY,III,JJJ,CC)*
---------------------------------
    | XXX - Start x coordinate (with leading zeros)
    | YYY - Start y coordinate (with leading zeros)
    | III - End x coordinate (with leading zeros)
    | JJJ - End y coordinate (with leading zeros)
    | CC - Color (with leading zeros)
    | example:
    
.. code-block:: C

    #1(001,004,010,123,01)*

drawFastVLine: #2(XXX,YYY,LLL,CC)*
----------------------------------
    | XXX - Start x coordinate (with leading zeros)
    | YYY - Start y coordinate (with leading zeros)
    | LLL - Length of line (with leading zeros)
    | CC - Solor (with leading zeros)
    | example: 
    
.. code-block:: C

    #2(142,425,040,05)*

drawFastHLine: #3(XXX,YYY,LLL,CC)*
----------------------------------
    | XXX - Start x coordinate (with leading zeros)
    | YYY - Start y coordinate (with leading zeros)
    | LLL - Length of line (with leading zeros)
    | CC - Color (with leading zeros)
    | example:
    
.. code-block:: c
    
    #3(123,014,100,03)*

drawRect: #4(XXX,YYY,WWW,HHH,CC)*
---------------------------------
    | XXX - Start x coordinate (with leading zeros)
    | YYY - Start y coordinate (with leading zeros)
    | WWW - Width of rect. (with leading zeros)
    | HHH - Height of rect. (with leading zeros)
    | CC - Color (with leading zeros)
    | example:
    
.. code-block:: c
    
    #4(123,014,050,010,01)*

drawCircle: #5(XXX,YYY,RRR,CC)*
-------------------------------
    | XXX - Start x coordinate (with leading zeros)
    | YYY - Start y coordinate (with leading zeros)
    | RRR - Radius of circle (with leading zeros)
    | CC - Color (with leading zeros)
    | example:
    
.. code-block:: c
    
    #5(050,100,040,01)*

drawTriangle: #6(XX1,YY1,XX2,YY2,XX3,YY3,CC)*
---------------------------------------------
    | XX1 - X coordinate of first corner (with leading zeros)
    | YY1 - Y coordinate of first corner (with leading zeros)
    | XX2 - X coordinate of second corner (with leading zeros)
    | YY2 - Y coordinate of second corner (with leading zeros)
    | XX3 - X coordinate of third corner (with leading zeros)
    | YY3 - Y coordinate of third corner (with leading zeros)
    | CC - Color (with leading zeros)
    | example: 
    
.. code-block:: c
    
    #6(250,250,100,400,375,450,04)*

drawRoudRect: #7(XXX,YYY,WWW,HHH,RRR,CC)*
-----------------------------------------
    | XXX - Start x coordinate (with leading zeros)
    | YYY - Start y coordinate (with leading zeros)
    | WWW - Width of rect. (with leading zeros)
    | HHH - Height of rect. (with leading zeros)
    | RRR - Radius (with leading zeros)
    | CC - Color (with leading zeros)
    | example: 
    
.. code-block:: c
    
    #7(123,014,050,010,005,00)*

fillRect: #8(XXX,YYY,WWW,HHH,CC)*
---------------------------------
    | XXX - Start x coordinate (with leading zeros)
    | YYY - Start y coordinate (with leading zeros)
    | WWW - Width of rect. (with leading zeros)
    | HHH - Height of rect. (with leading zeros)
    | CC - Color (with leading zeros)
    | example:
    
.. code-block:: c
    
    #8(123,014,050,010,01)*

fillCircle: #9(XXX,YYY,RRR,CC)*
-------------------------------
    | XXX - Start x coordinate (with leading zeros)
    | YYY - Start y coordinate (with leading zeros)
    | RRR - Radius of circle (with leading zeros)
    | CC - Color (with leading zeros)
    | example:
    
.. code-block:: c
    
    #9(050,100,040,01)*

fillTriangle: #A(XX1,YY1,XX2,YY2,XX3,YY3,CC)*
---------------------------------------------
    | XX1 - X coordinate of first corner (with leading zeros)
    | YY1 - Y coordinate of first corner (with leading zeros)
    | XX2 - X coordinate of second corner (with leading zeros)
    | YY2 - Y coordinate of second corner (with leading zeros)
    | XX3 - X coordinate of third corner (with leading zeros)
    | YY3 - Y coordinate of third corner (with leading zeros)
    | CC - Color (with leading zeros)
    | example:
    
.. code-block:: c
    
    #A(250,250,100,400,375,450,04)*

fillRoudRect: #B(XXX,YYY,WWW,HHH,RRR,CC)*
-----------------------------------------
    | XXX - Start x coordinate (with leading zeros)
    | YYY - Start y coordinate (with leading zeros)
    | WWW - Width of rect. (with leading zeros)
    | HHH - Height of rect. (with leading zeros)
    | RRR - Radius (with leading zeros)
    | CC - Color (with leading zeros)
    | example:
    
.. code-block:: c
    
    #B(123,014,050,010,005,00)*

print: #C("STRING")*
--------------------
    | STRING - Text/Strig coded in HEX Char (example: HELLO WORLD would be coded like 48454c4c4f20574f524c44, where 48 means 0x48 which is H in ASCII table)
    | example: for HELLO WORLD:
    
.. code-block:: c
    
    #C("48454c4c4f20574f524c44")*

setTextSize: #D(NN)*
--------------------
    | NNN - Text scaling (with leading zeros)
    | example:
    
.. code-block:: c
    
    #D(02)*

setCursor: #E(XXX,YYY)*
-----------------------
    | XXX - X position of text cursor (with leading zeros)
    | YYY - Y position of text cursor (with leading zeros)
    | example:
    
.. code-block:: c
    
    #E(002,010)*

setTextWrap: #F(T/F)*
---------------------
    | T - True if enable text wraping
    | F - False if disable text wraping
    | example: 
    
.. code-block:: c
    
    #F(T)* or #F(F)*

setRotation: #G(RRR)*
---------------------
    | RRR - Sets rotation (0-3, where each increment rotates whole screen by 90 deg)
    | example:
    
.. code-block:: c
    
    #G(003)*

drawBitmap: #H(XXX,YYY,"PATH")*
-------------------------------
    | XXX - X position of bitmap on display
    | YYY - Y position of bitmap on display
    | PATH - path to bitmap image on SD card, where path should be sent as HEX Char (same as for print command). Example: /image1.bmp should be sent as 2f696d616765312e626d70
    | example:  (2f696d616765312e626d70 means /image1.bmp)
    
.. code-block:: c

    #H(000,000,"2f696d616765312e626d70")* 
    
    | Response:
    
.. code-block:: c

    #H(1)* - Image loaded succesfully
    #H(0)* - Image load failed
    #H(-1)* - SD Card Init Error

| Note: This will not work on Inkplate 2, because it has no SD card slot

setDisplayMode: #I(D)*
----------------------
    | D - Display Mode (D = 3 -> 3 bit mode, D = 1 -> 1 bit mode)
    | example:
    
.. code-block:: c

    #I(3)* or #I(1)*

| Note: This will not work on Inkplate 2, because it doesnt't support grayscale

getDisplayMode: #J(?)*
----------------------
    | Response:
    
.. code-block:: c

    #J(1)* - 3 bit mode
    #J(0)* - 1 bit mode

clearDisplay: #K(1)*
--------------------
    | Clears display.

display: #L(1)*
---------------
    | Displays image buffer data to screen.

partialUpdate: #M(YY1, XX2, YY2)*
---------------------------------
    | YY1 - Start Y position of part of the screen that will be updated
    | XX2 - End X position of part of the screen that will be updated
    | YY2 - End Y position of part of the screen that will be updated
    | example:
    
.. code-block:: c
    
        #M(005,400,040)*

| Note: This will not work on Inkplate 2, because it has no partialUpdate support

readTemperature: #N(?)*
-----------------------
    | Response:
    
.. code-block:: c
    
    #N(23)* - 23 Celsius degrees

| Note: Not supported on Inkplate 2

readTouchpad: #O(P)*
--------------------
    | P - Name of pad that needs to be read (1, 2 or 3)
    | Response:
    
.. code-block:: c
    
    #O(1)* for high state of pad 
    or 
    #O(0)* for low state of pad

| Note: Not supported on Inkplate 2

readBattery: #P(?)*
-------------------
    | Response:
    
.. code-block:: c
    
    #P(3.65)* - Measured voltage on battery is 3.65VDC

| Note: Not supported on Inkplate 2

panelSupply(einkOff/on):#Q(S)*
------------------------------
    | S - State of panel power supply (S = 1 -> panel has power supply, S = 0 -> panel power supply has benn turned off)

    | Note: Not supported on Inkplate 2

getPanelState: #R(?)*
---------------------
    | Response:
    
.. code-block:: c
    
    #R(1)* - panel has power supply or #R(0)* - panel supply has been turned off

| Note: Not supported on Inkplate 2

drawImage: #S(XXX,YYY,"PATH")*
------------------------------
    | XXX - X position of bitmap on display
    | YYY - Y position of bitmap on display
    | PATH - path to bitmap image on SD card, where path should be sent as HEX Char (same as for print command). Example: /image1.bmp should be sent as 2f696d616765312e626d70
    | example:  (2f696d616765312e626d70 means /image1.bmp)

.. code-block:: c

    #S(000,000,"2f696d616765312e626d70")* 

    | Response:

| Note: This will not work on Inkplate 2, it has no SD card slot

drawThickLine: #T(XXX,YYY,III,JJJ,TT,CC)*
-----------------------------------------
    | XXX - Start x coordinate (with leading zeros)
    | YYY - Start y coordinate (with leading zeros)
    | III - End x coordinate (with leading zeros)
    | JJJ - End y coordinate (with leading zeros)
    | TT - Line thickness
    | CC - Color (with leading zeros)
    | example:

.. code-block:: C

    #T(001,004,010,123,05,01)*

drawElipse: #U(XXX,YYY,RRX,RRY,CC)*
-----------------------------------
    | XXX - Start x coordinate (with leading zeros)
    | YYY - Start y coordinate (with leading zeros)
    | RRX - X radius (with leading zeros)
    | RRY - Y radius (with leading zeros)
    | CC - Color (with leading zeros)
    | example:

.. code-block:: c

    #U(050,100,040,070,01)*


fillElipse: #V(XXX,YYY,RRX,RRY,CC)*
-----------------------------------
    | XXX - Start x coordinate (with leading zeros)
    | YYY - Start y coordinate (with leading zeros)
    | RRX - X radius (with leading zeros)
    | RRY - Y radius (with leading zeros)
    | CC - Color (with leading zeros)
    | example:

.. code-block:: c

    #V(050,100,040,070,01)*


rtcSetTime: #W(H,M,S)*
----------------------
    | H - Hours
    | M - Minutes
    | S - Seconds

    | example:
.. code-block:: c

    #W(15,22,30)*


rtcSetDate: #X(WD,D,M,Y)*
-------------------------
    | WD - weekday
    | D - day
    | M - month
    | Y - year

    | example:
.. code-block:: c

        #X(4,23,3,2023)*


rtcSetEpoch: #Y(E)*
-------------------
    | E - Time in epoch

    | example:
  .. code-block:: c

        #Y(1679581587)*  


rtcGetRtcData: #a(D)*
---------------------
    | D - What data do you want to return? [0, 6]
    | 0 - rtcGetSecond();
    | 1 - rtcGetMinute();
    | 2 - rtcGetHour();
    | 3 - rtcGetDay();
    | 4 - rtcGetWeekday();
    | 5 - rtcGetMonth();
    | 6 - rtcGetYear();

    | example:
  .. code-block:: c

     #a(2)*  or #a(5)*


rtcSetAlarm: #b(AS,AM,AH,AD,AW)*
--------------------------------
    | AS - Alarm seconds
    | AM - Alarm minutes
    | AH - Alarm hours
    | AD - Alarm day
    | AW - Alarm weekday

    | example:
  .. code-block:: c

        #b(0,30,15,23,4)*  


rtcSetAlarmEpoch: #c(AE,AMC)*
-----------------------------
    | AE - Alarm epoch
    | AMC - Alarm matching (see System.h)

    | example:
  .. code-block:: c

        #c(1679581587, 2)*


rtcCheckAlarmFlag: #d(?)*
-------------------------
    | Response:

    .. code-block:: c

        #d(1)* - if the alarm flag is 1
        #d(0)* - if the alarm flag is 0


rtcClearAlarmFlag: #e(1)*
-------------------------
    | Clears alarm flag.


rtcGetAlarm: #f(D)*
-------------------
    | D - Which component of the alarm want to get [0, 4]
    | 0 - rtcGetAlarmSecond();
    | 1 - rtcGetAlarmMinute();
    | 2 - rtcGetAlarmHour();
    | 3 - rtcGetAlarmDay();
    | 4 - rtcGetAlarmWeekday();

    | example:
  .. code-block:: c

        #f(3)* or #f(1)*


rtcTimerSet: #g(SC,V,IE,IP)*
----------------------------
    | SC - rtcCountdownSrcClock -> [0,3], see System.h
    | V - Coundowntime in seconds
    | IE -> 1 = enable interrupt; 0 = disable interrupt
    | IP -> 1 = interrupt generate a pulse; 0 = interrupt follows timer flag

    | example:
  .. code-block:: c

        #g(2,10,0,0)* 


rtcCheckTimerFlag: #h(?)*
-------------------------
    | Response:

  .. code-block:: c

        #h(1)* - if the flag is 1
        #h(0)* - if the flag is 0

rtcClearTimerFlag: #i(1)*
-------------------------
    | Clears timer flag.



rtcDisableTimer: #j(1)*
-----------------------
    | Disables the timer.



rtcIsSet: #k(?)*
----------------

    | Response: 

  .. code-block:: c

        #k(0)* - if RTC is not set
        #k(1)* - if RTC is set


rtcReset: #l(1)*
----------------
    | Resets RTC



**Note**: Next functions are only for Inkplate 6PLUS


frontlight: #m(F)*
------------------
    | F -> 1 to turn on; 0 to turn off the frontlight

    | example:
    .. code-block:: c

        #m(1)* or #m(0)*


setFrontlight: #n(BR)*
----------------------
    | BR - brightness [0, 63]

    | example:
    .. code-block:: c

        #n(50)* 


tsInit: #o(PWRS)*
-----------------
    | PWRS -> 1 for display.tsInit(1); 0 for display.tsInit(0);

    | example:
    .. code-block:: c

        #o(1)* or #o(0)*


tsShutdown: #p(1)*
------------------
    | Turns off touchscreen power.



tsAvailable: #r(?)*
-------------------
    | Response:

  .. code-block:: c

        #r(0)* - if not available or
        #r(1)* - if available

tsGetData: #s(?)*
-----------------
    | Response: 

  .. code-block:: c

        #s(x, y)* 
        

tsGetRawData: #t(?)*
--------------------
    | Response: raw data from the touchscreen in binary format


touchInArea: #u(XXX,YYY,TW,TH)*
-------------------------------
| touchInArea checks if touch occured in given rectangle area.

    | XXX - rectangle top left corner x plane
    | YYY - rectangle top left corner y plane
    | TW - rectangle width
    | TH - rectangle height

    | example:
    .. code-block:: c

        #u(0,0,200,300)* 
