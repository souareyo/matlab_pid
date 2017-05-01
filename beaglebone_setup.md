## Beaglebone black (BBB) setting up 
After  we received our open source hardware,  which is '''Beaglebone Black Rev C''' ( the specification of  our new  product  can be seen in documentation step 1), we will now  set it up  from our working station (Windows or Linux) and start using it from the scratch in order  to investigate  its basic functionalities.  The settings are  done by following  the instructions, which can be found on  [beaglebone.org](http://beagleboard.org/getting-started). We do recommend  to read these instructions  carefully step-by-step in order to connect Beaglebone to your Working station  and perform the basic settings, powered on, internet connection, driver installation and so on....

When we perform the basic settings on our new Beaglebone, we will also thing about to update it and install some new software on it. For this propose I installed the latest Debian 8. Distribution from 2016 on my 16 BG MicroSD Card. for the software installation and updating, one can follow the following [latest software images](http://beagleboard.org/latest-images)  

Having performed the basic settings, we will now go further and investigate  the different programming possibilities and how  to perform the further settings.  

### Bonescript and cloud9 IDE 


Beaglebone Balck is chipped with JavaScript library, Bonescript, which can be used with its integrated IDE, cloud9 IDE to develop directly on Beaglebone black (BBB) connected  with  the working station, which can be  Windows, Linux or Max. One can also connect BBB via VirtualBox, which I do not recommend for the beginners.  It is  fine to start with cloud 9 and bonescript to get familiar with the built-in functions in Bonescript library and programming on BBB, however, for the complex projects, we do recommend  one of the high level programming languages such as C/C++  with most popular IDE such as Eclipse. In what follows, we will discuss C/C++ Beaglebone (Beaglebone Black Rev C) programming, choosing the working platform (Windows, linux or Mac) and preparing it for BBB toolchain, setting up of eclipse development environment with  C/C++ Development Tools, Cross compilation configuration for BBB Rev C, remote System Explorer configuration, remote deployment configuration and remote debugging configuration.

For the rest of thy study, we will use ubuntu (Debian Distribution) for the Development platform. The   argumentation for this choice can have different explanations from Developer Team and the Company’s working platform, However, it is important to notices that all the  Version of Beaglebone are chipped with the latest Debian Distribution so using  one of the Linux distributions will not be a bad choice.

### Preparing Ubuntu for Beaglebone Programming 


Before we  start  programming on Ubuntu, we need to be sure that some settings have been  done

Install the latest  version of java jdk. To be sure that Java is installed on the machine one can verify it by using the command line in terminal

<pre> java -version </pre>

from my linux working station I got  this:

<pre>java version "1.8.0_111"
Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)</pre> 

<p>

 Of course, yours will be different from this but if you do not get something similar to  aforementioned lines, then you have to go and  install Java before the next steps.

### Install Toolchain for Beaglebone Black (BBB)



To install the cross compilation ''Toolchain'' for beaglebone, we need to know, which armel- architecture we are dealing with. These  can be ''hard-floating point'' or ''soft-floating point''. Beaglebone Black Rev C have ''hard-floating point'', which is represented by prefix  arm-linux-gnueabihf and the preview version have '''soft-floating point'', which is represented by prefix  arm-linux-gnueabi. It is important to know which  architecture we are dealing with in order to install the proper compiler for  the cross compilation. To install the cross compilation package for BBB we will use the following command line:
<pre>sudo apt-get install gcc-arm-linux-gnueabihf</pre>
 
This command line will install the ARM toolchain and you are good to go to cross compilation for Beaglebone Black (BBB) Rev C but you will also need to install G++ compiler for Beaglebone, which is done by the following command line.

<pre> sudo apt-get install g++-arm-linux-gnueabihf </pre> 
These two commands are important for the cross-compilation when we are dealing with C/C++ programming for '''Beaglebone Black Rev C'''.

### Setting up of eclipse 


We have two following ways to install eclipse on the working station:
* Using the following command line :
 sudo apt-get install eclipse eclipse-cdt g++ gcc

The above Command line will successfully the latest version of eclipse, The eclipse C/C++ development tools (CDT), The GNU G++ Compiler and GCC compiler if they are not already  installed on the working box.
* Download the latest version  of java eclipse, then  install  C/C++ Development  Tools  and you are done.
### Toolchain for cross compilation Configuration 


To configure the  Toolchains for cross compiler, we need to crate a C/C++ Project using  the installed eclipse. 

The following steps will resume  this configuration:
If eclipse installation is correct, whenever  we click to File -> New -> C/C++ Project we will see  the following Figure :

[
Under '''Toolchain''' We can choose  Cross GCC or Linux GCC, Empty Project or Hello World Project and click next to see the following windows:

[[File:B2 2.png|none|]([File:B00.png|none]])]

Clinking next , you will the following windows:

[3.png|none|]([File:B3)]

This is one of the most important part  of cross compilation. '''Under Cross Compiler prefix''' and under '''Cross Compiler path''', the prefix and cross compiler path  must be  properly and correctly  set and it only  works if the cross compiler toolchain packages have been properly installed on your  working machine. Clicking to finish, we will see our C/C++ project. Now  it is time to go and configure  the compiler  by following the instructions below:

Right click on the project and then click to '''Properties''' to the project settings windows.

'''Notes: ''' be attention to compiler prefix '''arm-linux-gnueabihf-'''


[5.png]([File:B5)]


We repeat this process for  ''' Cross G++ Compiler ''', ''' Cross G++ Linker ''' and '''Cross GCC Assembler '''. When you are done click '' Apply '' and click '' Ok ''. When we are successfully  done with this configuration we can now compile and see our target compiler from the figure below.

[1.png|none|]([File:B10)]

In what follows, we will configure our  '''Remote System Explorer'''  in order to connect to the remote System, which is Beaglebone Black in this case.

### Remote System Explorer (RSE) 


After we installed  eclipse with CDT, we should  have installed RSE. One can control it by clicking on:

<pre> Windows -> Show View -> Other -> Remote Systems </pre> If it doesn’t success, we can always go 

<pre>  Help -> Install New Software -> Select eclipse release </pre> to install RSE. Now we assume that we have RSE installed when we click 
<pre> Windows -> Show View -> Other -> Remote Systems </pre> We will see   the following windows :

[11.png]([File:B14)]

The local connection contains all the local files in our working station. In order to connect  to BBB, we will either right click to ''local -> new connection '' or simply click to new connection button on  top left of local to  see the following connection windows below:
[1.png]([File:B15)]

Under  the '''Remote System type''' we will choose '''Linux ''' and click next to the dialogue box below:

[1.png|none|]([File:B16)]
The most important information here is the Host name of the Linux system, which is Beaglebone in this case. The host name must be the The IP address of Beaglebone Black Rev C, Which is '''192.168.7.2'''. The other information can something else. For the next, we will choose Remote System using Secure Shell (ssh ) protocol and when we click on finish, we will see the following box:

[1.png]([File:B20)]

The '''User ID''' is required, but it must not necessary be  "root" one can change it to something else. When the remote connection is done, we will access all the  folder on the beaglebone Black. In order  to execute our compiled binary file on Beaglebone, we will copy it and paste into folder under Beablebone root and launch  a '''ssh-terminal''' to execute. This process can be seen in the following windows:
[1.png|none|]([File:B21)]

[1.png]([File:B22)]

[1.png]([File:B23)]

[1.png]([File:B24)]

We now execute our program on Beaglebone Black.

### Remote Deployment 


It is smart and fine to just copy our binary file (Executable file) from eclipse project and  '''Paste ''' it into a folder int Beaglebone Black root folder /root/folder, however there is always the way automate the programming process and save time. To do this, instead of doing '''Copy-Paste all the time''', we will now  remotely  deploy the excutable file directly to Beaglebone Black and execute it from there. In  what  follows, we will explain the remote deployment process. First of all we need to sure that we generate the public key in order to remotely  communicate between beaglebone and the local machine. This is done by executing the following command line and follow the instructions:
<pre> sudo ssh-keygen  </pre> 

When we are done with this process, we will now go to the eclipse project and perform the following settings:

Right  click to project name then click on '''Properties'''

[0.png|none|]([File:R0)]

Under  '''Command ''' do the secure copy of the binary file to beaglebone.  Your file name and the path will be different from mine. Under '''Description ''' you just write what you want. When you are done just hit '''Apply''' and  ''' OK '''. When you are finished with this process, you will need to build the project to see the compilation information similar the following table:
[1.png|none|]([File:R1)]

In case of troubleshooting or if you unfortunately see the information such as ''' No such file or directory ''', we will need to repeat the process by controling ssh-keygen, the Linux file system and path of your folder on Beaglebone. When you are done with the compilation process, you will now go to the Remote System Explorer of course '''' Refresh ''' BBB connection and expand the folder that have been created for the compiled  file. This process can be seen in the following figure.
[2.png|none|]([File:R2)]

From the above figure, we can see the BBTest folder  under Beaglebone connection that I have created to hold the executable file, which is remotely copied to the folder. The last thing we have to do is just to open ssh-terminal for Beaglebone and excute the file and  you are done !!!!


### Remote Debugging 


There is a way  to remotely  debug from beaglebone. But the debate   about if it is necessary  debug  from Beaglebone is open and I am not one of the supporters.
