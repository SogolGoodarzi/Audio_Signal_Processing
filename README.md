# Audio_Signal_Processing
In this project, we are going to examine the echo and noise removal process with the help of different filters.

* <p align="justify"> First, record a 10-second audio that you are reading a news sentence. Then apply an echo to the recorded sound using the following equation. In this section, consider 𝛼 = 0.8 and set the value of β arbitrarily so that the sound echoes well. </p>

![image](https://github.com/SogolGoodarzi/Audio_Signal_Processing/assets/125180530/f3ac103a-4d04-4842-9b2f-902ce890e635)

<p align="justify"> To add echo to the desired sound, according to the given relationship, we first find the impulse response of the system and coeval with the input signal. Here, we have considered the delay value to be 0.2 times the audio sampling frequency, which is 11025 Hz. </p>

![image](https://github.com/SogolGoodarzi/Audio_Signal_Processing/assets/125180530/d376617b-a0f5-4128-956c-13400b93afb5)

<p align="justify"> According to the above relationship and with the appropriate commands, we form the vector h, the value of the first element of which is 1 and the 2206 element (𝛽 + 1) is 𝛼. We convolute this vector with the x vector which is the audio data vector with the conv command and the output y which is the echoed sound is obtained. This audio can be heard in the first part of the written program. </p>

* <p align="justify"> Now add a random noise with an amplitude of 0.2 times the default to the echo sound. Save the final signal passed through the echo and noise stage as "noisy_echoed_voice". </p>

<p align="justify"> To add random noise, we have used the randn command, which forms a vector with the size of the echoed sound, i.e. y, with random values ​​that have a normal distribution. In order for the range of this noise to be the optimal value of the question, first we divide all the values ​​by the maximum value of this vector and then we multiply by the value of 0.2 and finally we add the formed noise with the echoed sound. The resulting sound is stored in the "noisy_echoed_voice.wav" file and can be heard. </p>

## Question 1. Single echo filter
<p align="justify"> One of the applications of Cepstrum transform can be mentioned to eliminate the echo signal created in an audio signal. More precisely, the Cepstrum transform of an echoed signal will have a peak at the starting point of the echo (β + 1). Note that the presence of noise will cause a peak to appear before the echo peak. </p>

* <p align="justify"> As it has been said, echo can be eliminated by using Cepstrum. For this purpose, in the function that we have written (Echo_Filter function), we use the rceps command to take a cepstrum from the echoed noisy sound, then we plot its cepstrum diagram. (It should be noted that when we take the cepstrum of a signal due to its noise, usually the values ​​at the beginning and end of the peaks are very large and intense due to the noise. In order to better see the desired peaks to obtain 𝛽, it is necessary to do not consider the first and last examples of Cepstrum. </p>

![image](https://github.com/SogolGoodarzi/Audio_Signal_Processing/assets/125180530/ef809741-9e8f-4540-9cd8-f16c4f3ce07c)

<p align="justify"> Now, we have used the max command to get the peak that the starting point of the echo refers to, but please note that we have not considered the first and last 20 samples of the cepstrum so that the large peaks caused by the sound are not misdiagnosed. With the find command, you can get the quefrency where the desired peak is located, and according to the description of the project, this value is equal to 𝛽 + 1, so the value of 𝛽 is equal to one less than the value obtained in the code written for these commands. We have considered this point. In the end, we have done the opposite to eliminate the echo of the sound and with the appropriate commands explained in the next part of the question, we have obtained the sound without echo. Finally, the sound without echo is saved in "noisy_voice.wav". </p>

* <p align="justify"> According to the following relationship, we have the signal y or output and we intend to find x or input through it. The value of 𝛽 was obtained earlier. The value of the echo domain, 𝛼, was also given according to the project and was equal to 0.8. One of the input arguments of the written function must be the value of 𝛼 so that we can act according to the following relationship and find the input signal. </p>

![image](https://github.com/SogolGoodarzi/Audio_Signal_Processing/assets/125180530/d95bcff7-597a-4215-adf3-c4be84f12c13)

![image](https://github.com/SogolGoodarzi/Audio_Signal_Processing/assets/125180530/ceeb7b20-935f-41fb-a140-72d9d5c427ea)

![image](https://github.com/SogolGoodarzi/Audio_Signal_Processing/assets/125180530/bcbca41b-110c-4c15-9a36-b808e675792f)

<p align="justify"> Now, in order to find $x[n]$, we use the filter function, in such a way that the input of the input signal of this function is $y[n]$ and its first two arguments are the coefficients of the inverse transformation function $H(z)$ that we obtained above. </p>

![image](https://github.com/SogolGoodarzi/Audio_Signal_Processing/assets/125180530/f7771ae1-56bc-4063-8195-fab9996be9e0)

According to the appropriate commands that can be seen in the written function, the input signal can be obtained, which is the same signal without echo.

If we run this function for the desired sound, the output beta value of the function is equal to 2205, which is the same as the beta we considered at the beginning:

![image](https://github.com/SogolGoodarzi/Audio_Signal_Processing/assets/125180530/b2515105-4cca-4053-be63-7342af6c430b)

* We have plotted the echoed noisy signal and the output signal of the function (removed sound echo) in two domains of time and frequency as below.

![image](https://github.com/SogolGoodarzi/Audio_Signal_Processing/assets/125180530/57371037-db8d-464b-9acc-f2b8057bd82e)

![image](https://github.com/SogolGoodarzi/Audio_Signal_Processing/assets/125180530/a76c4253-5ecf-48de-915c-9b513ece9de4)

<p align="justify"> The first difference that can be seen in the form of the two signals in the time domain is that in the signal that has an echo, because the delay of the signal is 0.2 seconds, it is added to the signal itself and makes the echoed signal, we see that it is almost a repetition is observed in the signal (this means that every point of the signal we consider, we have the same one 0.2 seconds before or after it, due to the delay we have created for the echo to occur in the signal). In the signal where the echo is removed, such descriptions are not observed, and we also see that the amplitude of the signal without echo is greater than the signal with echo. (I think the reason for this higher range is because of the filter we used to remove the echo). </p>

<p align="justify"> For the analysis in the frequency domain, we also see that in two values ​​in the echo signal, strong peaks are observed, which is due to the echo that we have placed for it. In the Fourier transform of the signal without echo, we can see that these peaks are weakened and the amplitude of other parts of the signal is increased compared to the case with echo. The justification for this is similar to the reason we mentioned for the time domain, that is, due to the filter we used to remove the echo, the noise has been amplified, and for this reason, in the frequency domain, similarly to the time domain, we see an increase in the signal amplitude for the noise. </p>

## Question 2. Noise removal using FIR filters
* <p align="justify"> The frequency of the audio signal that is caused by speaking is between 300 and 3400Hz. The limit of the stop band for this sound is around 3800Hz, and the attenuation of the stop band is 80dB at most. Also, the fluctuation of the bandwidth for these signals is less than 3dB due to the loss of quality after removing the noise. </p>

* <p align="justify"> According to the following table, with the help of fdatool and setting different parameters, try to remove noisy _voice and restore the original sound. Finally, compare with your original noise and echo-free audio. </p>

![image](https://github.com/SogolGoodarzi/Audio_Signal_Processing/assets/125180530/93e03525-b0b7-42c9-914f-4ceb651f3634)

<p align="justify"> We have used the fdatool to design a suitable filter to reduce audio noise, so that in the Designed Method section, we use the window mode to design the window. We have used the kaiser window among the windows listed in the project table. The reason for using this window is that the stopband attenuation is less than 80dB. Be careful that the filter we design is low pass. In the filter designed with this window, we can see that there is a good connection between the main lobe and the side lobes, which makes the filtering action a little better than the other windows. Next, in order to eliminate as much of the noise as possible, we use guesswork and testing, and we find the best classification and parameter settings by testing and listening to the sound. In the figure below, the appropriate values ​​of the parameters that we have used to design the filter, which are based on the data determined in the previous part, are given, and the shape of the designed filter is also known. By exporting the filter from the fdatool environment to the workspace environment, we can use the conv command to convolve the noisy voice (noisy_voice) with the designed filter and have the improved sound. If we compare the filtered sound with the noisy sound, it can be seen that we have been able to remove a good part of the noise, but it has not been completely removed. In fact, here the goal is to reach the best possible state, where by properly determining the filter parameters, we were able to reduce the desired sound noise as much as possible. (The filtered sound that we have reduced the noise of is stored in the "filtered_voice.wav" file. </p>

![image](https://github.com/SogolGoodarzi/Audio_Signal_Processing/assets/125180530/b4dbf938-afa6-4384-9b33-6bab294a7c1e)

![image](https://github.com/SogolGoodarzi/Audio_Signal_Processing/assets/125180530/3d69810d-cf1f-4bd7-8685-d284d8f4ff75)

<p align="justify"> As can be seen from the figure, we set fs to 11025, which is the frequency of our sound sampling. We have set the value of fpass and fstop in the upper and lower range of the audio frequency, i.e. 300 and 3400Hz respectively, and Apass, which is related to the fluctuation of the pass band, is 3dB, and Astop, which is related to the attenuation of the stop band, is 60dB, which is less than the upper limit of this parameter, which means less We have set it from 80dB. </p>

* We have plotted the signals in two time and frequency domain to compare them with each other:

![image](https://github.com/SogolGoodarzi/Audio_Signal_Processing/assets/125180530/cf963c71-13a4-4c07-883b-38a57a2e9288)

![image](https://github.com/SogolGoodarzi/Audio_Signal_Processing/assets/125180530/1fd73399-8bb1-492a-9eca-ad97c1a9b423)

<p align="justify"> As it is clear from the graph of the signals in the time domain, in the noisy signal, we can see that the range of the different points of the signal is larger compared to the range of the filtered signal points, which is due to the presence of noise so we expect the range of the signal to be reduced. Now, if we pay attention to the signals plotted in the frequency domain, we can see that the shape of the Fourier transform of the filtered signal is almost the shape of the filter through which we passed the sound. In fact, because the designed filter was low-pass, we can see that in the Fourier transform of the filtered signal, the larger amplitudes of the signal are in the range and near the zero or origin frequency, which is due to the low-pass design of the filter, and at higher frequencies we see the values We are insignificant and zero in the Fourier transform of the signal. In addition to the above justifications, it can be said that the amplitude of the peaks of the Fourier transform of the filtered signal has been reduced to a very small amount from the amplitude of the Fourier transform of the noisy signal, which can be justified due to the reduction of the noise effect by the designed filter. </p>
