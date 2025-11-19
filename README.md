# Frequency-Division-Multiplxing

# AIM

To generate multiple message signals, multiplex them using AM-FDM, and recover each channel using bandpass filtering and coherent demodulation in Scilab.

# APPARATUS REQUIRED

1. Computer with Scilab
2. Scilab script (.sci file)
3. Basic DSP knowledge (filters, convolution, FFT)

# ALGORITHM

1. Generate message signals ( m_i(t) ).
2. Multiply each with its carrier to form AM-DSB.
3. Sum all channels → FDM composite.
4. For each channel:
   a. Band-pass filter around carrier.
   b. Multiply with same carrier (coherent detection).
   c. Low-pass filter to recover baseband.
5. Plot message, FDM, recovered outputs.

# PROCEDURE 

1. Define sampling rate, time vector, message and carrier frequencies.
2. Generate sinusoidal messages and modulate them with cosine carriers.
3. Add all modulated signals to form the composite FDM signal.
4. Design FIR bandpass filter to isolate each channel.
5. Demodulate by mixing with original carrier and low-pass filtering.
6. Plot original messages, FDM signal and recovered signals.
# PROGRM
# OUTPUT
# MANUAL CALCULATION
# RESULT 

All message frequencies (415–465 Hz) were successfully multiplexed and individually recovered with minimal distortion using bandpass isolation and coherent demodulation.
---

If you want, I can give **very short viva questions**, **output verification statement**, or **neatly formatted PDF**.
