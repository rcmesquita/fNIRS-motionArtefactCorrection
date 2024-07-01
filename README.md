# fNIRS-motionArtefactCorrection

This code contains the hybrid motion artefact correction for fNIRS signals, as proposed in [Novi et al., Neurophotonics, 2020](https://www.spiedigitallibrary.org/journals/neurophotonics/volume-7/issue-01/015001/Functional-near-infrared-spectroscopy-for-speech-protocols--characterization-of/10.1117/1.NPh.7.1.015001.full#_=_). 

Requirements: MATLAB 2016b (Mathworks Inc., Milford, MA). 

The main function, *HybridMA.m*, identifies and corrects motion artefacts in time series data using a combination of spline interpolation followed by a Wavelet filter. The function identifies segments where motion artefacts exceed a user-specified threshold and applies a spline-based correction. Then, the spline-corrected data is decomposed into wavelets using a wavelet transform; the filter removes the wavelets with coefficients higher than a threshold, which can also be specified by the user.

**Inputs:**
- timeSeriesData: Matrix of input data (time points x channels).
- acquisitionFrequency: Sampling frequency of the data acquisition system.
- splineThreshold: Motion detection identification threshold.
- waveletThreshold: Parameter used to compute the statistics (iqr = 1.5 is 1.5 times the interquartile range and is usually used to detect outliers). Increasing it, it will delete fewer coefficients. If iqr<0 then this function is skipped.
- K: Free parameter for motion correction (leave empty for default. Default: 2.5*acquisitionFrequency).

**Outputs:**
- hybridCorrectedData: Motion-corrected time series by hybrid approach, using spline and wavelet combination (time points x channels).

The algorithm is detailed in 
Sergio L. Novi, Erin Roberts, Danielle Spagnuolo, Brianna M. Spilsbury, D'manda C. Price, Cara A. Imbalzano, Edwin Forero, Arjun G. Yodh, Glen M. Tellis, Cari M. Tellis, Rickson C. Mesquita, "Functional near-infrared spectroscopy for speech protocols: characterization of motion artifacts and guidelines for improving data analysis," Neurophoton. 7(1) 015001 (10 January 2020) https://doi.org/10.1117/1.NPh.7.1.015001

The Wavelet filter was adapted from HomER 2 and is based on
Behnam Molavi, Guy A Dumont, "Wavelet-based motion artifact removal for functional near-infrared spectroscopy," Physiol. Meas. 33 259. (25 January 2012) https://doi.org/10.1088/0967-3334/33/2/259

Please cite these works when using this code. 
