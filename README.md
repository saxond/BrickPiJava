BrickPiJava
===========

Java implementation of Raspberry PI/Brick Pi interface


This project uses a version of pi4j that has been modified to support a baud rate of 500000.

Some sensors are still missing, the Light, Ultrasonic and Touch are there and (minimally) tested.  The Color Sensors and RCX Light should all follow the Light Sensor pattern, but I don't have any to test. Color Full and I2C sensors are a little different - again, I don't have those sensors.  The EV3 touch and color sensors have been tested.

Motors are implemented.  You can get the instantaneous speed of the motor, as calculated from the encoder values, by means of the `getCurrentSpeed` method of your [Motor](src/main/java/com/ergotech/brickpi/motion/Motor.java) class.  There are problem problems with this, such as if the encoder over/underflows, when changing direction, etc. - create an issue with a good description (and preferably a use-case)  The speed also seems to be double the actual speed.  No real idea why that is, unless the ticks per rev are 1440 and not 720.	

Take a look at the [BrickPiTests.java](src/main/java/com/ergotech/brickpi/BrickPiTests.java) for usage examples.  
Conceptually, it's pretty simple.  You create instances of one of the Sensor classes and/or Motors.  Associate them with the correct port number on the BrickPi instance.  You need to run `setupSensors`, after that, it should all just work. 

The interfaces/APIs may change, but should be pretty stable.
 
Gradle
------

The gradle build can generate IDE projects for Eclipse and IntelliJ and publish the BrickPiJava
library to the local maven repository.  

Building the jar
--------

To build the jar run

    ./gradlew jar
    
The jar will be created in the `build/libs` directory.  Because a modified version of pi4j is used, those classes are included in the generated (fat) jar, and the pi4j library is NOT listed as a 
dependency.

To install to your local maven repository, run

    ./gradlew install

To build the jar file and secure copy it to your Raspberry Pi, run

    PI_PASSWORD=raspberry PI_HOST=192.168.1.44 ./gradlew deploy

(Replace the password and host with the appropriate values for your system).  The `deploy` task uses the `pi` user.
    
Using Eclipse
----------

To generate the Eclipse project files, run

    ./gradlew eclipse 

