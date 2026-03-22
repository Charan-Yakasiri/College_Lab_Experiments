# Ideal-Sampling
## Aim:
  To demonstrate the sampling and reconstruction of a continuous-time signal using Python.
## Tools required:
+ Python IDE (Numpy)
## Program:
``` 
    import numpy as np
    import matplotlib.pyplot as plt
    from scipy.signal import resample
    Define message signal (low-frequency signal)
    fs = 1000  # High sampling rate to represent the original signal
    t = np.arange(0, 1, 1/fs)
    fm = 2  # Message signal frequency (low frequency)
    message_signal = np.sin(2 * np.pi * fm * t)  # Message signal
    Carrier Signal (Higher frequency)
    fc = 20  # Carrier frequency
    carrier_signal = np.sin(2 * np.pi * fc * t)
    Modulated Signal (Message × Carrier)
    modulated_signal = message_signal * carrier_signal
     Sampling process
    fs_sampled = 40  # Sampling frequency
    t_sampled = np.arange(0, 1, 1/fs_sampled)
    message_sampled = np.sin(2 * np.pi * fm * t_sampled)  # Sampled message signal
    Reconstruction using sinc interpolation
    message_reconstructed = resample(message_sampled, len(t))
    Plot Message Signal
    plt.figure(figsize=(10, 5))
    plt.plot(t, message_signal, label="Original Message Signal", color='b')
    plt.xlabel("Time (s)")
    plt.ylabel("Amplitude")
    plt.title("Message Signal")
    plt.legend()
    plt.grid()
    plt.show()
    Plot Ideal Sampling
    plt.figure(figsize=(10, 5))
    plt.plot(t, message_signal, label="Original Signal", linestyle="dashed", alpha=0.7)
    plt.stem(t_sampled, message_sampled, linefmt='r', markerfmt='ro', basefmt=" ", label="Sampled Signal")
    plt.xlabel("Time (s)")
    plt.ylabel("Amplitude")
    plt.title("Ideal Sampling of Message Signal")
    plt.legend()
    plt.grid()
    plt.show()
    Plot Reconstructed Signal
    plt.figure(figsize=(10, 5))
    plt.plot(t, message_signal, label="Original Signal", linestyle="dashed", alpha=0.7)
    plt.plot(t, message_reconstructed, label="Reconstructed Signal", color='g')
    plt.xlabel("Time (s)")
    plt.ylabel("Amplitude")
    plt.title("Reconstruction from Sampled Signal")
    plt.legend()
    plt.grid()
    plt.show()
```
## Output Waveform:
![image](https://github.com/user-attachments/assets/16441c20-951d-4f64-8675-896480c46d6d)

![image](https://github.com/user-attachments/assets/958fee7f-c3ca-479a-88d5-7249dd07b7ab)

![image](https://github.com/user-attachments/assets/11962e9d-41f8-46b7-b49a-9c343ee9dd41)

## Results:
The experiment demonstrated accurate signal sampling and reconstruction using sinc interpolation. The reconstructed waveform closely matched the original signal, validating the Nyquist-Shannon Sampling Theorem. Proper sampling ensures that a continuous signal can be perfectly restored from discrete data.
