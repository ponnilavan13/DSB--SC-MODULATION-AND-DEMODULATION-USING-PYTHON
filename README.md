# DSB--SC-MODULATION-AND-DEMODULATION-USING-PYTHON

__AIM__:

To generate a Double Sideband Suppressed Carrier (DSB-SC) signal in Python (Google Colab), transmit it (optionally add noise), and recover the message using coherent (synchronous) demodulation with a low-pass filter. Observe time and frequency domain waveforms and measure demodulation performance

__APPARATUS REQUIRED__:

Google Colab (or any Python environment)

Python libraries: numpy, matplotlib, scipy (scipy.signal)

__Theory__:

DSB-SC signal: s(t) = m(t) · cos(2πf_c t)
Coherent demodulation: multiply received s(t) by a synchronized carrier cos(2πf_c t) then low-pass filter (LPF) to remove double-frequency components:

r(t) = s(t)·cos(2πf_c t) = m(t)·cos²(2πf_c t) = 0.5 m(t) + 0.5 m(t)·cos(4πf_c t)
LPF extracts 0.5·m(t) → scale by 2 to recover m(t).

__Procedure__:

1) Import libraries and set parameters
2) Define message and carrier signals
3) Generate DSB-SC signal (modulation)
4) View spectra (FFT) of message and DSB-SC
5) (Optional) Add noise
6) Coherent demodulation (multiply by synchronized carrier)
7) Low-pass filter to recover message

__Program__:
   import numpy as np
   import matplotlib.pyplot as plt
   fs = 10000 
   t = np.arange(0, 0.01, 1/fs)

   Am = 1       
   Ac = 5      
   fm = 100     
   fc = 1000    
   mod_index = 0.7  

   message = Am * np.sin(2 * np.pi * fm * t)
   carrier = Ac * np.sin(2 * np.pi * fc * t)
   am_signal = Ac * (1 + mod_index * np.sin(2 * np.pi * fm * t)) * np.sin(2 * np.pi * fc * t)
   rectified = np.abs(am_signal)
   N = 50
   demodulated = np.convolve(rectified, np.ones(N)/N, mode='same')
   plt.figure(figsize=(12,10))

   plt.subplot(4,1,1)
   plt.plot(t, message)
   plt.title("Message Signal (Modulating Signal)")
   plt.xlabel("Time")
   plt.ylabel("Amplitude")

   plt.subplot(4,1,2)
   plt.plot(t, carrier)
   plt.title("Carrier Signal")
   plt.xlabel("Time")
   plt.ylabel("Amplitude")

   plt.subplot(4,1,3)
   plt.plot(t, am_signal, color='red')
   plt.title("AM Modulated Signal")
   plt.xlabel("Time")
   plt.ylabel("Amplitude")

   plt.subplot(4,1,4)
   plt.plot(t, demodulated, color='green')
   plt.title("Demodulated Signal (Recovered Message)")
   plt.xlabel("Time")
   plt.ylabel("Amplitude")

   plt.tight_layout()
   plt.show()


 __Tabulation__:
![WhatsApp Image 2025-11-26 at 22 47 27_d28e6bde](https://github.com/user-attachments/assets/e4f77520-da3c-4389-8835-024695a27355)



__Output__:

   <img width="1189" height="990" alt="image" src="https://github.com/user-attachments/assets/1b7cbd4d-7def-463f-8f02-b9b551a65169" />

 __Result__:

Thus the DSB-SC is proved and verified using python successfully.
