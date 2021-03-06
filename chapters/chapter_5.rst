Connecting sensors
------------------



Distance Sensors
================


Infra-red sensor
~~~~~~~~~~~~~~~~


Overview of the experiment
^^^^^^^^^^^^^^^^^^^^^^^^^^

In this experiment the IR sensor module is interfaced with
anuduino.We use 3 LEDs One as transmitter, One as receiver
and other LED as indicator.Whenevr IR receiver gets signal
the third LED glows. The IR is connected to analog pin 2 (ADC1).


Components required
^^^^^^^^^^^^^^^^^^^

- Breadboard    x1
- Attiny85      x1
- Resistors(68 x2, 1.5k x1, 10k x1)
- ZenerDiode(3.6v)  x2
- USB               x1
- IR-sensor module  x1
- LED               x2


Schematic
^^^^^^^^^
.. image:: ../images/16_IR-Anuduino_schem.png
    :scale: 110%


Circuit diagram
^^^^^^^^^^^^^^^


.. image:: ../images/16_IR-Anuduino_bb.png
   :scale: 80%

Code
^^^^

.. code-block::  c


	#include <DigiUSB.h>

	void setup() {
	  DigiUSB.begin();
	  pinMode(2,INPUT);
	}

	void loop() {
	  // print output
	  DigiUSB.println("Waiting for input...");
	  // get input
	  int val=analogRead(1);
	  DigiUSB.println(val);
	  DigiUSB.refresh();
	  DigiUSB.delay(500);
	}
	











Environmental Sensors
=====================


Temperature sensor
~~~~~~~~~~~~~~~~~~


Overview of the experiment
^^^^^^^^^^^^^^^^^^^^^^^^^^

The Thermistor is interfaced with Anuduino in this experiment. 
Here the thermistor is conncted to analog pin 2 of Attin85. The 
circuit is connected on breadboard as shown in the below figures.
and The circuit is connected to the computer through USB. The thermistor 
reads the temperature from pin 2 and displays on the monitor of computer. 


Components Required
^^^^^^^^^^^^^^^^^^^

- Breadboard    x1
- Attiny85      x1
- Resistors(68 x2, 1.5k x1, 10k x1)
- ZenerDiode(3.6v)  x2
- USB        x1
- Thermistor  x1


Schematic
^^^^^^^^^

.. image:: ../images/14_Thermistor-Anuduino_schem.png
   :scale: 125%

Circuit Diagram
^^^^^^^^^^^^^^^

.. image:: ../images/14_Thermistor-Anuduino_bb.png
   :scale: 80%

Code
^^^^

.. code-block::  c


	// this sketch reads data from thermistor and takes average of 30 samples in 4 seconds
	
	
	#include <DigiUSB.h>
	#define TEMP 1 //using PB2 as analog INPUT

	void setup() {
	  DigiUSB.begin();
	  pinMode(2, INPUT); //defining PB2 as INPUT
  
	}

	void returnTemp( int degree ){
  
	  float celsius;
	 int sample;
	 int thirty_samples;
 
	   for (sample = 0; sample < 29; sample++) {
        // convert PB2 value to temperature
        celsius = ((float)analogRead(TEMP) * 5.0 / 1024.0);
        celsius = celsius / 0.01;
        // sample every 100 milliseconds
        delay(100);
        // sum of all samples
        thirty_samples = thirty_samples + celsius;
        DigiUSB.refresh();
       
	    }

    celsius = thirty_samples / 30.0; //taking average
 
	  if ( degree == 1 ){
    DigiUSB.print(celsius);
    DigiUSB.println("C");
    DigiUSB.delay(10);
  
	}
	  }
  

	void loop() {
  
	returnTemp(1); //calling function to output temp
	DigiUSB.delay(990);

	}


Humidity Sensor
~~~~~~~~~~~~~~~


Overview of the experiment
^^^^^^^^^^^^^^^^^^^^^^^^^^

The DHT11 is interfaced with Anuduino in this experiment. 
Here the humidity sensor is conncted to analog pin 2 of Attin85. The 
circuit is connected on breadboard as shown in the below figures.
and The circuit is connected to the computer through USB. The temperature
values are observed on monitor by using DigiUSB. we can Watch both
temperature and humidity by interfacing bluetooth with this circuit. 
Code is different for that which is mentioned below.


Components required
^^^^^^^^^^^^^^^^^^^

- Breadboard    x1
- Attiny85      x1
- Resistors(68 x2, 1.5k x1, 10k x1)
- ZenerDiode(3.6v)  x2
- USB        x1
- Humidity-sensor(dht-11)  x1


Schematic
^^^^^^^^^

.. image:: ../images/15_Humidity_sensor_schem.png
    :scale: 125%

Circuit diagram
^^^^^^^^^^^^^^^

.. image:: ../images/15_Humidity_sensor_bb.png
   :scale: 80%

Code_1
^^^^^^

.. code-block::  c


	// this sketch reads data from humidity sensor and takes average of 30 samples in 4 seconds
	//@Author_Nivedita Tigadi//
	
	
	
	#include <DigiUSB.h>
	#define TEMP 1 //using PB2 as analog INPUT

	void setup() {
	  DigiUSB.begin();
	  pinMode(2, INPUT); //defining PB2 as INPUT
  
	}

	void returnTemp( int degree ){
  
	 float celsius;
	 int sample;
	 int thirty_samples;
 
	   for (sample = 0; sample < 29; sample++) {
        // convert PB2 value to temperature
        celsius = ((float)analogRead(TEMP) * 5.0 / 1024.0);
        celsius = celsius / 0.01;
        // sample every 100 milliseconds
        delay(100);
        // sum of all samples
        thirty_samples = thirty_samples + celsius;
        DigiUSB.refresh();
       
	    }

    celsius = thirty_samples / 30.0; //taking average
 
	  if ( degree == 1 ){
    DigiUSB.print(celsius);
    DigiUSB.println("C");
    DigiUSB.delay(10);
  
	}
	  }
  

	void loop() {
  
	returnTemp(1); //calling function to output temp
	DigiUSB.delay(990);

	}
	
	
Code_2
^^^^^^
	
.. code-block::  c


    #include <dht11.h>
    #include <SoftSerial.h>
    #include <TinyPinChange.h>
    
    SoftSerial blue(0,1);

    dht11 DHT11;

    #define DHT11PIN 2

    void setup()
    {
      Serial.begin(9600);
      blue.begin(9600);
      //blue.println("DHT11 TEST PROGRAM ");
      //blue.print("LIBRARY VERSION: ");
      //blue.println(DHT11LIB_VERSION);
      //blue.println();
    }
    
    double Fahrenheit(double celsius)
    {
      return 1.8 * celsius + 32;
    }
    
    void loop()
    {
      //blue.println("\n");
    
      int chk = DHT11.read(DHT11PIN);
    
      blue.print("Read sensor: ");
      switch (chk)
      {
        case 0: blue.println("OK"); break;
        case -1: blue.println("Checksum error"); break;
        case -2: blue.println("Time out error"); break;
        default: blue.println("Unknown error"); break;
      }
    
      blue.print("Humidity (%): ");
      blue.println((float)DHT11.humidity, 2);
    
      blue.print("Temperature (oC): ");
      blue.println((float)DHT11.temperature, 2);
    
      //blue.print("Temperature (oF): ");
      //blue.println(Fahrenheit(DHT11.temperature), 2);
    

      delay(2000);
    }

