# harmonic-analysis

Harmonic analysis in Rust. FFT, wavelets, and spectral methods.

A library for decomposing signals into frequency components — Fourier series, DFT/FFT, convolution, windowing, Laplace/Z transforms, Haar wavelets, spectral estimation, and periodicity detection.

## Features

- **Fourier series** decomposition with Parseval's theorem verification
- **DFT/FFT** (radix-2 Cooley-Tukey) with roundtrip guarantees
- **Convolution** (naive and FFT-based)
- **Windowing** (Hamming, Hann, Blackman, Gaussian)
- **Laplace transform** (numerical forward + Gaver-Stehfest inverse)
- **Z-transform** (DTFT, frequency response, group delay)
- **Haar wavelets** (DWT, multi-resolution analysis, denoising)
- **Spectral estimation** (periodogram, Welch's method)
- **Signal analysis** (autocorrelation, period detection)

76 unit tests cover all modules.

## Install

```toml
[dependencies]
harmonic-analysis = "0.1"
```

## Quick Start

```rust
use harmonic_analysis::*;
use num_complex::Complex64;

// FFT
let signal: Vec<Complex64> = (0..64).map(|j| {
    Complex64::new((2.0 * std::f64::consts::PI * 4.0 * j as f64 / 64.0).cos(), 0.0)
}).collect();
let spectrum = Dft::fft(&signal);

// Welch's PSD
let signal: Vec<f64> = (0..1024).map(|i| {
    (2.0 * std::f64::consts::PI * 50.0 * i as f64 / 44100.0).sin()
}).collect();
let (freqs, psd) = SpectralEstimation::welch(&signal, 44100.0, 256, 128);

// Haar wavelet denoising
let denoised = Wavelet::denoise(&vec![4.0, 6.0, 8.0, 10.0, 2.0, 4.0, 6.0, 8.0], 1.0);
```

## License

MIT OR Apache-2.0
