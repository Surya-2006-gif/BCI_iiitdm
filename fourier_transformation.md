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
