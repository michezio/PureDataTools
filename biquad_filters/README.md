# Biquad filters

Biquadratic filters are very flexibles and can generate almost every kind of second order filter, but it's quite complex to calculate the right coefficients for each single case. That's why I created these helpers that generate different types of filters using common parameters such as central frequency, bandwidth or slope, gain/attenuation and so on.

A digital biquadratic filter can be rapresented by the following diagram:  

![](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0b/Biquad_filter_DF-IIx.svg/400px-Biquad_filter_DF-IIx.svg.png)  
where the parameters `a` are the feedback coefficients and `b` are the feedforward ones. The transfer function `H(z)`, normalized such as `a0 = 1` is the following:  
![](https://latex.codecogs.com/svg.image?H(z)=\frac{b_0+b_1z^{-1}+b_2z^{-2}}{1-a_1z^{-1}-a_2z^{-2}})  
For the filters we will calculate `a0`, then each of the other coefficients will be divided by that.

In Pd there is the `biquad~` object but its usage is only with those coefficients:
`[biquad~ -a1 -a2 b0 b1 b2]`
So we need to find those coefficients given the measures we need. We are going to use `Fs` as the sampling frequency, `fc` as the central frequency of the filter, `Q` or `S` or `BW` respectively the quality factor, the slope (dB/Oct) or the bandwidth (-3dB from peak) of the filter, and `dBGain` as the gain in dB for some filters.

To calculate the coefficients we are going to use these variables here declared:  
![](https://latex.codecogs.com/svg.image?{\omega}_0=2\pi\frac{f_0}{F_s}~~~~~~\alpha=\frac{sin({\omega}_0)}{2Q}~~~~~~A=10^{\frac{dBGain}{40}})  
In case we are using `BW` or `S` we can get `Q` with the following formulas:  
![](https://latex.codecogs.com/svg.image?Q_{BW}=\left(2{\cdot}sinh\left(\frac{ln(2)}{2}{\cdot}BW{\cdot}\frac{{\omega}_0}{sin({\omega}_0)}\right)\right)^{-1})  
![](https://latex.codecogs.com/svg.image?Q_{S}=\left(\sqrt{\left(A+\frac{1}{A}\right)\left(\frac{1}{S}-1\right)+2}\right)^{-1})  

Another "variable" that's quite useful with shelving filters is the following:  
![](https://latex.codecogs.com/svg.image?2\alpha\sqrt{A}=sin({\omega}_0)\sqrt{\left(A^2+1\right)\left(\frac{1}{S}-1\right)+2A})  

## Content

### `[bq_lowpass~ fc Q]` Low-Pass Filter

![](https://latex.codecogs.com/svg.image?a_0=1+\alpha)  
![](https://latex.codecogs.com/svg.image?a_1=-2cos({\omega}_0))  
![](https://latex.codecogs.com/svg.image?a_2=1-\alpha)  
![](https://latex.codecogs.com/svg.image?b_0=\frac{1-cos({\omega}_0)}{2})  
![](https://latex.codecogs.com/svg.image?b_1=1-cos({\omega}_0))  
![](https://latex.codecogs.com/svg.image?b_2=\frac{1-cos({\omega}_0)}{2})  

### `[bq_highpass~ fc Q]` High-Pass Filter

![](https://latex.codecogs.com/svg.image?a_0=1+\alpha)  
![](https://latex.codecogs.com/svg.image?a_1=-2cos({\omega}_0))  
![](https://latex.codecogs.com/svg.image?a_2=1-\alpha)  
![](https://latex.codecogs.com/svg.image?b_0=\frac{1+cos({\omega}_0)}{2})  
![](https://latex.codecogs.com/svg.image?b_1=-1-cos({\omega}_0))  
![](https://latex.codecogs.com/svg.image?b_2=\frac{1-cos({\omega}_0)}{2})  

### `[bq_allpass~ fc Q]` All-Pass Filter
For the all-pass filter, `fc` and `Q` influence the behaviour in the phase response of the filter leaving the amplitude unchanged.

![](https://latex.codecogs.com/svg.image?a_0=1+\alpha)  
![](https://latex.codecogs.com/svg.image?a_1=-2cos({\omega}_0))  
![](https://latex.codecogs.com/svg.image?a_2=1-\alpha)  
![](https://latex.codecogs.com/svg.image?b_0=1-\alpha)  
![](https://latex.codecogs.com/svg.image?b_1=-2cos({\omega}_0))  
![](https://latex.codecogs.com/svg.image?b_2=1)  

### `[bq_bandpass~ fc BW]` Band-Pass Filter
`[bq_bandpassq~ fc Q]` variant with `Q` instead of `BW`.

![](https://latex.codecogs.com/svg.image?a_0=1+\alpha)  
![](https://latex.codecogs.com/svg.image?a_1=-2cos({\omega}_0))  
![](https://latex.codecogs.com/svg.image?a_2=1-\alpha)  
![](https://latex.codecogs.com/svg.image?b_0=\alpha)  
![](https://latex.codecogs.com/svg.image?b_1=0)  
![](https://latex.codecogs.com/svg.image?b_2=-\alpha)  

### `[bq_bandpasspeak~ fc Q]` Peaking Band-Pass Filter

![](https://latex.codecogs.com/svg.image?a_0=1+\alpha)  
![](https://latex.codecogs.com/svg.image?a_1=-2cos({\omega}_0))  
![](https://latex.codecogs.com/svg.image?a_2=1-\alpha)  
![](https://latex.codecogs.com/svg.image?b_0=\frac{sin({\omega}_0)}{2}=Q\alpha)  
![](https://latex.codecogs.com/svg.image?b_1=0)  
![](https://latex.codecogs.com/svg.image?b_2=\frac{-sin({\omega}_0)}{2}=-Q\alpha)  

### `[bq_notch~ fc BW]` Notch Filter
`[bq_notchq~ fc Q]` variant with `Q` instead of `BW`.

![](https://latex.codecogs.com/svg.image?a_0=1+\alpha)  
![](https://latex.codecogs.com/svg.image?a_1=-2cos({\omega}_0))  
![](https://latex.codecogs.com/svg.image?a_2=1-\alpha)  
![](https://latex.codecogs.com/svg.image?b_0=1)  
![](https://latex.codecogs.com/svg.image?b_1=-2cos({\omega}_0))  
![](https://latex.codecogs.com/svg.image?b_2=1)  

### `[bq_peak~ fc BW dBGain]` Peak Filter
`[bq_peakq~ fc Q dBGain]` variant with `Q` instead of `BW`.

![](https://latex.codecogs.com/svg.image?a_0=1+\frac{\alpha}{A})  
![](https://latex.codecogs.com/svg.image?a_1=-2cos({\omega}_0))  
![](https://latex.codecogs.com/svg.image?a_2=1-\frac{\alpha}{A})  
![](https://latex.codecogs.com/svg.image?b_0=1+{\alpha}A)  
![](https://latex.codecogs.com/svg.image?b_1=-2cos({\omega}_0))  
![](https://latex.codecogs.com/svg.image?b_2=1-{\alpha}A)  

### `[bq_lowshelving~ fc dBGain S]` Low Shelving Filter

![](https://latex.codecogs.com/svg.image?a_0=A+1+(A-1)cos({\omega}_0)+2\alpha\sqrt{A})  
![](https://latex.codecogs.com/svg.image?a_1=-2(A-1+(A+1)cos({\omega}_0)))  
![](https://latex.codecogs.com/svg.image?a_2=A+1+(A-1)cos({\omega}_0)-2\alpha\sqrt{A})  
![](https://latex.codecogs.com/svg.image?b_0=A(A+1-(A-1)cos({\omega}_0)+2\alpha\sqrt{A}))  
![](https://latex.codecogs.com/svg.image?b_1=2A(A-1-(A+1)cos({\omega}_0)))  
![](https://latex.codecogs.com/svg.image?b_2=A(A+1-(A-1)cos({\omega}_0)-2\alpha\sqrt{A}))  

### `[bq_highshelving~ fc dBGain S]` High Shelving Filter

![](https://latex.codecogs.com/svg.image?a_0=A+1-(A-1)cos({\omega}_0)+2\alpha\sqrt{A})  
![](https://latex.codecogs.com/svg.image?a_1=2(A-1-(A+1)cos({\omega}_0)))  
![](https://latex.codecogs.com/svg.image?a_2=A+1-(A-1)cos({\omega}_0)-2\alpha\sqrt{A})  
![](https://latex.codecogs.com/svg.image?b_0=A(A+1+(A-1)cos({\omega}_0)+2\alpha\sqrt{A}))  
![](https://latex.codecogs.com/svg.image?b_1=-2A(A-1+(A+1)cos({\omega}_0)))  
![](https://latex.codecogs.com/svg.image?b_2=A(A+1+(A-1)cos({\omega}_0)-2\alpha\sqrt{A}))  
  
  
## Extra

### `[bq_fexpr~]` Generic biquad filter using fexpr~

This is just an implementation of the differential equation of a generic biquadratic filter (the one described in the introduction) using `[fexpr~]` to work on raw samples. This is in theory much heavier than the builtin `[biquad~]` object but allows to use signals to control the parameters.

### `[bq_vcraw~]` Generic biquad filter using raw pole/zero filters

This is an implementation of a biquadratic filter using raw `[cpole~]` and `[czero~]` filter objects. It uses `[quadroots~]` object from `utils` folder to calculate their parameters so it may be a little bit heavy. This however allows for the parameters to be controlled by signals instead of floats. Also this filters outputs both real and imaginary signal from two different outlets.

### Speaker emulations

All the other abstractions are compound filters made of different biquadratic ones that aproximate the frequency response of real speakers and tube amplifiers. I use them at the end of a guitar effect chain to simulate the cabinet.

## Credits

All formulas taken from [Audio EQ Cookbook by Robert Bristow-Johnson](https://webaudio.github.io/Audio-EQ-Cookbook/audio-eq-cookbook.html)