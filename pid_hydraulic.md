Having set-up the programming environment of our new open hardware, which is '''Beaglebone Black Rev C''', we will now investigate its  potentiality  for embedded code of Hydraulic motor speed controlled using Matlab and Simulink   PID controller algorithm . To achieve this, we  will start by a brief description of the functional system in order to describe a mathematical model of the controlled system and then implement the Simulink model from  the differential equations. We will  then  generate C/C++ code and  execute it  on the '''Beaglebone Black Rev C'''.
## Overview of the system
The system includes a Tank, a hydraulic Pump, a hydraulic motor, a proportional valve and the electromechanical parts. Our study will be focused on the implementation of  a controlled speed of a hydraulic Motor  using PID controller in Matlab Simulink. The complete documentation of the system can be seen in  Teejet technical information document. So I do not think there is need to go in details about how the system function. Therefore, in the next section, we will sketch the functional schema of the system. Just to figure out how the system function in the  real world.

## Functional Schema
The functional schema of the system is represented on the figure below:

'' The schema will go here ''

## Setup Matlab &  Simulink

To implement the block diagram of the system, Matlab and Simulink 2016b has been used. We started  by installing Matlab Simulink on Linux machine, but  unfortunately,and at the moment of writing  this documentation, Matlab support for Beaglebone Black  is only available on Winddows 64 bit not Linux. Therefore  for the rest of this documentation, we will consider that we are working on Windows Machine 64 bit with at least  windows 8 installed, MATLAB Support Package for BeagleBone Black Hardware and Embedded Coder Support Package for BeagleBone Black Hardware. To find out whether the essential tools are installed, one can write '''ver ''' on matlab command windows.
<pre> ver </pre>
From Matlab tool bar, we can always  install the needed tool packages. Having set Matlab up, in what follows,  we will discuss the different differential equations for the system components and use Matlab and '''Simulink ''' for the  block Diagrams and simulation. If you are new in using Matlab and Simulink, I  do recommend you will you to go on [Step-by-Step Guides to MATLAB and Simulink](https://se.mathworks.com/academia/student_center/tutorials.html).

## Differential Equations
In order to implement the block diagram of the system, we need  the differential equations of the system components and transform them into ''S'' domain using Laplace Transform. To achieve this, we will divide the system in the following part: 
Electro-magnetic, mechanical, hydraulic parts.

### Electro-magnetic part



A PWM (pulse width modulation) signal of 3.3v will be injected in a proportional valve and intensity(current) through coil will generate a flux, the interaction flux-current generate  a  magnetomotive force (MMF). The MMF is the cause  of movement(kinematic) of the cylinder inside the proportional valve, which will direct  control the flow of  fluid (oil) from the tank to the hydraulic motor according to the  supply pressure. The derivative flux created in magnetic circuit can be express as the following expression: 


<math> \frac{d{\Phi}}{dt} =  \frac{V_{c} - RI_{pvl}}{N} </math>

Where:

<math> V_{c} </math> is the signal command, R is winding resistance of coil, '' I '' the current through coil and '' N'' is the number of turns of coil.

On other hand, the force magnetic of the circuit can be expressed  as the  following:

<math>F_{m} = \frac{B^{2}A}{2{\mu}}</math>

Where:

''B'' is the density of flux in magnetic circuit, ''A'' is the area of the cylinder and \mu is the permeability of the  material.

Using the magnetic flux density one can determine the intensity of flux through the magnetic circuit as following :

<math>H_{coil} = \frac{B}{\mu}</math>

Flux intensity inside the aluminium can be loockup using  following hysteresis curve  <math>H_{alum} =f(B)</math>

using the aluminium length and the flux intensity, one can calculate the  magnetomotive force in the magnetic circuit as the following:

<math>MMF =H_{alum}L_{alum} + L_{alum}H_{oil} </math>

Using magnetomotive force and the number of turns of coil the magnetic circuit current through the magnetic circuit can be express as the following:

<math>I_{pvl} = \frac{MMF}{N}</math>

The block Diagram of the magnetic circuit can be seen in  the following figure :

In the what follows, we will focus on dynamic of Proportional valve.

### Mechanical part



The  dynamic of  mechanical part of the system can be represented by the figure below:

[Diagram of the system]([File:Demo_fig.png|450px|thumb|center|Block)]

The Mathematics model of the dynamic part of the system can be represented by the following equation:

<math>M\frac{d^{2}x}{{dt}^{2}} = F_{m} + F_{prs} - F _{pld} - F_{s} - F_{sf} - F _{b}</math>

Where :

<math>M</math> is the mass of the armature of cylinder, <math>F_{m}</math> is the magnetic force of  the armature

<math>F_{prs}</math> is the pressure force, which can be calculated by the following expression:

<math>F_{prs} = P_{s}A </math>

Where:

<math>P_{s}</math> is the pressure supply from the hydraulic pump to proportional valve, and   <math>A</math> is the area of cylinder at  a given position x. The preload force  can be express as the following expression:

<math>F _{pld} = K_{s}l_{pld} </math>

Where <math>K_{s}</math> is a spring constant and <math>l_{pld}</math> is the length of the prelod.


<math> F_{b} = K_{b}V = K_{b}\frac{dx}{dt}</math>


Where <math>F_{b}</math> is a viscous friction force, which is  proportional  of the derivative of the cylinder position and friction constant <math>K_{b}</math> .


<math>F_{s} =K_{s}x </math> 

Where <math>F_{s}</math> is spring force, which is proportional of spring constant and the position of cylinder.

<math>F_{sf} =F_{m} - F _{pld} </math> is a force static of friction.

Finally, the dynamic of the armature can be represented as the following differential equation:


<math>M\frac{d^{2}x}{{dt}^{2}} + K_{b}\frac{dx}{dt} +  K_{s}x = F_{m} +F_{prs} - K_{s}l_{pld} - F_{sf}  </math>
 
Having implemented the dynamic part of the  system, the next section will focus on the  hydraulic of the proportional valve and  the hydraulic motor.

### hydraulic part


This section will discuss the dynamic of  oil flow, the supply pressure from the tank(reservoir) through hydraulic pump to the hydraulic motor, the produced torque and variation of the the motor velocity according to the pressure and flow of oil. To tackle  this will start by the hydraulic of the proportional valve.
Assuming that the supply pressure <math>P_{s}</math> is constant, the flow of oil to the  valve can be calculated by the following expression:

<math>q_{inv} = q_{s} - q_{l} </math>  

Where:

<math>q_{s}</math> - is the supply flow of oil,
<math>q_{l}</math> - is the leakage in valve. The supply flow can be express by the following expression:

<math>q_{s} = K_{p}A_{0}(P_{s} -P_{c})\sqrt{\frac{2}{\rho}|P_{s} -P_{c}|}</math>

Where:

<math>K_{0}</math>  is pressure constant and <math>A{o}</math> is a supply orifice of proportional valve in the a given position xp and <math>\rho</math> is fluid density, which is oil in our case.

<math>P_{s}</math> is supply pressure and <math>P_{c}</math> control pressure

<math>q_{l} = K_{0}A_{0}\sqrt{P_{c}} </math>

<math>q_{inv} = q_{s} -q_{l} = K_{f}A_{0}[-P_{c})\sqrt{\frac{2}{\rho}|P_{s} -P_{c}|} - \sqrt{P_{c}}]((P_{s}) </math>

The control pressure is  a function of flow control <math>q_{inv}</math> in cylinder and the area of cylinder at a given position and can be computed by using the following differential equation:

<math>\frac{dP_{c}}{dt} = \frac{\beta}{x_{p}A_{p}}(q_{inv} - \frac{dx_{p}}{dt}A_{p})</math>

To complete the hydraulic of proportional valve, we will also compute the different forces acting on the piston. This can be computed by the following expression:

<math>M_{p}\frac{d^{2}x}{dt^{2}} =  P_{c}A_{p} - K_{f}x_{p}</math> 

These expressions can be represented by the following Simulink block Diagram:

### Hydraulic Motor


The mathematical model of hydraulic motor should  describe its dynamics which includes the moment inertia, its angular  acceleration, describe the equations of flows( input and output flow), determine the losses in the different parts of hydraulic circuit and the resultant pressures  acting on its shaft. Consider these parameters, one can write the following equations:

<math>\frac{\omega_{m}}{dt} = J_{m}^{-1}[- P_{j})-(M_{i} + b_{\omega}\omega_{m} + b_{p} |P_{i} - P_{j}|.\omega_{m} + b_{k}\omega_{m})](v_{m}f(v)(P_{i}) </math> 

<math>Q_{i,j} =v_{m}f(v)\omega_{m} - K_{lea}P_{i,j} </math> 

Where:

<math>\omega_{m}</math> - is angular speed of the hydraulic motor;

<math>J_{m}</math> - is the moment of inertia of the  motor hydraulic motor according to rotating masses of working echanism;

<math>v_{m}</math> - is the hydraulic motor maximal  geometric volume;

<math> f(v) </math> - is a parameter of regulation; – 1≤  f (v) ≤ 1

<math> b_{\omega},b_{p}, b_{k}, k_{lea} </math> -  are the coefficient of hydraulic motor hydro mechanical losses depending on motor angular speed, pressure, coefficient of hydro mechanical losses and coefficient of leakage.

<math>M_{i} </math> -  is moment of inertia of mechanism.

<math>Q_{i,j} </math> - is the flow of fluid in node '' (i,j) '' of the hydraulic circuit. This can be  positive or negative.

<math>P_{i} - P_{j} </math> - is  the variation of pressure in node (''i,j'').


## Special Case study 

In case of our study, we will focus on a hydraulic motor of type '''Danfoss OMP 100 Hydraulic Motor - Model: 151-0312'''. The specifications of the this motor can be found  [here](http://danfoss-hydraulic-motors-india.blogspot.dk/2015/06/danfoss-omp-100-hydraulic-motor-model.html).
The system is composed on a hydraulic pump a tank,  a proportional valve and a hydraulic motor. The functional schema of  the system can be found on Teejet Technical document. In the study, we will focus on block diagram  of the system, which we can see on the figure below:


[Diagram of the system]([File:Block_diagram.png|450px|thumb|center|Block)]
  
  
Consider the oil flow  from the proportional valve and the pressure, and based on the proportional Technical data (Pressure, flow and current) the linear equation of flow through proportional valve can be written the following equation:

### Transfer function of Proportional valve




'''Note''' In this study we will note use a spool position so the use of <math>Fm</math> described in the previous section is not needed, we will instead  use the current as input of the proportional valve.  

<math>f(i_v) = k_{qi} i_v + K_{estm} </math>

Where 

<math> i_{v} </math> is the current  through proportional valve, which is function of the resistance in proportional valve and the voltage.

<math>K_{qi}</math> is the  coefficient of flow current,

<math>K_{estm} </math> is the estimation coefficient, which can be positive or negative

One can estimate These coefficients by using proportional valve information from '''Comatrol''', which can be found [here](http://www.comatrol.com/attachments/article/300/PFC12-PC%20Catalog%20Page.pdf)

The flow through proportional valve will be the input of the  hydraulic motor.


#### Transfer function of hydraulic motor 


Based on the output of the proportional valve and the flow continuity principle one can write the following equations: 

<math>Q_{l} = K_{qi}i_{v} - K_{p}P_{l}</math>  

<math>Q_{l} =D_{m}\theta_{m} + (C_{tm} + \frac{V_{t}}{4\beta}s)P_{l} </math>


The Torque  produced by  hydraulic motor can be written as the following:

<math>T_{m} = D_{m}P_{l} = J_{m}\frac{d^{2}\theta_{m}(t)}{dt^{2}} + B_{m}\frac{d\theta_{m}(t)}{dt} + G\theta_{m}(t) + T_{l}  </math>

From the 3 aforementioned equations and using Laplace Transform, the transfer function of the motor can be written as following:

<math>\theta_{m}(s) =\frac{\frac{K_{q}}{D_{m}}i_{v}(s) - \frac{K_{fp}}{D_{m}^{2}}(1 +\frac{V_{t}}{4\beta_{e}}s)T_{l}(s)}{\frac{1}{\omega^{2}_{h}}s^{2}+\frac{2\zeta_{h}}{\omega^{2}_{h}}s + 1} </math>


For the sake  of simplicity, some parameters have been simplified or ignored. 

One can  simply see that this transfer function has two different parts. The one is proportional with the output current from the proportional valve. This represents the transfer function of the motor with control flow as input and the speed as the output. The second part of the transfer function is proportional with the external torque ( Disturbance of the system. When We separate these two parameters, we will come to the following transfer functions:

<math>\frac{\omega(s)}{T_{l}(s)} =\frac{\frac{K_{fp}}{D_{m}^{2}}(1 +\frac{V_{t}}{4\beta_{e}}s)}{\frac{1}{\omega^{2}_{h}} s^{2} +\frac{2\zeta_{h}}{\omega^{2}_{h}}s + 1} </math>


<math>\frac{\omega(s)}{Q_{l}(s)} =\frac{\frac{K_{q}}{D_{m}}}{\frac{1}{\omega^{2}_{h}}s^{2}+\frac{2\zeta_{h}}{\omega^{2}_{h}}s + 1} </math>


Where:

<math>\omega_{h} =\sqrt{\frac{4\beta_{e}D_{m}^{2}}{V_{t}J_{m}}} </math>   is the hydraulic resonance frequency in  rd/s.


<math>\zeta_{h} = \frac{K_{q}}{D_{m}}\sqrt{\frac{\beta_{e}J_{m}}{V_{t}}} </math> is hydraulic damping 

<math>V_{t} = V1 + V2</math> 

One can Calculate the total volume as the following:

<math>V_{t} = \frac{Q_{m}.1000.\eta_{v}}{n}</math>

Where:

<math>\eta_{v}</math>     is the volumetric efficiency 

<math>J_{m} =m\frac{D_{m}^{2}}{8} </math>      is the inertia of the motor 

The model of the controlled system ( The model, matlab,C based generated code and all the related files) can be found here:


<pre>\\lhdev\ua\Udv\sw\FastPrototypes\Youssouf\Matlab\PID for Hydraulic Motor\hydrauli_motor_speed_controller_06_03_17 </pre>


The model includes the following  folder and files:

[and files of the model]([File:ModelFolder.png|400px|center|thumb|Folder)]


'''Notes: ''' It is important to noticed that  Matlab  R2016b and Simulink have are used.

If you are  familiar of  Matlab, you can see that the files have different extensions:

The file with the extension '''.slx ''' is the most  important, the one that contains the model itself. There is only one file with  the ''' .slx ''' extension for one simulink model.

The files with the extension ''' .mlx '''  are the LiveScript files for the calculated parameters such as 

'''motor_param.mlx ''', which contains the variables and  the calculated parameters of the transfer function of the hydraulic motor speed (controlled parameters).

'''cal_parm.mlx''' contains the variables and the calculated parameters of proportional valve such as the Resistance ''' R''' and  voltage.

The files with the  extension '''.mat''' are the where the variables are saved in order to be used as  model variables.

The file with the extension '''.sid ''' is the system identification files for the proportional valve, These files are not used in the model because we didn't use the identification for the proportional valve.

The Excel file is to represent the linear equation, which express the  relationship between oil flow and the current through proportional valve.

The other folders, which the name end by ''' grt_rtw ''' contain the generated c based  files  ''' c and h files ''' from the model.



 



<!---

Form this equation, one can derive the angular speed of the hydraulic motor as the following equation:

<math>\frac{\omega_{m}}{dt} = J_{m}^{-1}[- P_{out})- ( B_{m}\omega_{m} + F_{fm} + T_{m} )](D_{m}(P_{in}) </math>

This equation can be represented in the following Simulink block Diagram:



The transfer function of the hydraulic motor can be represented as the following equation:

<math> \frac{\omega_{m}}{x_{p}} = \frac{K_{m}}{(\frac{1}{\omega_{h}^{2}}s^{2} +\frac{2\delta_{h}}{\omega_{h}}s + 1 )} </math>

Where:

<math>\omega_{h} = \sqrt{\frac{2\beta D_{m}^{2}}{J_{m}V_{t}}}</math>

<math>\delta_{h} =\frac{K_{l}}{D_{m}} \sqrt{\frac{\beta J_{t}}{2V_{c}}}</math> 

Where  <math>Q_{inet}</math> is the net flow  from the cylinder to hydraulic motor, <math>\beta</math> is the coefficient of     -->

## Choice of PID Controller
The purpose of this choice is find out how to limit or avoid the fluctuation of hydraulic motor speed with  the input flow or pressure variable. For this regulation we will choose a two stage PID controller which will allows  us to control both the output speed in (rpm) and the input flow of the motor <math>Q_{m}</math>.

In our case, we will design a discrete tunable PID controller and using Matlab toolbox, we will update the different values of the parameters (constants) of controller.

Generally, the differential equation of the controller can be represented as the following equation:

<math>u(t) = K_\text{p} e(t) + K_\text{i} \int_0^t e(t) \,dt + K_\text{d} \frac{de(t)}{dt}</math>

Where:

<math>u(t)</math> - is the output of the controller

<math> e(t) </math> - is the error signal between setpoint and feedback from output signal.

<math> K_\text{p} </math> - is a proportional constant, which is proportional to  signal error ( a kind of amplifier for signal error)

<math>K_\text{i}</math> -  is an integrator constant, which accelerates the process towards the setpoint (reference signal) for the stability point.

<math> K_\text{d}</math> - is a derivative constant, which impact  the stability of the system. The details of PID controller can be found [here](https://en.wikipedia.org/wiki/PID_controller).

Depending on our special case study and after our model, We design a PI controller is enough for the system. 

The block diagram of the system is showing in the following figure:
[Diagram of System with PID regulator]([File:Pi_block_diagram_2.png|400px|center|thumb|Block)]

## Experiments 
From the block diagram of the system and using Matlab Simulink, we perform the following  simulation of the system, which gives the  following results:

[speed and setpoint of system.]([File:SpeedSetPoint.png|500px|center|thumb|Controlled)]


[Controller Parameters]([File:pid_gains.png|400px|center|thumb|)]

## Data Collection Table 
This table contains the symbols, the constants and their units and description. To make it easy to find the values or nature of the different symbols used in the modelling and simulink.

{| class="wikitable"
|-
!width ="100"|Symbols 

!width = "400"|Description

!width ="200"|Values
!width ="100"|Units in SI
!width ="200"|Sources of Info.
|-
|N
|Numner of turns of coil.
| -
| -
|
|-

|R

|Winding Resistance in magnetic circuit
|  Calculated
| <math>\Omega</math>
|
|-
|<math>\mu</math>

|Permeability of aluminium 
|<math>1.256665.10^{6} </math>
|<math>N.A^{2}</math>
|
|-
|<math>D_{m}</math>

|Displacement of hydraulic motor 
|<math>97.3 </math>
|<math>cm^{3}</math>
|
|-
|<math>\omega_{m}</math>

|Defines the number of revolution per minute 
|<math>770</math>
|<math>rpm (rev/min)</math>
|
|-
|<math>T_{m}</math>

|Max. Torque Continous 
|<math>190 </math>
|<math>Nm</math>

|
|-
|<math>J_{m}</math>

|Defines the moment of enertia of  hydraulic motor 
|<math>-</math>
|<math>kgm^2</math>
|
|-
|<math>F_{m}</math>

|Defines forces magnetic. 
|<math>Calculated</math>
|<math>Nm</math>
|
|-
|<math>MMF</math>

|Defines MMF in magnetic circuit 
|<math>Calculated</math>
|<math>A</math>
|

|-

|<math>Q_{m}</math>

|Flow of oil from valve to motor
|<math>Calculated</math>
|<math>l/min</math>
|
|-

|<math>P_{s}</math>

|Spply pressure from pump to proportional valve
|<math> </math>
|<math>bar</math>
|
|-
|<math>\beta_{e}</math>

|Bulk Modulus
|<math> 1.8.10^{9} </math>
|<math>bar</math>
|
|-
|<math>V_{t}</math>
|Total volume of motor
|<math> Calculated</math>
|<math>cm^3</math>
|

|-
|<math>\omega{h}</math>
|Resonance frequency 
|<math> Calculated</math>
|<math>rd/s</math>
|
|}

## Beaglebone Settings for Matlab and Simulink

Beaglebone settings for cross-compilation has been discussed in [Documentation 4](http://bznwiki.spray.com/wiki/AAB_DEVELOPMENT:Proof_Of_Concept_Fast_Prototyping_Step_4_Results) so the rest of this section will  deal with how to install and configure Matlab support for beaglebone hardware and how to configure Matlab and Simulink for C/C++ Code Generation. Therefore in what follows we will discuss about the aforementioned sections. 

### Install Matlab support for Beaglebone Black hardware


Before we generate Matlab code for Beaglebone, we need ensure that Matlab release has the necessary support for Beaglebone hardware and install it on  Matlab. Matlab R2016b has support for Beaglebone Hardware but we have install it. This process is very simple we only need Matlab 'Add-ons ' and follow the instruction.

### C/C++ Code Generation


Matlab r2016b has important features for C/C++ code generation and there are different ways to Generate code from the model or from Matlab itself.

In our case, we need Embedded code from the model. To achieve  this  we need to have ''' Embedded Coder 6.1.1 ''' installed. Matlab r2016b is shipped Embedded coder to sure just write '' ver'' in windows and hit enter to see the list of all the installed  toolbox. If we can not find, it si time to go and install it before the next step. We also need to ensure that the required C/C++ or crosstolchain  are installed and configured properly. We have done with this in [Documentation 4](http://bznwiki.spray.com/wiki/AAB_DEVELOPMENT:Proof_Of_Concept_Fast_Prototyping_Step_4_Results).

The Generated code from the controller can be found:
