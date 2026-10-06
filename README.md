# PSK
# Aim
Write a simple Python program for the modulation and demodulation of PSK and QPSK.
# Tools required
Google colab
# Program
## PSK
```
import numpy as np
import matplotlib.pyplot as plt

fs = 1000
fc = 50

t = np.arange(0, 1, 1/fs)

bits = np.random.randint(0, 2, 10)
print("Original bits:", bits)

bit_dur = len(t) // len(bits)
msg = np.repeat(bits, bit_dur)

carrier = np.sin(2 * 3.14 * fc * t)

# PSK Modulation
psk = np.sin(2 * 3.14 * fc * t + 3.14 * msg)

# Demodulation
demod = psk * carrier

decoded = []

for i in range(len(bits)):
    start = i * bit_dur
    end = (i + 1) * bit_dur

    value = np.mean(demod[start:end])

    decoded.append(0 if value > 0 else 1)

print("Decoded:", decoded)

# Plot
plt.figure(figsize=(12, 10))

plt.subplot(4,1,1)
plt.plot(t, msg)
plt.title("Message Signal")
plt.grid()

plt.subplot(4,1,2)
plt.plot(t, carrier)
plt.title("Carrier Signal")
plt.grid()

plt.subplot(4,1,3)
plt.plot(t, psk)
plt.title("PSK Modulated Signal")
plt.grid()

plt.subplot(4,1,4)
plt.step(np.arange(len(decoded)), decoded, where='mid')
plt.title("Decoded Bits")
plt.grid()

plt.tight_layout()
plt.show()
```
## QPSK
```
#QPSK 


import numpy as np
import matplotlib.pyplot as plt

# Input bit pairs
x = ['10', '11', '11', '10']

# Time
t = np.arange(-np.pi, np.pi, 0.1)

# QPSK signals for 4 phases
signals = {
    '00': np.sin(t + np.pi/4),
    '01': np.sin(t + 3*np.pi/4),
    '10': np.sin(t + 5*np.pi/4),
    '11': np.sin(t + 7*np.pi/4)
}

# Modulation
mod = []
inp = []

for bits in x:
    mod.extend(signals[bits])
    inp.extend([int(bits[0]), int(bits[1])])

# Demodulation
demod = []

for i in range(len(x)):
    value = mod[i * len(t) + 2]

    if value <= -0.77:
        demod.extend([0, 0])
    elif value <= -0.63:
        demod.extend([0, 1])
    elif value >= 0.77:
        demod.extend([1, 0])
    else:
        demod.extend([1, 1])

# Plot
plt.figure(figsize=(10, 6))

# Input
plt.subplot(3, 1, 1)
plt.step(range(len(inp)), inp, where='post')
plt.title('Input Binary Data')
plt.ylim(-0.5, 1.5)
plt.grid()

# Modulated signal
plt.subplot(3, 1, 2)
plt.plot(mod)
plt.title('QPSK Modulated Signal')
plt.grid()

# Demodulated
plt.subplot(3, 1, 3)
plt.step(range(len(demod)), demod, where='post')
plt.title('Demodulated Signal')
plt.ylim(-0.5, 1.5)
plt.grid()

plt.tight_layout()
plt.show()
```
# Output Waveform
### PSK
<img width="1282" height="788" alt="image" src="https://github.com/user-attachments/assets/8af246d8-89d2-46cd-8b51-2f3d9ab49e95" />
### QPSK
<img width="1035" height="586" alt="image" src="https://github.com/user-attachments/assets/3c3e6cbb-b2ed-4147-8243-034e47dc46b7" />

# Results
Therefore python program for the modulation and demodulation of PSK and QPSK is executed successfully.
