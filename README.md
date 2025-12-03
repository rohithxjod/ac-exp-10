# Frequency Division Multiplexing


## AIM
To implement Frequency Division Multiplexing (FDM) for six different message signals using Scilab, generate the multiplexed signal, and perform demultiplexing to recover all the original message signals. The experiment also includes plotting the message signals, multiplexed signal, and demultiplexed signals.

## APPARATUS REQUIRED

1. Computer System
2. Scilab Software

## ALGORITHM

1. Set sampling frequency, time duration, and time vector.
2. Generate six message signals with different frequencies.
3. Assign six different carrier frequencies.
4. Perform DSB-SC modulation by multiplying each message with its carrier.
5. Add all modulated signals to form the multiplexed FDM signal.
6. For each channel, multiply the multiplexed signal with the same carrier (demodulation).
7. Apply a low-pass filter to extract the recovered message.
8. Plot message signals, multiplexed signal, and recovered s  ignals.

## THEORY

Frequency Division Multiplexing (FDM) is a technique in which multiple message signals are transmitted simultaneously over a single communication channel by assigning each signal a different carrier frequency. Each message modulates its own carrier, and all modulated signals are added to form the multiplexed signal. Since the carrier frequencies are well separated, the signals do not overlap in the frequency domain.

At the receiver, each signal is recovered by multiplying the multiplexed signal with the corresponding carrier (coherent demodulation) and passing it through a low-pass filter to extract the original baseband message. FDM is widely used in radio broadcasting, telephone systems, and cable TV.

## PROGRAM
```
t = linspace(0, 1, 1000);
fs = 1000; 

freqs = [4, 8, 12, 16, 20, 24];

signals = zeros(6, length(t));
for i = 1:6
    signals(i, :) = sin(2 * %pi * freqs(i) * t);
end

fdm_signal = zeros(1, length(t));
for i = 1:6
    fdm_signal = fdm_signal + signals(i, :);
end

order = 50;
cutoff_freq = 8 / (fs/2); 
h = ffilt("lp", order, cutoff_freq);

demux_signals = zeros(6, length(t));
for i = 1:6
    mixed = fdm_signal .* sin(2 * %pi * freqs(i) * t);
    demux_signals(i, :) = filter(h, 1, mixed);
end

scf(1);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, signals(i, :));
    title('Original Signal f=' + string(freqs(i)));
end

scf(2);
clf;
plot(t, fdm_signal);
title('FDM Signal');

scf(3);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, demux_signals(i, :));
    title('Demultiplexed Signal f=' + string(freqs(i)));
end
```

## OUTPUT WAVEFORM
<img width="757" height="716" alt="image" src="https://github.com/user-attachments/assets/6074d4fb-4de3-4300-b636-76f71ca69316" />

<img width="763" height="737" alt="image" src="https://github.com/user-attachments/assets/2fa0348f-d722-4ef1-84dd-cea0c1cc97de" />

<img width="763" height="711" alt="image" src="https://github.com/user-attachments/assets/6dd553b7-7cf7-4408-9bc5-e827bf34b583" />




## CALCULATION

![WhatsApp Image 2025-12-03 at 14 53 37_3324d592](https://github.com/user-attachments/assets/1cc329e1-8d04-49ac-9920-9b8f9ea3859b)
![WhatsApp Image 2025-12-03 at 14 53 37_3324d592 - Copy](https://github.com/user-attachments/assets/44a473c4-5ffb-4e4a-ab63-457f7291c904)




## RESULT
Six different message signals were generated and modulated using FDM. All modulated signals were added to form a multiplexed FDM signal. Each message was successfully recovered using coherent demodulation followed by low-pass filtering. The plots confirmed accurate multiplexing and demultiplexing.
