# Hearing AID System

This MATLAB project simulates a basic Hearing Aid system. It processes an audio signal by adding noise, filtering it, and performing amplitude shaping to enhance the signal. The script demonstrates the steps of loading an audio file, adding noise, filtering the noise, frequency shaping, and performing amplitude adjustments. 

## Features

1. **Load and Play Input Sound:**
   - The script starts by loading an audio file (`handel.mat`) and plays the original sound.

2. **Add White Gaussian Noise:**
   - White Gaussian noise is added to the signal with a specified Signal-to-Noise Ratio (SNR).

3. **Low-pass Filtering:**
   - A low-pass filter is designed and applied to the noisy signal to reduce the noise.

4. **Band-pass Filtering:**
   - A band-pass filter is applied to shape the frequency content of the denoised signal.

5. **Amplitude Shaping:**
   - The amplitude of the frequency-shaped signal is adjusted to simulate a hearing aid's compression function.

6. **Spectrogram Visualization:**
   - The script generates spectrograms for both the noisy and the processed signals for visual analysis.

## Prerequisites

- **MATLAB**: The script is designed to be run in MATLAB.
- **handel.mat**: The script uses `handel.mat`, a built-in MATLAB file, for demonstration purposes.

## Usage

1. **Clone the repository**:
    ```
    git clone https://github.com/yourusername/Hearing-AID-System.git
    cd Hearing-AID-System
    ```

2. **Run the script**:
   - Open the `HearingAIDSystem.m` file in MATLAB and run it.

3. **Process Flow**:
   - The script will load the input audio, play it, and then proceed to add noise, filter it, and perform the necessary adjustments. Each step will display plots and play the corresponding audio.

## Code Breakdown

- **Loading and Playing the Sound**:
  ```matlab
  load handel.mat;
  sound(y);
  ```

- **Adding Noise**:
  ```matlab
  y = awgn(y, 40);
  ```

- **Low-pass Filtering**:
  ```matlab
  hlpf = fdesign.lowpass('Fp,Fst,Ap,Ast', 3.0e3, 3.5e3, 0.5, 50, fs);
  D = design(hlpf);
  x = filter(D, y);
  ```

- **Band-pass Filtering**:
  ```matlab
  f1 = fdesign.bandpass(['Fst1,Fp1,Fp2,Fst2,Ast1,Ap,Ast2'], 2000, 3000, 4000, 5000, 60, 2, 60, 2*fs);
  hd = design(f1, 'equiripple');
  y = filter(hd, x);
  ```

- **Amplitude Shaping**:
  ```matlab
  out1 = fft(y);
  outfinal = real(ifft(out1)) * 10000;
  ```

- **Spectrogram Visualization**:
  ```matlab
  subplot(2,2,1);
  specgram(noi);
  subplot(2,1,2)
  specgram(outfinal);
  ```

## Note

- The script contains a line that attempts to load a non-existent file (`load handel.mat`), which may cause an error. This line is likely a placeholder or a mistake. Ensure the correct file path or remove this line if unnecessary.


## Contact

For any queries, feel free to contact [your email or GitHub profile].

---