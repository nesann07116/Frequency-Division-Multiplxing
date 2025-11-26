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
```
clc; clear; close;
fs=80000; N=floor(0.05*fs); t=(0:N-1)/fs;
fm=[474 484 494 504 514 524];
fc=[4740 4840 4940 5040 5140 5240];
Am=[6.1 6.2 6.3 6.4 6.5 6.6];
Ac=[12.2 12.4 12.6 12.8 13 13.2];
num=length(fm);
for i=1:num
    m(i,:)=Am(i)*sin(2*%pi*fm(i)*t);
end
fdm=zeros(1,N);
for i=1:num
    fdm = fdm + Ac(i)*cos(2*%pi*fc(i)*t).*m(i,:);
end
function h=FIR(fc1,fc2,fs,M,mode)
    n=-M:M; L=length(n);
    x1=2*fc1*n/fs; x2=2*fc2*n/fs;
    s1=ones(1,L); s2=ones(1,L);
    for k=1:L
        if x1(k)<>0 then s1(k)=sin(%pi*x1(k))/(%pi*x1(k)); end
        if x2(k)<>0 then s2(k)=sin(%pi*x2(k))/(%pi*x2(k)); end
    end
    lp1=(2*fc1/fs)*s1; lp2=(2*fc2/fs)*s2;
    w=(0.54-0.46*cos(2*%pi*(n+M)/(2*M)));
    if mode==1 then h=lp1.*w;
    else h=(lp2-lp1).*w; end
    h=h/sum(h);
endfunction
M=300;
for i=1:num
    bp=FIR(fc(i)-600,fc(i)+600,fs,M,2);
    iso=conv(fdm,bp,"same");
    mix=iso.*cos(2*%pi*fc(i)*t);
    lp=FIR(800,0,fs,M,1);
    demod(i,:)= (2/Ac(i))*conv(mix,lp,"same");
end
scf(1); clf;
for i=1:num subplot(num,1,i); plot(t,m(i,:)); end
scf(2); clf; plot(t,fdm);
scf(3); clf;
for i=1:num subplot(num,1,i); plot(t,demod(i,:)); end

```
# OUTPUT

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/ba2da03e-330d-4c58-ae43-e9e81cfb39c5" />

<img width="1917" height="1073" alt="image" src="https://github.com/user-attachments/assets/37599d05-5940-4922-b5b9-c3e8bbb889ae" />

<img width="1915" height="1078" alt="image" src="https://github.com/user-attachments/assets/2bf3e967-b7e8-41b7-99dd-b2537ce896dd" />



# MANUAL CALCULATION

![WhatsApp Image 2025-11-26 at 22 01 10_e32fb658](https://github.com/user-attachments/assets/8606d8e9-9a60-4b97-ba10-fe4fe6c27f94)

![WhatsApp Image 2025-11-26 at 22 01 30_159406ad](https://github.com/user-attachments/assets/f29aab32-0212-4191-91c5-f495be3ded84)



# RESULT 

All message frequencies (415–465 Hz) were successfully multiplexed and individually recovered with minimal distortion using bandpass isolation and coherent demodulation.
