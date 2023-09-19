## Converting Between Digital and Analog

Their are 4 types of Digital-Analog Conversion

- **Digital to Digital** : Encode digital data into a digital signal
	- Sending computer data
		- Polar
- **Analog to Digital** : Digitizing an analog
	- Sending voice in telephone (Decrease effect of noise )
- **Digital to Analog** : Modulating a digital signal
	- Sending computer data through public telephone line
- **Analog to Analog** : Modulating an analog signal
	- Sending music from radio station


### Digital to Digital

![[Digital-to-Digital.png|  400]]

![[Digital-to-Digital-2.png| 400]]
#### Unipolar Encoding (One level of value)

**Unipolar encoding** is a line code(a pattern of voltage, current, or photons used to represent digital data) A *positive voltage* represents a *binary 1*, and *zero volts* indicates a *binary 0*.

Anyway, there are two problems in Unipolar Encoding
1. **DC components**
	- Average voltage of the signal in unipolar encoding is *not centered around zero* (tend to be positive)
		- **Voltage Shift**
		- **Loss of Data**
1. **Synchronization**
	- Beginning/ending problem (1111111111)
	- Distortion (four 1111 -> five 11111)

#### Polar Encoding (Two Levels of value (+, -))
Note: We will start on positive side
1. **NRZ (Nonreturn to Zero)** : 
	1. **NRL-L (level)** : Stay down when we found 1, otherwise, stay up   ![[NRZ-L.png|  500 ]]
	  2. **NRZ-I (inverted)** : Turn to opposite side if we found 1, otherwise, don't have to do anything                           ![[NRZ-I.png| 500]]
2. **RZ (Return to Zero)** : Every half step go down to 0, when found 1 go up, when found 0 go down

![[RZ.png| 500]]

3. **Biphase** 

![[Biphase.png| 500]]

1. **Manchester** :  There are 2 type of signal shape like in the picture, we draw it down and drag end of each shape to start of next shape.
2. **Diff-Manc (Different Manchester)** : whenever we found 0, we will go to the other side and then come back again to the same side (Reverse Manchester shape) [VIDEO](https://www.youtube.com/watch?v=du_boiwX1yU)

![[Biphase-zoom.png]]

#### Bipolar

1. **Alternate Mark Invision (AMI)** : Start at neutral level, on 0 we will stay on 0 but when found 1 if previous one (of 1) is up we will go down if down we will go up.

![[AMI.png| 500]]

### Concept of Modulation

**Modulation** involves altering(changing) attributes (Amplitude, Frequency, Phase) of a *regular waveform*, known as the **carrier signal** using a *distinct signal* called the **modulation signal**. This *modulation signal usually carries information for transmission*.

Carrier signal usually has a much higher frequency than the message signal does. This is because it is impractical to transmit signals with low frequencies.

![[sql-query.jpg | 500]]

![[Amplitue_Modulation.png | 400]]
### Analog to Digital

In Analog to Digital Conversion we use one form of signal modulation **Pulse-amplitude modulation** (**PAM**) where the message information is encoded in the *amplitude* of a series of signal pulses.

We have 4 steps to do the conversion

1. **Pulse Amplitude Modulation(PAM)**

![[PAM-1.png| 400]]
2. **Quantized PAM Signal** 

![[PAM.png| 400]]
3. **Quantizing Using Sign and Magnitude**

![[Quantizing-Sign-Magnitude.png|  400]]
4. **Pulse Code Modulation (PCM)** ![[PCM.png| 500]]
### Digital to Analog

#### Basic Concepts
- Bit rate : Bits transfer in second
- Baud rate: Number of Signal per second
- Carrier Signal
	- High Frequency as a basis for information
	- Sender and Receiver agree on the frequency

![[Digital-Analog.png| 400]]

Digital Data is *modulated (Shift Keying)* on the carrier using carrier characteristic
- Amplitude
- Frequency
- Phase

1. **Amplitude Shift Keying (ASK)**
2. **Frequency Shift Keying (FSK)**
3. **Phase Shift Keying (PSK)**
4. **Quadrature Amplitude Modulation (QAM) (ASK + PSK)**

### Analog to Analog

![[Analog-Analog.png| 400]]

There are 3 types of Modulation

1. **Amplitude Modulation (AM)**
2. **Frequency Modulation (FM)**
3. **Phase Modulation (PM)**