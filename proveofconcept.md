## Fast prototyping with open source hardware
---

This page describes a few predefined steps involved in evaluating the concept of using "Open Source Hardware when prototyping new products".
Our main target is not to use standardized open source hardware directly in production. It is rather to learn how we can work with open source hardware to enhance our development process further. What we learn through our evaluation shall at the end of the day influence on our mainstream development, by enabling us to build even better products, faster and at a lower cost.

## Open Source Hardware
---
You will find a wide range of open source hardware devices out there. We will however limit our study to a few of the better known ones:
* BeagleBone
* Raspberry pi
* Arduino

A few other ones can be add for our initial studies when we find it appropriate.

Like Cypress CY8CKIT or NXP LPCXpresso.

See also: http://makezine.com/2013/04/15/arduino-uno-vs-beaglebone-vs-raspberry-pi/

See also: http://randomnerdtutorials.com/arduino-vs-raspberry-pi-vs-beaglebone-vs-pcduino/

## Step 01 - Evaluate candidates for further study 
---
This initial study work is about collecting further information about above mentioned open source hardware candidates.
Below some examples of information that are of interest:  

* Performance.
* Price.
* How is Open Source defined for product in question?
* Development resources. Supporting tools etc.
* Limiting factors.
* License models such as GPL or LGPL. What are we allowed to do and what can't we do?

Other characteristics can be described too when we find it appropriate. 

Information collected via this step will be documented at: [[AAB_DEVELOPMENT:Proof_Of_Concept_Fast_Prototyping_Step_1_Results|Documentation - Step 1]]


## Step 02 - Evaluate candidates for further study
---
We expect that open source hardware potentially could be used when prototyping many of our products. This study is however limited to evaluate how we can use open source hardware for our prototyping of a new PowerLink+ module.

The PowerLink+ module to be developed shall be rather generic, as we want it to:
* Serve as a PLP ECU that simultaneously collects input from minimum six grain-loss sensors and and makes related data available on the PLP bus.
* Serve as a PLP node that implements a PID controller enabled to control the speed of a hydraulic driven shaft.
* Serve as a PLP node that implements a PID controller enabled to control the position of a LA12 actuator piston.
* Serve as a PLP node that control the flow through a TeeJet sprayer regulation valve.  

The purpose of this step is to evaluate how above mentioned requirements influences on our final selection of a piece of open source hardware. We need to obtain a basic understanding of PLP communication, and we need to understand the HW requirements imposed by the tasks that we want to solve with this new product. 

We shall also look into methods of how to develop PID controls for various actuators, and consider if we can find a new approach for this work.

The final goal of this step is to select what open source hardware we will order and work with for the remaining of this work. 
 
Information collected via this step will be documented at: [[AAB_DEVELOPMENT:Proof_Of_Concept_Fast_Prototyping_Step_2_Results|Documentation - Step 2]]

## Step 03 - Suggest extensions for the PLP protocol
Some commands will need to be added to the PLP protocol to allow this new product to implement the features defined in Step 2. 

We will define our extensions to the protocol via this step. We can however only describe those extensions when we have a better understanding of:

* The PLP protocol.
* The grain-loss sensor.
* PID control of a hydraulic driven shaft.
* PID control of the actuator position.
* PID control of the flow through a sprayer regulation valve.  

Information collected via this step will be documented at: [[AAB_DEVELOPMENT:Proof_Of_Concept_Fast_Prototyping_Step_3_Results|Documentation - Step 3]]

## Step 04 - Prepare our hardware for development 
---
We will receive our open source hardware and start working with it. We want to make it easy for others to repeat this step in case they will use similar hardware for other projects. We will for this reason document our work for later reference.
 
Information collected via this step will be documented at: [[AAB_DEVELOPMENT:Proof_Of_Concept_Fast_Prototyping_Step_4_Results|Documentation - Step 4]]

## Step 05 - Develop PLP grain-loss sensor ECU 
---
We will write the software needed to enable our open source hardware device to join the PLP bus and respond to messages concerning the grain-loss registered by six connected grain-loss sensors.

We will use a CAN-analyzer to verify the functionality of what we develop.

Information collected via this step will be documented at: [[AAB_DEVELOPMENT:Proof_Of_Concept_Fast_Prototyping_Step_5_Results|Documentation - Step 5]]

##  Step 06 - Develop PID control of a hydraulic driven shaft 
---
We will write the software needed to enable our open source hardware device to join the PLP bus and control a hydraulic driven shaft. This is about implementing a PID controller that can receive e.g. set-points via the PLP bus.

We will test on a mechanical setup in the testhall and e.g. use a CAN-analyzer to verify the functionality of what we develop.

We want to experiment with methods like automated code generation from Matlab/Simulink during this step. 

Information collected via this step will be documented at: [[AAB_DEVELOPMENT:Proof_Of_Concept_Fast_Prototyping_Step_6_Results|Documentation - Step 6]]

## Step 07 - PID control of the actuator position
---
We will write the software needed to enable our open source hardware device to join the PLP bus and control the position of a LA12 piston. This is about implementing a PID controller that can receive e.g. set-points via the PLP bus.

We will test on a mechanical setup in the testhall and e.g. use a CAN-analyzer to verify the functionality of what we develop.

We want to experiment with methods like automated code generation from Matlab/Simulink during this step. 

Information collected via this step will be documented at: [[AAB_DEVELOPMENT:Proof_Of_Concept_Fast_Prototyping_Step_7_Results|Documentation - Step 7]]

## Step 08 - PID control of the flow through a sprayer regulation valve 
---
We will write the software needed to enable our open source hardware device to join the PLP bus and control the flow through a sprayer regulation valve. This is about implementing a PID controller that can receive e.g. set-points via the PLP bus.

We will test on a mechanical setup in the testhall and e.g. use a CAN-analyzer to verify the functionality of what we develop.

We want to experiment with methods like automated code generation from Matlab/Simulink during this step.

Information collected via this step will be documented at: [[AAB_DEVELOPMENT:Proof_Of_Concept_Fast_Prototyping_Step_8_Results|Documentation - Step 8]]

## Step 09 - Fast prototyping of GUI's 
---
Watch following link[[https://www.youtube.com/watch?v=L1TPs6dI11k|video]]. Will will order the components needed to do something similar. 
The main objective is GUI prototyping, but we will at the same time see if it is realistic that some of our customers can be enabled to develop "simple things" for TeeJet produced devices the same way.

We need case to study. This could e.g. be to develop a small monitor for one of the PLP devices we worked with previously.       

Information collected via this step will be documented at: [[AAB_DEVELOPMENT:Proof_Of_Concept_Fast_Prototyping_Step_9_Results|Documentation - Step 9]]
