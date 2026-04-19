# Companion to *Spectral Audio Signal Processing* by Julius O. Smith III

An interactive, animated companion to Julius O. Smith III's third online book,
[*Spectral Audio Signal Processing*](https://ccrma.stanford.edu/~jos/sasp/).
This companion sits *above* the plain STFT layer and *below* neural spectrum
modelling: it covers the parametric methods that turn a spectrogram into a list
of sinusoids, envelopes, pitch estimates, and residuals.

**[&#10140; View the Live Guide](https://brendanjameslynskey.github.io/Companion_JOS_Spectral_Audio_Signal_Processing/)**

---

## What's Inside

Thirteen chapters walk through the history, mathematics, and audio applications
of spectrum-based parametric analysis, each with a live interactive demo and a
hand-written radix-2 FFT doing the numbers in your browser.

### 1 &middot; Prologue &mdash; Why Spectral Audio
Where SASP sits among Smith's four online books. What this companion adds
beyond the STFT companion. Hero canvas with drifting sinusoidal tracks on the
time&ndash;frequency plane.

### 2 &middot; STFT Refresher &mdash; What Peaks Look Like
Windowing, zero-padding, and mainlobe/sidelobe tradeoffs with a parametric
eye. Interactive window-library comparison with live readouts of mainlobe
6 dB width, peak sidelobe level, and scalloping loss.

### 3 &middot; Quadratic Peak Interpolation
Parabolic dB-axis formula $\delta = \tfrac{1}{2}(a-c)/(a-2b+c)$ for sub-bin
peak estimation. Abe&ndash;Smith bias derivation. Interactive: move a tone
between bins and watch the raw arg-max estimate jump while the parabolic
estimate tracks continuously.

### 4 &middot; Sinusoidal Modelling &mdash; McAulay &amp; Quatieri
The 1986 speech-coder paper that started a field. Peak picking, track linking
with frequency-threshold match, cubic-phase oscillator resynthesis. Flagship
interactive: MQ track visualiser on voice, piano, chord, and vibrato signals
with birth/death threshold toggle and resynth A/B audio.

### 5 &middot; Spectrum Modelling with Residuals &mdash; SMS
Serra &amp; Smith 1990: sinusoids plus stochastic residual. Interactive:
pick a signal, pick how many sinusoids to keep, listen to the original,
deterministic, and residual parts separately.

### 6 &middot; Spectral Envelope Estimation
Cepstral liftering, R&ouml;bel&ndash;Rodet true envelope, and LPC. Interactive
LPC-order slider on a synthetic vowel with formant peak extraction; LPC vs
cepstral envelope overlay.

### 7 &middot; Pitch Estimation
Autocorrelation, cepstrum, and YIN (de Cheveign&eacute; &amp; Kawahara 2002).
Interactive YIN monitor with SNR slider; shows both d(&tau;) and the
cumulative-normalised d'(&tau;) with threshold-crossing detection.

### 8 &middot; Time&ndash;Frequency Reassignment
Kodera 1976, Auger&ndash;Flandrin 1995. Three-STFT reassignment formula
using window, time-weighted window, and window derivative. Interactive
reassigned spectrogram on chirp, bell, and impulse signals.

### 9 &middot; The Chirp-Z Transform
Rader 1968, Bluestein 1970. Evaluating $H(z)$ on an arbitrary spiral in the
z-plane. Interactive: pick a frequency centre, span, and radius; see the
z-plane contour and the zoomed-resolution CZT overlaid on the full DFT.

### 10 &middot; Linear Prediction &mdash; Levinson and the Lossless Tube
Normal equations, Levinson&ndash;Durbin recursion, reflection coefficients
and their acoustic-tube meaning. Interactive: reflection-coefficient bar
chart with stability indicator, prediction-error power vs order on a vowel.

### 11 &middot; Phase-Vocoder Variants
Flanagan &amp; Golden 1966, Laroche&ndash;Dolson phase-locking 1999,
Griffin&ndash;Lim magnitude-only, and the sinusoidal-model phase vocoder.
Cross-link to the STFT companion for the phase-update mechanics.

### 12 &middot; Applications
Additive resynthesis with track editing, timbre-preserving pitch-shifting,
sinusoidal-model denoising, adaptive spectral whitening, differentiable
spectral modelling (DDSP).

### 13 &middot; Legacy and Continuing Impact
SPEAR, SMSTools, Loris, World, SuperVP; MPEG-4 HILN; neural spectrogram
vocoders (WaveNet, HiFi-GAN, BigVGAN); differentiable spectral modelling.
Full bibliography and cross-links.

---

## Technical Details

* **Zero dependencies.** No npm, no bundler, no external libraries. All
  rendering uses the HTML Canvas API. Audio uses the Web Audio API. Math
  typesetting uses KaTeX via jsdelivr &mdash; the only third-party asset.
* **All maths computed in real time.** Every STFT, window-library FFT,
  peak-interpolation fit, MQ tracking, SMS decomposition, LPC analysis,
  YIN period search, reassigned-spectrogram computation, chirp-z transform,
  and Levinson&ndash;Durbin recursion is calculated live in the browser
  with a hand-written radix-2 FFT.
* **Audio playback.** Every signal can be listened to via the Web Audio API
  &mdash; synthesised on demand, not pre-recorded.
* **Responsive.** Canvases scale with DPR for sharp rendering on Retina/HiDPI
  displays.
* **Single file.** Everything lives in `index.html`.

### What's computed where

| Visualisation | Algorithm | Notes |
|---|---|---|
| Hero canvas | Parametric sinusoidal tracks with per-track vibrato, drift, birth/death, trail accumulation | Layered-canvas trails |
| Window library | FFT of zero-padded window, log-magnitude | Mainlobe, sidelobe, scalloping readouts |
| Peak interpolation | Three-point parabolic fit in dB | True vs raw vs parabolic comparison |
| MQ tracker | Hann-STFT peak-picking + greedy frequency-threshold linking + cubic-phase oscillator resynthesis | Voice / piano / chord / vibrato |
| SMS | Peak-kept spectra IFFT / OLA for deterministic part; subtraction for residual | Original / det / res audio A/B/C |
| LPC envelope | Autocorrelation + Levinson + evaluate $1/|A(e^{j\omega})|$ | LPC vs cepstral overlay |
| Cepstral envelope | IFFT log-magnitude, keep low quefrency, back-FFT | Same plot as LPC |
| YIN | Full difference function + cumulative-normalised + threshold + parabolic interp | Cents-accurate with noise slider |
| Reassignment | Three STFTs (w, tw, w') and Auger&ndash;Flandrin formulas | Chirp / bell / impulse |
| Chirp-z | Direct-sum CZT around chosen spiral contour | z-plane contour plot + spectrum overlay |
| Levinson | Full order-by-order recursion; reflection coefficients and error power | Stability check on k_i |
| Audio synthesis | Web Audio API buffer playback | All sounds generated algorithmically |

---

## Key References

1. Smith, J. O. (2011). *Spectral Audio Signal Processing.* W3K Publishing. [Online](https://ccrma.stanford.edu/~jos/sasp/).
2. McAulay, R. J. &amp; Quatieri, T. F. (1986). *Speech Analysis/Synthesis Based on a Sinusoidal Representation.* IEEE Trans. ASSP, 34(4), 744&ndash;754.
3. Serra, X. &amp; Smith, J. O. (1990). *Spectral Modeling Synthesis.* Computer Music Journal, 14(4), 12&ndash;24.
4. Abe, M. &amp; Smith, J. O. (2004). *Design Criteria for the Quadratically Interpolated FFT Method.* CCRMA Tech. Report STAN-M-117.
5. de Cheveign&eacute;, A. &amp; Kawahara, H. (2002). *YIN, a Fundamental Frequency Estimator for Speech and Music.* J. Acoust. Soc. Am., 111(4), 1917&ndash;1930.
6. Kodera, K., Gendrin, R. &amp; de Villedary, C. (1976). *A New Method for the Numerical Analysis of Nonstationary Signals.* Phys. Earth Planet. Int., 12, 142&ndash;150.
7. Auger, F. &amp; Flandrin, P. (1995). *Improving the Readability of Time-Frequency and Time-Scale Representations by the Reassignment Method.* IEEE Trans. SP, 43(5), 1068&ndash;1089.
8. Rabiner, L. R., Schafer, R. W. &amp; Rader, C. M. (1969). *The Chirp z-Transform Algorithm.* IEEE Trans. Audio Electroacoust., 17(2), 86&ndash;92.
9. Atal, B. S. &amp; Schroeder, M. R. (1979). *Predictive Coding of Speech Signals and Subjective Error Criteria.* IEEE Trans. ASSP, 27(3), 247&ndash;254.
10. Markel, J. D. &amp; Gray, A. H. (1976). *Linear Prediction of Speech.* Springer-Verlag.
11. Flanagan, J. L. &amp; Golden, R. M. (1966). *Phase Vocoder.* Bell System Technical Journal, 45(9), 1493&ndash;1509.
12. Laroche, J. &amp; Dolson, M. (1999). *Improved Phase Vocoder Time-Scale Modification of Audio.* IEEE Trans. SAP, 7(3), 323&ndash;332.
13. R&ouml;bel, A. &amp; Rodet, X. (2005). *Efficient Spectral Envelope Estimation.* Proc. DAFx, 30&ndash;35.
14. Engel, J. et al. (2020). *DDSP: Differentiable Digital Signal Processing.* Proc. ICLR 2020.

---

## Related Guides

* [STFT for Sound](https://github.com/BrendanJamesLynskey/STFT_for_Sound) &mdash; Gabor, Allen &amp; Rabiner, the phase vocoder and Griffin&ndash;Lim. Prerequisite for this companion.
* [Wavelets for Sound](https://github.com/BrendanJamesLynskey/Wavelets_for_Sound) &mdash; Kronland-Martinet, Grossmann &amp; Morlet; adaptive time-frequency resolution.
* [Constant-Q Transform for Sound](https://github.com/BrendanJamesLynskey/Constant_Q_Transform_for_Sound) &mdash; Brown &amp; Puckette's log-frequency spectrum.
* [MFCC for Sound](https://github.com/BrendanJamesLynskey/MFCC_for_Sound) &mdash; Davis &amp; Mermelstein; the cepstrum-based ASR feature.
* [MDCT for Sound](https://github.com/BrendanJamesLynskey/MDCT_for_Sound) &mdash; Princen &amp; Bradley; the transform inside every codec.
* [Sound Transforms &mdash; History and Practical Guide](https://github.com/BrendanJamesLynskey/Sound_Transforms_History) &mdash; meta-guide with a decision tree.
* [DDSP Differentiable DSP](https://github.com/BrendanJamesLynskey/DDSP_Differentiable_DSP) &mdash; the neural descendant of SMS.
* [PhaseVocoder](https://github.com/BrendanJamesLynskey/PhaseVocoder) &mdash; minimal reference implementation.
* [MusicalTimeStretchingPitchShifting](https://github.com/BrendanJamesLynskey/MusicalTimeStretchingPitchShifting) &mdash; the working-software sibling.
* [Synth Additive](https://github.com/BrendanJamesLynskey/Synth_Additive), [Synth Spectralist](https://github.com/BrendanJamesLynskey/Synth_Spectralist) &mdash; synthesis cousins.

### Sibling Companion guides to JOS books

* [Companion to Mathematics of the DFT](https://github.com/BrendanJamesLynskey/Companion_JOS_Mathematics_of_the_DFT)
* [Companion to Introduction to Digital Filters](https://github.com/BrendanJamesLynskey/Companion_JOS_Introduction_to_Digital_Filters)
* [Companion to Physical Audio Signal Processing](https://github.com/BrendanJamesLynskey/Companion_JOS_Physical_Audio_Signal_Processing)
* [Companion to Audio Signal Processing in Faust](https://github.com/BrendanJamesLynskey/Companion_JOS_Audio_Signal_Processing_in_Faust)

---

## License

MIT &mdash; use it however you like. Attribution appreciated but not required.
