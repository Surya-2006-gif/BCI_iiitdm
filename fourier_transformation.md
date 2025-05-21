# TASK-1



# The Fourier Transformation


     A fourier transformation transforms time-domain signal to the frequency domain.But how does that do,that is what exactly we are gonna see in here



![th](https://github.com/user-attachments/assets/15407c3e-bcea-4a4d-9740-219cb738e94c)

1.Frequency:

      - This tells how fast should a sine wave should travel
      - So a fourier transformation utilises this,it splits the given signal as multiple sine waves of different frequencies. 

![th](https://github.com/user-attachments/assets/1979a2e0-114e-4dbe-8218-eb66dec1613e)


##### **But what mechanism to use exactly to split and identify the frequency componentss??**

**We use dot product**.I will provide a little intution behind it.



- when you take dot product between two vectors in space,basically you check the similarity scores between them.


![dot product](https://github.com/user-attachments/assets/2116426e-6e11-44f8-9890-d893d9f721ab)
- So consider two vectors in a 2D space, Tjhe formula for dot product is `A.B=|A||B|cos(included angle)`
- The dot product is max whe `cos(included angle)` is 1(`included angle`=0),meaning one vector is same as other giving a highest similar score.In the same way it is minimum when  `cos(included angle)` is 0(`included angle`=pi/2).

      Interpreting the sign:
       1. when they are positive,it means when you project one vector onto another (in phase)

       2.It is negative when they are out of phase,the projection of one vector lies on the backwards extension of another vector.


- So yeah the eeg data and sine wave has dimensions more than 2,but the same concept or intutuion can be applied.

- In digital systems, both sine waves and EEG signals are stored as a set of points instead of smooth, continuous lines. This is because the signals are sampled at regular time steps. To find out how much of a certain frequency is in the EEG signal, we take a sine wave of that frequency, sample it in the same way, and then multiply each point of the sine wave with the matching point from the EEG signal. After multiplying all the points, we add them up. The final sum tells us how strong that frequency is in the EEG signal — a bigger number means the frequency is more present.



- ##### **Digital systems use DTFT(Discrete Time Fourier Transform) to covert from time domain to frequency doman**

**_Principle_:**
   
    - Any signal used can be expressed as a combination of different sine waves,each with its own frequency,amplitude and phase


- DTFT is implemented using FFT(an effective algorithm to calculate  DTFT till now)


- Steps:
     
      1.we take the complex sine wave with different frequencies calculate the dot product

      2.By the above process we get a complex number(called Fourier Coefficients) where the real part tells the cosine similarity and the imaginary part tells the similarity of sine wave.

      3.For Magnitude spectrum we take the magnitude of the Fourier coefficients and plot

      4.For Phase spectrum we calculate the phase of the particular frequency from Fourier coeffcients and then plot
      
      - steps for phase spectrum:

           1. Get sampled signal (discrete time-domain values)

           2. Compute DFT or FFT to get frequency-domain representation

           3. For each complex number, calculate phase

           4. Plot: Frequency vs. Phase angle



#### Stationarity:

- A stationary wave is a wave whose statistical property(such as mean,variance,skewness,....) does not change over time

- EEG signal is a highly Non-Stationary wave


      When we apply Fourier Transformation to a Non-Stationary wave the plot of the frequency domain is less interpretable


![Non-stationarity-a-A-non-stationary-signal-containing-20-Hz-40-Hz-and-80-Hz](https://github.com/user-attachments/assets/88a4b9cb-656a-4a88-8b67-0234a2689f4b)

- So the above issue gave rise to STFT,wavelet transformation


----

# Convolution with morlet wavelet



 ![th](https://github.com/user-attachments/assets/7a07eef6-2bb8-4901-9b3c-4b19342fcba7)
-  We take a kernel (which consists of a wavelet) and slide it over the signal. At each position, we calculate the dot product between the wavelet and the overlapping segment of the signal, then place the result at the center of the wavelet's current position.

- We slide it from start to the end of the given signl which gives us the temporal informatin of that frequency component(frequency of wavelet we slided)

- Repeat the above two process for multiple frequencies you will get a time-frequency domain


NOTE:

       -When convolving a signal with a wavelet of a single frequency, the length of the output is given by N+M−1, where N is the length of the signal and M is the length of the wavelet. 
       
       -To ensure the output aligns with the original signal’s timeline, we often apply zero-padding to the signal before convolution. After convolution, the result is typically trimmed so that each output value corresponds to the center of the wavelet’s position. This allows the filtered signal to retain the same length as the original, maintaining temporal alignment.


![Screenshot 2025-05-20 105626](https://github.com/user-attachments/assets/6a81f4c0-c035-46d9-82f0-c1d004e11ca4)


#### A Property of Convolution:
![Screenshot 2025-05-20 120141](https://github.com/user-attachments/assets/b497f17d-03ff-4847-a730-b3b7e07659fc)

- Important feature of convolution,it can act as filters

      -If you use a low-pass kernel, convolution smooths the signal (removes high-frequency noise).

      - If you use a high-pass kernel, convolution emphasizes fast changes (like edges or spikes).

      - If you use a band-pass kernel (like a Morlet wavelet), convolution shows how a specific frequency band varies over time.
    

![th](https://github.com/user-attachments/assets/78d5a3a3-57bd-416d-805c-34d6a68cb6c0)

-  The result of dot product of kernel with the eeg data at one time stamp gives us a complex number

       - From the above pic we can extract phase,magnitude and the real value
       - using phase we can construct phas-time domain plot,using the magnitude we can construct amplitude-time domain lot and the real value of the signal we can constryct the band pass filtered signal


### Trade off between Time precision and Frequency precision:

- we are going to review the parameter `The number of cycles`

 ![effect of cycles parameter on gaussian bell](https://github.com/user-attachments/assets/2ad8a5a7-67d0-4f47-bb07-b677dc700a89)

 ![effect of cycles parameter on the morlet wavelet](https://github.com/user-attachments/assets/0b0acea5-5471-4465-a97c-3f3d9aee9d47)

- So you can kind of visualize, in the Morlet wavelet, the one with the high number of cycles tends to include the activities of the complete oscillatory pattern over a longer time window.Giving rise to a poor temporal resolution


![morlet wavelet  with different frequencies in frequency domain](https://github.com/user-attachments/assets/a4073d5f-50dc-4698-8399-0591a0230e96)



- On the other hand,The morlet wavelet with low number of cycles captures a long window of frequency activity giving rise to a poor frequency precision 



# Hilbert method for Analytic function:

To apply the Hilbert transform, first band-pass the EEG signal to isolate the frequency band you care about, like 8–12 Hz for alpha. Then take the FFT of that band-passed signal, zero out the negative frequencies, double the amplitude of the remaining ones (except DC and Nyquist), and do an inverse FFT. That gives you a complex analytic signal. From that, you can get the power by taking the magnitude, and the phase by taking the angle at each time point. Basically, the Hilbert method gives you both the phase and power info of that frequency band over time.


# Band-pass filtering:

- Band-pass filtering means keeping only the parts of a signal that are in a specific range of frequencies and removing everything else.

- It can be implemented using two ways,
     
       1.Use a real Morlet wavelet, apply convolution → gives a real-valued signal showing how similar the EEG is to that frequency band over time.

       2.Use FIR or IIR  band pass filtering



# Power spectral density:





  
