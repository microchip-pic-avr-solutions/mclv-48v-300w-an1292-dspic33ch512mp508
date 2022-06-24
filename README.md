![image](images/microchip.jpg) 

## MCLV-48V-300W dsPIC33CH512MP508 AN1292

## 1. INTRODUCTION
<p style='text-align: justify;'>
This document describes the setup requirements for running the Sensorless FOC algorithm using
PLL Estimator, which is referenced in AN1292 “Sensorless Field Oriented Control (FOC) for a Permanent Magnet Synchronous Motor (PMSM) Using a PLL Estimator and Field Weakening (FW)” using MCLV-48V-300W Inverter Board and dsPIC33CH512MP508 Motor Control Dual In-line Module (DIM).</p>



## 2.	SUGGESTED DEMONSTRATION REQUIREMENTS

### 2.1 Motor Control Application Firmware Required for the Demonstration
To clone or download this application from Github, go to the [main page of this repository](https://github.com/microchip-pic-avr-solutions/mclv-48v-300w-an1292-dspic33ch512mp508) and then click Clone button to clone this repository or download as zip file.
> **_NOTE:_**
>In this document, hereinafter this firmware package is referred as firmware.
### 2.2 Software Tools Used for Testing the firmware

- MPLAB® X IDE v5.50 
- MPLAB® XC16 Compiler v1.70
- MPLAB® X IDE Plugin: X2C-Scope v1.3.0 
- DFP: dsPIC33CH-MP_DFP v1.9.207 
> **_NOTE:_**
>The software used for testing the firmware prior to release is listed above. It is recommended to use the version listed above or later versions for building the firmware.
### 2.3 Hardware Tools Required for the Demonstration
- MCLV-48V-300W Inverter Board (EV18H47A)
- 	dsPIC33CH512MP508 Motor Control DIM (EV62P66A)
- 24V Power Supply [(AC002013)](https://www.microchipdirect.com/dev-tools/AC002013)
- 24V 3-Phase Brushless DC Motor [(AC300020)](https://www.microchip.com/en-us/development-tool/AC300020)
  <br />
> **_NOTE:_**
> All items listed under the section Hardware Tools Required for the Demonstration are available at [microchip DIRECT]()https://www.microchipdirect.com/

## 3. HARDWARE SETUP
<p style='text-align: justify;'>This section describes hardware setup required for the demonstration.</p>

1. <p style='text-align: justify;'> Motor currents are amplified by the amplifiers ( U10 and U11 )on the MCLV-48V-300W Inverter Board. By default, the firmware and DIM are configured to sample and convert external amplifier outputs ('external Op Amp configuration'), measuring the motor currents needed for implementing FOC.</p>

2. <p style='text-align: justify;'> Insert the dsPIC33CH512MP508 Motor Control DIM into the DIM Interface Connector J8 provided on the MCLV-48V-300W Inverter Board. Make sure the DIM is placed and oriented correctly.</p>

    <p align="left">
    <img  src="images/dimconnected.PNG"></p>


3. <p style='text-align: justify;'> Connect the three phase wires from the motor to PHA, PHB, and PHC terminals of connector J4 (there is no specific order) provided on the MCLV-48V-300W Inverter Board.</p>
    <p align="left">
      <img  src="images/motorconnection.png"></p>

4. <p style='text-align: justify;'>	Plug in the 24V power supply to connector J1 provided on the MCLV-48V-300W Inverter Board. Alternatively, the Inverter Board can also be powered through Connector J3.</p>
      <p align="left">
      <img  src="images/mclvpower.png"></p>
 

 5.	<p style='text-align: justify;'>The board has an onboard programmer ‘PICkit™ On Board (PKoB4)’ , which can be used for programming or debugging the dsPIC33CH512MP508. To use an on-board programmer, connect a micro-USB cable between Host PC and Connector J16 provided on the MCLV-48V-300W Inverter Board.</p>


      <p align="left">
     <img  src="images/mclvpkob4.png"></p>

 6.	<p style='text-align: justify;'>Alternatively, the device can also be programmed using the programmer/debugger (MPLAB® PICkit™ 4 In-Circuit Debugger - PG164140) by interfacing it through connector J9 of the MCLV-48V-300W Inverter Board as shown below. Ensure that the programmer is oriented correctly before proceeding.</p> 

      <p align="left">
       <img  src="images/mclvprogramming.PNG"></p>
 
<br />

## 4. SOFTWARE SETUP AND RUN
### 4.1 Setup: MPLAB X IDE and MPLAB XC16 Compiler

Install MPLAB X IDE and MPLAB XC16 Compiler versions that support the device dsPIC33CH512MP508 and PKoBv4. The MPLAB X IDE, MPLAB XC16 Compiler, and X2C-Scope plug-in used for testing the firmware are mentioned in the [Motor Control Application Firmware Required for the Demonstration](#21-motor-control-application-firmware-required-for-the-demonstration) section. To get help on  

- MPLAB X IDE installation, refer [link](https://microchipdeveloper.com/mplabx:installation)
- MPLAB XC16 Compiler installation steps, refer [link](https://microchipdeveloper.com/xc16:installation)

<p style='text-align: justify;'>If MPLAB IDE v8 or earlier is already installed on your computer, then run the MPLAB driver switcher (It is installed when MPLAB®X IDE is installed) to switch from MPLAB IDE v8 drivers to MPLAB X IDE drivers. If you have Windows 7 or 8, you must run MPLAB driver switcher in ‘Administrator Mode’. To run the Device Driver Switcher GUI application as administrator, right click on the executable (or desktop icon) and select ‘Run as Administrator’. For additional details refer MPLAB X IDE help topic <i>“Before You Begin: Install the USB Device Drivers (For Hardware Tools): USB Driver Installation for Windows Operating Systems”</i>. </p>

### 4.2  X2C-Scope
<p style='text-align: justify;'>
X2C-Scope is a MPLAB X IDE plugin that allows a developer to interact with an application while the application program is running. X2C-Scope enables you to read, write, and plot global variables (for motor control) in real time. It communicates with the target using the UART. To use X2C-Scope, the plugin must be installed:</p>

- In MPLAB X IDE, select <i>Tools>Plugins</i> and click on the Available Plugins tab.
- Select X2C-Scope plug-in by checking its check box, and then click Install.
- Look for tool X2C-Scope under <i>Tools>Embedded.</i>

<p align="left">
  <img  src="images/x2cscopeconfiguration.png"></p>
 
<br />

## 5.  BASIC DEMONSTRATION
### 5.1 Firmware Description

The firmware version needed for the demonstration is mentioned under the [Motor Control Application Firmware Required for the Demonstration](#21-motor-control-application-firmware-required-for-the-demonstration) section.
<p style='text-align: justify;'>
This firmware is implemented to work on Microchip’s dual-core 16-bit Digital signal controller (dsPIC® DSC) dsPIC33CH512MP508. There are two independent dsPIC DSC Cores called ‘Main Core’ and ‘Secondary Core’ in the device. For more information, see the dsPIC33CH512MP508 Family datasheet.</p>

<p style='text-align: justify;'>In MPLAB X IDE, the code for two cores is developed as separate projects with the following device selections.</p>

- <p style='text-align: justify;'>Device selection in Main Project (code for Main Core) is dsPIC33CH512MP508
- <p style='text-align: justify;'>Device selection in Secondary Project (code for Secondary Core) is dsPIC33CH512MP508S1

Hence the firmware used in this demonstration consists of two MPLAB X projects, main.X (Main Project) and pmsm.X (Secondary Project). 

The firmware directory structure is shown below:
    <p align="left">
       <img  src="images/folderStructure.png"></p>

> **_NOTE:_**
> The project may not build correctly in Windows OS if Maximum path length of any source file in the project is more than 260 characters. In case absolute path is exceeding or nearing maximum length, do any (or both) of the following:
> - Shorten the directory name containing the firmware used in this demonstration. If you renamed the directory, consider the new name while reading the instructions provided in the upcoming sections of the document.
> - Place firmware in a location, such that absolute path length of each file included in the projects does not exceed the Maximum Path length specified. 
Refer to MPLAB X IDE help topic <i>“Path, File, and Folder Name Restrictions”</i> for details.</p>

<p style='text-align: justify;'> The function of the Main Core is defined by the Main Project main.X and they are:

- <p style='text-align: justify;'>To set device Configuration bits applicable for both Main and Secondary cores (Con-figuration bits for Main and Secondary cores exist in Main core). Note that the Configu-ration bits decide the I/O port ownership between Main Core and Secondary Core. 
- <p style='text-align: justify;'>Configure Main Core Oscillator Subsystem to generate clocks needed to operate Core and its peripherals. In the firmware, Main is configured to use at 90MHz.
- <p style='text-align: justify;'>To program and enable the Secondary core by invoking XC16 library (libpic30.h) routines <i>_program_secondary()</i> and <i>_start_secondary()</i>.

<p style='text-align: justify;'>The function of the Secondary Core (as defined in the Secondary Project pmsm.X) is:

- <p style='text-align: justify;'>To configure Secondary Core Oscillator Subsystem to generate clocks needed to operate Core and its peripherals. In the firmware, the Secondary core is configured to operate at 100MHz.

- <p style='text-align: justify;'>To configure I/O ports and Secondary Core peripherals (such as PWM Generators PG1, PG2, and PG3, ADC Cores, UART1) required to function the firmware.

- <p style='text-align: justify;'>To execute the Motor Control Demo Application based on the Microchip Application note AN1292. 

<p style='text-align: justify;'>Once Main Core programs and enables the Secondary Core, it can autonomously run the Motor Control Demo application residing in its PRAM. The Motor Control Demo application uses a push button to start or stop the motor and a potentiometer to vary the speed of the motor.</p>

For more details, refer to Microchip Application note AN1292 “Sensorless Field Oriented Control (FOC) for a Permanent Magnet Synchronous Motor (PMSM) Using a PLL Estimator and Field Weakening (FW)” available on the [Microchip website](https://www.microchip.com//).

### 5.2 Basic Demonstration
<p style='text-align: justify;'>
Follow below instructions step by step to setup and run the motor control demo application:</p>

1. <p style='text-align: leftjustify;'> Start MPLAB X IDE and open<span style="font-family:Courier New; font-size:;"> (File>Open Project)</span> the Main project <span style="font-family:Courier New; font-size:;">main.X</span> with device selection dsPIC33CH512MP508 (Main core).</p>
    <p align="left">
       <img  src="images/idedeviceselection.png"></p>
  

2. <p style='text-align: leftjustify;'> Set the project <span style="font-family:Courier New; font-size:;">main.X </span>as main project by right clicking on the project name and selecting 'Set as Main Project' as shown. The project <b>'main'</b> will then appear in bold.</p>
    <p align="left">
     <img  src="images/ideprojectsetup.png"></p>
 

	
3. <p style='text-align: leftjustify;'> In the project window, right click on the Secondaries folder of the project tree (of Main project <span style="font-family:Courier New; font-size:;">main.X</span>) and select "Properties". This will open the "Secondaries"category of the Project Properties dialog. </p>
    <p align="left">
     <img  src="images/SecondariesProperties.png"></p>

     <p style='text-align: leftjustify;'>

<p style='text-align: leftjustify;'>Verify the “Secondaries” category of Project Properties dialog, and ensure details are as follows (see figure):</p>

- Item is <span style="font-family:Courier New; font-size:;">pmsm.X </span>
- Image name is <i>“pmsm”</i>
- Check Box <i>"Build"</i> is checked
- Check Box <i>"Debug"</i> is unchecked
        <p align="left"> <img  src="images/SecondaryPropertiesSelect.png"></p>

> **_NOTE:_**
>You may encounter build error,</p>
> - If any of the values are not as mentioned above 
> - If the secondary project <span style="font-family:Courier New; font-size:;">pmsm.X </span> is moved or deleted from the firmware directory 

4. <p style='text-align: leftjustify;'>In the Projects window, right-click on the Secondaries folder of the project tree (of Main project <span style="font-family:Courier New; font-size:;">main.X</span>) and select the project “pmsm.” This will open the Secondary project <span style="font-family:Courier New; font-size:;">pmsm.X</span> in the MPLAB X IDE project window. Alternatively, you can open <span style="font-family:Courier New; font-size:;">(File>Open Project)</span> the Secondary project from its current location like any other MPLAB X project.</p> 
     <p align="left"> <img  src="images/openSecondaryproject.png">></p>

     The selected device in Secondary project <span style="font-family:Courier New; font-size:;">pmsm.X</span> can be viewed by opening its Project Property Dialog. As can be seen from the figure below, this device is set as dsPIC33CH512MP508S1, representing the secondary core of the dsPIC33CH512MP508. 

     <p align="left"> <img  src="images/SecondariesPropertiesConfig.png"></p>

5. Unfold Header Files folder of Secondary project tree and click open the header file <span style="font-family:Courier New; font-size:;">userparms.h</span> in Editor window. Verify header file <span style="font-family:Courier New; font-size:;">userparms.h</span> (included in the Secondary project <span style="font-family:Courier New; font-size:;">pmsm.X</span>) to ensure macro definitions <span style="font-family:Courier New; font-size:;">TUNING, OPEN_LOOP_FUNCTIONING, TORQUE_MODE and SINGLE_SHUNT</span> is not defined.
     <p align="left"> <img  src="images/configParam.png"></p>

   > **_NOTE:_**
   > <p>The motor phase currents can be reconstructed from the DC Bus current by appropriately sampling it during the PWM switching period, called a single-shunt reconstruction algorithm. The firmware can be configured to demonstrate the single shunt reconstruction algorithm by defining the macro<span style="font-family:Courier New; font-size:;">‘SINGLE_SHUNT’</span> in the header file userparams.h 
   >For additional information, refer to Microchip application note <b>AN1299, “Single-Shunt Three-Phase Current Reconstruction Algorithm for Sensorless FOC of a PMSM.”</b>
   >By default, the firmware uses phase currents measured across the phase shunt resistors on two of the half-bridges of the three-phase inverter (‘dual shunt configuration’) to implement FOC.

6. Right click on the Main project <i>main.X</i> and select “Properties”  to open its Project Properties Dialog. Click the “Conf: [default]” category to reveal the general project configuration information. The development tools used for testing the firmware are listed in the section [2.2 Software Tools Used for Testing the firmware](#22-software-tools-used-for-testing-the-firmware).
   <p style='text-align: justify;'>
    In the <b><i>‘Conf: [default]’</i></b> category window: 
    <p style='text-align: justify;'>
 - Select the specific Compiler Toolchain from the available list of compilers. Please ensure MPLAB® XC16 Compiler supports the device dsPIC33CH512MP508.In this case, “XC16(v1.70)” is selected.
      <p style='text-align: justify;'>
 - Select the Hardware Tool to be used for programming and debugging. 
       <p style='text-align: justify;'>
-	Select the specific Device Family Pack (DFP) from the available list of Packs. In this case, “dsPIC33CH-MP_DFP 1.9.207” is selected.     
 -   After selecting Hardware Tool and Compiler Toolchain, click button <b>Apply</b>
        <p align="left">
        <img  src="images/projectpropertiessettings.png"></p>

7. Right click on the associated Secondary project <i>pmsm.X</i> and select “Properties”  to open its Project Properties Dialog. Click the “Conf: [default]” category to reveal the general project configuration information.</p>

   <p style='text-align: justify;'>
    In the <b><i>‘Conf: [default]’</i></b> category window: 

     - Select the specific Compiler Toolchain from the available list of compilers. Please ensure MPLAB® XC16 Compiler supports the device dsPIC33CH512MP508S1.<p style='text-align: justify;'>
     
     -   After selecting Hardware Tool and Compiler Toolchain, click button <b>Apply</b>

     This step is required to build the Secondary Project with a specific compiler version.

8. <p style='text-align: justify;'>To build the Main project (in this case <span style="font-family:Courier New; font-size:;">main.X</span>) and program the device dsPIC33CH512MP508, click <b>'Make and Program Device Main project'</b> on the toolbar. Upon this, MPLAB X IDE begin executing the following activities in order:</p>

     - Builds Secondary project pmsm.X (linked to Main project)
     - Builds Main project main.X
     - Programs the Main flash memory of dsPIC33CH512MP508 with code generated when building the Main Project and the Secondary Project. </p>

    <p align="left">
    <img  src="images/deviceprogramming.png"></p>

     > **_NOTE:_**
     > <p style='text-align: justify;'>In this firmware configuration, the Main Core programs the Slave Core. When device is programmed, the Slave core image is placed in the Main flash. When the Main Core is powered on and begins execution of code, it transfers the Slave image from the Main flash to the Slave PRAM.  </p>
  
7. <p style='text-align: justify;'>	 	If the device is successfully programmed, <b>LD2 (‘LED1’)</b>  will be turned ON, indicating that the dsPIC® DSC is enabled. </p> 
    <p align="left">
     <img  src="images/led.png"></p>


8. <p style='text-align: justify;'> 	Run or stop the motor by pressing the push button <b>SW1</b>. The motor should start spinning smoothly in one direction in the ‘Normal Speed Range’. Ensure that the motor is spinning smoothly without any vibration. The LED <b>LD3 (‘LED2’)</b> is turned ON to show the button is pressed to start the motor </p>
     <p align="left">
     <img  src="images/pushbuttons.png"></p>
 

9.  <p style='text-align: justify;'> The motor speed can be varied using the potentiometer (labeled <b>'POT1'</b>).</p>
    <p align="left">
    <img  src="images/potentiometer.png"></p>

 
10.	<p style='text-align: justify;'>To enter the extended speed range (NOMINAL_SPEED_RPM to MAXIMUM_SPEED_RPM) press the push button <b>SW2</b>. Press the push button <b>SW2</b> again to revert the speed of the motor to its normal speed (END_SPEED_RPM to NOMINAL_SPEED_RPM) range. </p>
      <p align="left">
     <img  src="images/stopButton.png"></p>
  

11. <p style='text-align: justify;'>	Press the push button <b>SW1</b> to stop the motor.</p>


>**_NOTE:_**
>The macro definitions END_SPEED_RPM, NOMINAL_SPEED_RPM, and MAXIMUM_SPEED_RPM are specified in userparms.h file included in the project pmsm.X. The definitions NOMINAL_SPEED_RPM, and MAXIMUM_SPEED_RPM are defined as per the specification provided by the Motor manufacturer. Exceeding manufacture specification may lead to damage of the motor or(and) the board. 

## 5.3  Data visualization through X2C-Scope Plug-in of MPLABX
<p style='text-align: justify;'>
 X2C-Scope is a third-party plug-in for MPLAB X, which helps in real-time diagnostics. The application firmware comes with the initialization needed to interface controller with the host PC to enable data visualization through X2C-Scope plug-in.</p>

1. Ensure X2C-Scope Plug-in is installed. For additional information on how to set up a plug-in refer [https://microchipdeveloper.com/mplabx:tools-plugins-available](https://microchipdeveloper.com/mplabx:tools-plugins-available)
 
2.	To establish serial communication with the host PC, connect a micro-USB cable between the host PC and the MCLV-48V-300W Inverter Board (connector J16). This interface is also used for programming.


3. Ensure application is configured and running as described under Section [Basic Demonstration](#5-basic-demonstration   ) by following steps 1 through 13.

4. Build the secondary project pmsm.X. To do that, right-click on the project <span style="font-family:Courier New; font-size:;">pmsm.X</span> and select “Clean and Build.”</p>
      <p align="left">
       <img  src="images/PMSMCleanBuild.png"></p>

5. Ensure that the checkbox “Load symbols when programming or building for pro-duction (slows process)” is checked, which is under the “Loading” category of the Project Properties window. </p>
      <p align="left">
       <img  src="images/LoadingPMSMSetting.png"></p>

6. Open the X2C-Scope window by selecting <span style="font-family:Courier New; font-size:;">Tools>Embedded>X2CScope.</span></p>
      <p align="left">
       <img  src="images/x2cselection.png"></p>
 
7. Open the X2C-Scope Configuration window and in <b>'Select project'</b> menu, select <b>pmsm</b> project as shown.
    <p align="left">
    <img  src="images/x2cprojectselection.png"></p>

8.	Serial communication needs to be set up, as shown in the following figure. Ensure the communication baud rate is set to 115200 as configured in the application firmware. The COM port used depends on the system settings. The <span style="font-family:Courier New; font-size:;">refresh button</span> lists the available COM Ports. Select the COM Port as per the connection.

    <p align="left">
     <img  src="images/x2cconnectionsetup.png"></p>
 


9. Once the COM port is detected, click on <b>'Disconnected'</b> and turn to <b>'Connected'</b>, to establish a serial communication between Host PC and the board.
     <p align="left">
    <img  src="images/x2cconnectionbutton.png"></p>


10. Set the <b>'Project Setup'</b> as shown below and click <b>'Set Value'</b>. Set Scope sample time as interval at which <span style="font-family:Courier New; font-size:1;">X2CScopeUpdate()</span> is called. In this application it is every 50µs.
      <p align="left">
      <img  src="images/x2cprojectsetup.png"></p>


11. When the setup is established, click on open scope View (under sub window <b>'Data Views'</b>), this opens 'Scope Window'.
     <p align="left">
      <img  src="images/x2cdataview.png"></p>
    	     

12. In this window, select the variables that needs to be monitored. To do this, click on the source against each channel, a window Select Variables opens upon the screen. From the available list, the required variable can be chosen. Ensure check boxes Enable & Visible are checked for the variables to be plotted.<br>
To view data plots continuously, uncheck <span style="font-family:Courier New; font-size:1;">Single-shot </span>. When <span style="font-family:Courier New; font-size:1;">Single-shot</span> is checked it captures the data once and stops. The Sample time factor value multiplied with Sample time determines the time difference between any two consecutive data points on the plot.
    <p align="left">
    <img  src="images/x2cdatapointselection.png"></p>

13.	Click on <b>'SAMPLE'</b>, then X2C-Scope window shows variables in real time, which is updated automatically.
     <p align="left">
     <img  src="images/x2csample.png"></p>
 

14.	Click on <b>'ABORT'</b> to stop.
     <p align="left">
     <img  src="images/x2cabort.png"></p>
 
 ## 6. REFERENCES:
For additional information, refer following documents or links.
1. AN1292 Application Note “[Sensorless Field Oriented Control (FOC) for a Permanent Magnet Synchronous Motor (PMSM) Using a PLL Estimator and Field Weakening (FW)](https://ww1.microchip.com/downloads/aemDocuments/documents/OTH/ApplicationNotes/ApplicationNotes/01292A.pdf)”
2. AN1299 Application Note “[Single-Shunt Three-Phase Current Reconstruction Algorithm for Sensorless FOC of a PMSM](http://ww1.microchip.com/downloads/en/appnotes/01299a.pdf)”
3. MCLV-48V-300W Inverter Board User’s Guide 
4. dsPIC33CH512MP508 Family datasheet [(DS70005371D)](https://ww1.microchip.com/downloads/en/DeviceDoc/dsPIC33CH512MP508-Family-Data-Sheet-DS70005371D.pdf)
5. [Family Reference manuals (FRM) of dsPIC33CH512MP508 family](https://www.microchip.com/en-us/product/dsPIC33CH512MP508#document-table)
6. MPLAB® X IDE User’s Guide (DS50002027) or MPLAB® X IDE help
7. [MPLAB® X IDE installation](http://microchipdeveloper.com/mplabx:installation)
8. [MPLAB® XC16 Compiler installation](http://microchipdeveloper.com/xc16:installation)










