# ELECTROMYOGRAPHIC SIGNALS
The implementation of the mathematical tool known as Discrete Wavelet Transform (DWT), its adaptation in the company Microchip's microcontroller PIC18F2550, and its subsequent use for the analysis of electrical signals sent by motor neurons to the common flexor muscle of the fingers of the hand is presented

In the realization of the project, the analysis of the electromyography signal was achieved through the DWT mathematical tool for the recognition of one of the possible states studied: open hand or closed hand. The information about the state was sent via Bluetooth by serial communication to a Bluetooth terminal on a cell phone with an Android system, where the current state of the hand is shown in a designed App.
## INTRODUCTION
Electromyography (EMG) is a diagnostic procedure used primarily to assess the health of muscles and the nerve cells that control them (motor neurons). Motor neurons produce electrical signals that cause muscles to contract. The study of electrical stimuli in muscles is performed by means of sensors called electrodes. The electrodes can be of the needle type, being embedded in the muscle (invasive), or by means of surface electrodes (non-invasive).

With the help of the superficial electrodes adhered to the skin, it is possible to study the electrical nerve conduction and thus measure the speed and intensity of the signals that move between two or more points. Now, in our project, we propose using the signal generated by the surface electrodes to identify at least two positions or movements of the hand in order to be applied in technological and engineering advances rather than preferentially medicinal matters in a new version of the project.For example, the remote control of a robotic hand that manipulates dangerous substances for a human being by means of the analysis of the EMG signal; that is to say, that the movement of the robotic hand is a faithful copy of the human hand.

The use of the Fourier Transform (FT) in the mathematical analysis of electrical signals is common. However, the FT is frequently used for signals that are, in some way, periodic in time; in the case of EMG signals, there is no evidence of periodicity in time because it is a signal localized in time.For this reason, and the fact that the FT requires the use of complex numbers and could occupy a larger memory space in the PIC18F2550 microcontroller, the use of the Wavelet Transform (WT) was chosen.

Unlike in the FT analysis, where the basis functions are sines and cosines of infinite length, in the WT analysis the basis are functions located in frequency (dilation) and time (translation). Thus, WT analysis is suitable for analyzing EMG signals; however, we are faced with the problem of properly selecting the basis or wavelet family to use. In the project, WT with Haar mother Wavelet was selected, since this is the simplest Wavelet family to use and, consequently, to program.

The signal to be analyzed by means of the DWT is a signal generated by the MyoWare AT-04-001 sensor. This is input to the PIC18F2250 microcontroller where the signal is converted from analog to digital and the DWT is performed. When the DWT process is finished, the microcontroller analyzes the transformed signal and through Rs232 serial communication to a Bluetooth module, the movement information is sent to a mobile device with Android operating system. By means of a mobile application, it is evidenced which of the two movements was performed.

##TARGETS
- Describe the signal generated by the electromyography sensor (100%).

- To create code in C that allows the Discrete Wavelet Transform to be realized using the Wavelet Haar family.(100%)

- To perform Rs232 serial communication between the microcontroller and Bluetooth module and mobile device (100%).

- To design an application for mobile devices with the Android operating system that allows one to visualize in real time the movement made by the hand. (100%)

- Develop a prototype that integrates all the components and/or devices necessary for the realization of the system of acquisition, processing, analysis, and recognition of electromyography signals (100%).

## BLOCK DIAGRAM
![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/imagen/diagrmaDeBloques.png)

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/imagen/diagrmaEsquimatico.png)

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/imagen/esquematicoLM317TG.png)

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/imagen/esquematicoLM7805.png)

## PRINTED CIRCUIT

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/imagen/dise%C3%B1oCircuito1.png)

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/imagen/dise%C3%B1oCricuito2.png)

## TROUBLESHOOTING GUIDE
- The EMG sensor has a gain adjustment screw, which can become either very sensitive or insufficiently sensitive to EMG signals. 

- - This was solved by establishing a single site on the forearm to place the sensor and adjusting it to a medium gain.

- When performing analog-to-digital conversion (ADC) it was evident that the signal oscillated between values of 450 to 550 units on the scale of [0, 1024] units when the hand was closed and remained at 400 when it was open. These are very small changes compared to the reference scale, in addition to being very noisy.

- - The code and the Wavelet approximation were adjusted so that the noise was filtered by the DWT (2nd approximation). This allowed the changes to be more accurate and not oscillate between values for the same movement. 

- The signal provided by the EMG sensor is localized in a time lapse. This causes the signal to be captured only once and lost even with the hand closed. It is necessary that the user continues to exert force on his closed hand for this signal to remain in time.

- - This is a problem with the functioning of the EMG sensor. It was solved by suggesting extending the force to close the hand, as well as establishing a delay in the App code for the reception of information via Bluetooth.

- The serial communication of the PIC18F2250 and the sending through the Bluetooth module to the cell phone is too fast for the mobile device to decode the information. Therefore, the App was not able to change the image even if the circuit elements before this block performed their tasks well. 

- - It was proposed to add a delay between each data send from the PIC18F2550 to the Bluetooth module, even with the delay of the App. This change solved the problem of decoding the information on the mobile device.

- To avoid problems in possible failures of the prototype and to save time in identifying the problem, it was proposed to program the DWT in a programming language different from the one used for the PIC18F2550 and test it. With this action, the DWT operation was ruled out as an error. However, when translating the code to C language, there were several problems in the Wavelet coefficient matrix, where the values disappeared or behaved as null values.

- - This was solved by performing a new translation of the DWT code to C language. 


## OPERATION MANUAL

- Each electrode of the AT-04-001 sensor is provided with an adhesive to place it as well as possible on the common flexor muscle of the fingers of the hand.

- Connect the AT-04-001 sensor to the equipment in the input properly marked and arranged exclusively for the sensor.

- Turn on the device and the AT-04-001 sensor.

- Open the "EMG" App on the mobile device.

- Pair the Bluetooth of the equipment with the Bluetooth of the mobile device.

- When the status changes to "Connected" in the App, it is possible to open or close the hand to display the status on the mobile device.

- Adjust the gain of the AT-04-001 sensor if necessary.
--------------------------------------------------------------------------------------------------
## LOGBOOK
>  ### Monday, July 29, 2019.
For this day, reading and programming of the ADC and serial communication with the help of the DataSheet of the PIC18F2550 microcontroller was performed. The test run will be performed next session.
The ADC was made with the following specifications:
Acquisition Time: 1MHz
Conversion Time: 0.000016 s

> ### Thursday, August 01, 2019.
The characterization of the Myoware Muscle Sensor AT-04-001 was performed, and the characteristics were summarized as shown below:

#### MyoWare Muscle Sensor Characterization AT-04-001
![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/imagen/MyoWareMusculeSensor1.png)

##### Features:
- 3V to 5V power supply.
- Reverse polarity protection.
- Outputs.     	
- - Amplified EMG.
- - Amplified, rectified and integrated EMG.
- Adjustable signal amplification.

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/imagen/MyoWareMusculeSensor2.png)

The differences between the different signal types are shown in Figure 3. Within these three signals, the supplier recommends the use of the amplified, rectified and integrated EMG signal (EMG SIG) for microcontroller processing. In addition, it indicates that all output signals are centered on an offset of Vs/2, where Vs is the maximum voltage of the ADC.

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/imagen/MyoWareMusculeSensor3.png)

**NOTE:** An attempt was made to perform ADC verification on PIC18F2550, but due to additional permissions for ADC verification via serial communication, the test could not be performed. Therefore, it is postponed to the next session.

> ### Saturday, August 03, 2019.

A search was performed for the creation of the Wavelet Transform inside the PIC18F2550. Performing the evaluation of what was needed for the project, it was found that the Wavelet Transform with the least memory consumption was the Haar Mother Wavelet.

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/imagen/wavelet1.png)

> ### Monday, August 05, 2019.

It was possible to configure the HC-06 bluetooth module for computer-to-cell phone communication. It was successfully performed sending information from the PIC18F2550, but it was not possible to send concise information via the Bluetooth module. It is believed that the error is in the ADC because it was successfully achieved sending the initial text "Initialization of analog/digital conversion."

We continue with the problem of sending this information by serial cable to the computer. This communication is still not successfully achieved. 

> ### Tuesday, August 06, 2019.

The ADC was tested along with the serial communication and the Arduino serial terminal to the computer. The test was successful for a DC signal, controlling the input voltage to the PIC18F2550 with a potentiometer. 

The integration of the values on the serial output to a.txt file is planned for the function graph to be input to the PIC18F2550. This signal should be equal to the signal input to the micro-controller.

> ### Thursday, August 08, 2019.

The ADC of a sinusoidal signal was successfully performed on the PIC18F2550. This signal was sent via serial communication to a Bluetooth module, which was subsequently sent to a cell phone with a Bluetooth terminal. The application allows you to send the data collected on your cell phone in a.txt file, which is plotted in an attempt to reconstruct the signal.The sine signal was reconstructed but does not have much detail (or a smooth reconstruction) of the function. It is left as a task to change the sampling frequency.

> ### Mars August 12, 2019.

The sampling frequency change was performed. Sampling with acceptable resolution at 500 Hz was achieved. Discrete Wavelet transform with Wavelet Haar family in FORTRAN language was performed and is functional. We will continue with the translation of the DWT in FORTRAN language to C language to be implemented in the PIC18F2550.

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/Wavelet/Original%20-%20128%20points.png)

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/Wavelet/6th%20approximation.png)

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/Wavelet/5th%20approximate.png)

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/Wavelet/4th%20approximation.png)

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/Wavelet/3rd%20approximation.png)

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/Wavelet/2nd%20approximation.png)

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/Wavelet/1st%20approximation.png)

![](https://github.com/jucgarciagon/Se-alesElectromiograficas/blob/main/Wavelet/0th%20approximation.png)

> ### Thursday, 15th of August, 2019

We successfully performed ADC signal sending with a maximum frequency of 1 kHz.

> ### The 17th of August, 2019

Started translation of discrete wavelet transform code with Harr mother wavelet kernel in the FORTRAN language to the C language. 

> ### Sunday, August 18, 2019.

The application that will allow visualization of the current state of the hand was successfully realized. The app was developed on the MIT app inventor website. When the cell phone bluetooth receives a "5", it changes the image to "Gripped". With any other value, the app arranges the image to "Open". 

> ### Monday, August 19, 2019.

The first translation of the discrete Wavelet transform on the PIC18F2550 microcontroller was attempted, unsuccessfully. It is believed that there may be an error in how the filling and calling of the wavelet coefficient vector are being performed.

> ### Tuesday, 20th of August, 2019.

We successfully performed the translation of the Wavelet Haar transform from the FOTRAN language to the C language. The wavelet transform of a sinusoidal signal from the signal generator was performed by the PIC18F2550.

With the transform working correctly, the coupling of all the parts of the project was carried out. With everything assembled, we proceeded to perform the tests with the sensor, the microcontroller, Bluetooth module, and the EMG App. These tests were successful, but the response times of the App and the serial sending of the Bluetooth module must be corrected in the programming.

> ### Thursday, August 22, 2019.

The printed circuit board was designed for bakelite assembly. This design was sent to CNC cutting.
