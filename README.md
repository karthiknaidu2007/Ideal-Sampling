# Ideal, Natural, & Flat-top -Sampling
# Aim
Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.
# Tools required

# Program
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, filtfilt

fs = 500
t = np.arange(0,1,1/fs)
m = np.sin(2*np.pi*5*t)

step = int(fs/50)
idx = np.arange(0,len(t),step)
w = int(fs/(2*50))

# Sampling pulse train
pulse = np.zeros(len(t))
pulse[idx] = 1

# Ideal sampling
ideal = np.zeros(len(t))
ideal[idx] = m[idx]

# Natural sampling
natural = np.zeros(len(t))
for i in idx:
    natural[i:i+w] = m[i:i+w]

# Flat-top sampling
flat = np.zeros(len(t))
for i in idx:
    flat[i:i+w] = m[i]

# -------- RECONSTRUCTION --------
def lowpass(signal, cutoff, fs, order=5):
    nyq = fs/2
    b, a = butter(order, cutoff/nyq, btype='low')
    return filtfilt(b, a, signal)

cutoff = 10   # > message frequency (5 Hz)

rec_ideal = lowpass(ideal, cutoff, fs)


# -------- PLOTS --------
plt.figure(figsize=(14,16))

plt.subplot(6,1,1)
plt.plot(t,m)
plt.title("Message Signal")

plt.subplot(6,1,2)
plt.stem(t,pulse,basefmt=" ")
plt.title("Sampling Signal")

plt.subplot(6,1,3)
plt.stem(t,ideal,basefmt=" ")
plt.title("Ideal Sampling")

plt.subplot(6,1,4)
plt.plot(t,natural)
plt.title("Natural Sampling")

plt.subplot(6,1,5)
plt.plot(t,flat)
plt.title("Flat Top Sampling")

plt.subplot(6,1,6)
plt.plot(rec_flat)
plt.title("Reconstructed signal")

plt.tight_layout()
plt.show()
```
# Output Waveform

# Results
Thus, the construction and reconstruction of Ideal, Natural, and Flat-top sampling were successfully implemented using Python, and the corresponding waveforms were obtained.
