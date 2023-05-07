Download Link: https://assignmentchef.com/product/solved-mtrn3500-assignment-2
<br>
<h1>1          Aims</h1>

<ul>

 <li>To implement object-oriented programs using C++.</li>

 <li>To demonstrate interprocess communication and process management.</li>

 <li>To interface with live streams of data and to use them to assist in the tele-operation of a UGV.</li>

</ul>

Note: The word “module” is used to describe a piece of self-contained software. The word “process” is used to describe a module that is running.

<h1>2          Background</h1>

Often, in writing software for Mechatronic Systems, we need to integrate software modules that interact with sensors and actuators and software modules that carry out computational tasks, under the supervision of a process management software module. Rather than building a monolithic application, a multi-process approach can be used to separate functional tasks and to simplify the software development, upgrade and maintenance. Such an approach has the added benefit of limiting the impact of software errors that may occur during operation, via process isolation. As such, we need to use interprocess communication to allow for these specialised processes to communicate with each other.

<h1>3          What is Required of You</h1>

In this assignment, you are expected to write independent modules that interact with each other through shared memory.   At a minimum, your development should include the following software modules:

<ul>

 <li>a Process Management Module module to set up shared memory and to startup, monitor and</li>

</ul>

shutdown the operation of all the modules listed below.

<ul>

 <li>a Laser Module module to interface to a data stream originating from an LMS151 laser rangefinder.</li>

 <li>a GNSS Module to interface to a data stream originating from an Novatel SMART-VI GPS receiver.</li>

 <li>a Vehicle Control Module to control the unmanned ground vehicle.</li>

 <li>a XBox Module to issue commands using an Xbox game controller.</li>

 <li>a Display Module to graphically display the x-y data of the laser range finder and GNSS data in a virtual world.</li>

</ul>

You are then required to (i). demonstrate GPS data display, (ii). demonstrate steering and propulsion control of the UGV and (iii). demonstrate the graphical display of laser data and GPS data. See from Section 4 onwards for the details. Start by completing Part I in Section 4 and then follow the other parts.

<h1>4          Part 1 – Process Management Module</h1>

The purpose of the process management module is to set up shared memory, start up all processes and monitor the operational health of all the processes and finally to shutdown all the processes. Develop the process management module to:

<ol>

 <li>set up shared memory. the shared memory module must have the capability to:

  <ul>

   <li>provide read/write access to laser data.</li>

   <li>provide read/write access to GPS data.</li>

   <li>provide read/write access to Xbox data.</li>

   <li>provide read/write access to vehicle control data.</li>

   <li>provide read/write access to process management data.</li>

  </ul></li>

 <li>start all other processes one by one in the most logical sequence suitable for tele-operation ofthe UGV.</li>

 <li>monitor the heartbeats of all the other processes.</li>

 <li>carry out a complete shutdown in the event the process management process detects the failureof a critically important process.</li>

 <li>attempt to restart a failed non-critical process.</li>

 <li>carry out a routine shutdown of all the processes in response to an Xbox event.</li>

 <li>indicate to all the other modules that it is alive and operational. If process management fails all other processes should terminate.</li>

</ol>

Process Management is the most important module and therefore will form a critical process.

<h1>5          Part 2 – Laser Module</h1>

The UGV mentioned earlier will have its own server running onboard. The purpose of the server is to allow you to interact with the UGV. Therefore, in this part your first task is to establish a Wi-Fi connection with this server over the wireless network. Use 192.168.1.200 as the IP address and 23000 as the port number to connect to and receive laser data. The server will authenticate you as a permitted user, subsequent to which, you will be allowed to connect to the laser rangefinder to enable you to collect laser range data. The most recent laser range data you collected must then be stored as an array of X, Y coordinates in the shared memory for other modules to use.

Incorporate mechanisms in the laser module to enable the process management module to detect the heartbeat of the laser process and for the laser process to respond to shutdown commands form the process management process. This is a critical process for tele-operation.

<h1>6          Part 3 – GNSS Module</h1>

First, establish a Wi-Fi connection with the server over the wireless network. Use 192.168.1.200 as the IP address and 24000 as the port number. The server does not need any authentication. As soon as you connect to the GNSS receiver it will allow you to get global position data records as a continuous stream of binary data. Process the binary data to obtain the X, Y position in UTM coordinates and height in meters, and make them available in the shared memory for other modules to use. In addition, this module should print on the screen, Northing, Easting and Height in meters + the CRC value.

Incorporate mechanisms in the GNSS module to enable the process management module to detect the heartbeat of the GNSS process and for the GNSS process to respond to shutdown commands form the process management process. This is a non-critical process for tele-operation.

<h1>7          Part 4 – Vehicle Control Module</h1>

The purpose of the vehicle control module is to control the UGV. To control the UGV, you must first establish a Wi-Fi connection with the onboard server of the UGV. Use 192.168.1.200 as the IP address and 25000 as the port number to establish this connection. You must send the UGV the following ASCII string to make it move. Replace the field <em><sub>&lt;</sub></em>steer<em><sub>&gt; </sub></em>by a numerical value between ±40<sup>◦ </sup>as the required steering angle and, <em><sub>&lt;</sub></em>speed<em><sub>&gt; </sub></em>by a numerical value between ±1m/s. as the required speed. Replace the <em><sub>&lt;</sub></em>flag<em><sub>&gt; </sub></em>field by 0 and 1 alternatingly to indicate you are actively controlling the vehicle. the spaces and the # are required.

<h2># &lt;steer&gt; &lt;speed&gt; &lt;flag&gt; #</h2>

Incorporate mechanisms in the vehicle control module to enable the process management process to detect the heartbeat of the vehicle control process and for the vehicle control process to respond to shutdown commands form the process management process.

<h1>8          Part 6 – Xbox Module</h1>

You may use the Xbox module you created in MTRN2500 for this purpose. You will be using the Xbox controller to tele-operate the vehicle. Use one of the joysticks to control the speed of the vehicle and another joystick to control the steering of the vehicle. Make the speed and steering commands generated this way available to the vehicle control module through shared memory. In addition, program one of the Xbox buttons to indicate to the process management process to shutdown all modules at the end of your tele-operation.

Incorporate mechanisms in the Xbox module to enable the process management process to detect the heartbeat of the Xbox process and for the Xbox process to respond to shutdown commands form the process management process.

<strong>Note: </strong>If Xbox is disconnected or turned off, set the speed and steering to zero! This is a critical process for tele-operation.

<h1>9          Part 7 – Display Module</h1>

The supplied code (See Assignment 2 page in Moodle) can directly be compiled, linked and executed. When executed, it will show a virtual world centred at the origin of the vehicle coordinate frame which is also called the body fixed coordinate frame. The vehicle coordinate frame is such that the positive <em>x</em>-axis is pointing in the direction of the front of the vehicle, the <em><sub>z </sub></em>axis is vertically up and the <em><sub>y </sub></em>axis is such that it forms a right-handed coordinate frame.

Modify the supplied code, provide access to the shared memory, and plot the laser data and GNSS data in the virtual world. The laser rangefinder’s scanning plane is 30 cm above the ground level. You will then be able to select the pursuit position by pressing the key ’P’ and tele-operate the vehicle using the Xbox controller while visualizing the laser data in real time.


