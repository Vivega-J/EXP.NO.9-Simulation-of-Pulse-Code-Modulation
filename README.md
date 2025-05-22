# EXP.NO.9-Simulation-of-Pulse-Code-Modulation
9.Simulation of PCM

# AIM

To study and implement 2-channel Time Division Multiplexing (TDM) and Sampling of analog signals, and perform Pulse Code Modulation (PCM) and Demodulation


# SOFTWARE REQUIRED

1. Python
2. Colab
   libraries: numpy, matplotlib

# ALGORITHMS

1. Start the simulation in Google Colab.

2. Import necessary libraries such as NumPy for numerical operations and Matplotlib for plotting.

3. Generate an analog signal, typically a sine wave using NumPy.

      Example: 1 kHz sine wave with sampling rate of 8 kHz.

4. Sample the analog signal at a fixed sampling frequency.

      Use np.arange() or np.linspace() to define the time vector.

5. Quantize the sampled signal:

       Define the number of quantization levels (e.g., 8-bit or 256 levels).

       Perform uniform quantization by mapping amplitude values to nearest level.

6. Encode the quantized signal into binary (PCM).

        Convert each quantized value to its binary equivalent.

7. Plot waveforms for:

       Original analog signal

       Sampled signal

       Quantized signal

# PROGRAM

```pythonimport matplotlib.pyplot as plt
import numpy as np

# Parameters
sampling_rate = 5000
duration = 0.1
quantization_levels = 16

# Time base
t = np.linspace(0, duration, int(sampling_rate * duration), endpoint=False)

# Two message signals
frequency1 = 50
frequency2 = 120
message_signal1 = np.sin(2 * np.pi * frequency1 * t)
message_signal2 = np.sin(2 * np.pi * frequency2 * t)

# Quantization function
def quantize(signal, levels):
    step = (max(signal) - min(signal)) / levels
    quantized = np.round(signal / step) * step
    pcm = ((quantized - min(quantized)) / step).astype(int)
    return quantized, pcm

# Quantize both signals
quantized_signal1, pcm_signal1 = quantize(message_signal1, quantization_levels)
quantized_signal2, pcm_signal2 = quantize(message_signal2, quantization_levels)

# Multiplexing the PCM signals by interleaving
multiplexed_pcm = np.empty((pcm_signal1.size + pcm_signal2.size,), dtype=int)
multiplexed_pcm[0::2] = pcm_signal1
multiplexed_pcm[1::2] = pcm_signal2

# Time base for multiplexed signal
t_mux = np.linspace(0, duration, multiplexed_pcm.size, endpoint=False)

# Clock signal for reference
clock_signal = np.sign(np.sin(2 * np.pi * 200 * t))

# Plotting
plt.figure(figsize=(14, 12))

plt.subplot(8, 1, 1)
plt.plot(t, message_signal1, label="Message Signal 1 (50Hz)", color='blue')
plt.title("Original Message Signal 1")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 2)
plt.plot(t, clock_signal, label="Clock Signal", color='green')
plt.title("Clock Signal")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 3)
plt.step(t, quantized_signal1, label="Quantized Signal 1", color='red')
plt.title("Quantized Signal 1")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 4)
plt.plot(t, message_signal2, label="Message Signal 2 (120Hz)", color='orange', alpha=0.7)
plt.title("Original Message Signal 2")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 5)
plt.plot(t, clock_signal, label="Clock Signal", color='green')
plt.title("Clock Signal")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 6)
plt.step(t, quantized_signal2, label="Quantized Signal 2", color='purple', alpha=0.7)
plt.title("Quantized Signal 2")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 7)
plt.step(t, quantized_signal1, label="Quantized Signal 1", color='red')
plt.step(t, quantized_signal2, label="Quantized Signal 2", color='purple', alpha=0.7)
plt.title("Overlay of Quantized Signals")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 8)
plt.step(t_mux, multiplexed_pcm, label="Multiplexed PCM Signal", color='black')
plt.title("Multiplexed PCM Signal (Interleaved)")
plt.xlabel("Time [s]")
plt.ylabel("PCM Value")
plt.grid(True)
plt.legend()

plt.tight_layout()
plt.show()
)
```


# OUTPUT

![image](https://github.com/user-attachments/assets/f42b952f-cf82-425e-8097-b53a7b4885e5)

 
# RESULT / CONCLUSIONS

The Pulse Code Modulation (PCM) technique was successfully implemented and simulated in Google Colab using Python. A sinusoidal analog signal was sampled, quantized, and encoded into binary form. The simulation demonstrated the process of converting an analog signal into a digital stream using PCM. The reconstructed signal closely resembled the original waveform, validating the accuracy of the simulation. This highlights the efficiency of PCM in representing analog data in digital communication systems.
