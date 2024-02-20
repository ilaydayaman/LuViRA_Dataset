# Audio Details

* The audio recordings are single-channel WAV-files with a sample rate of $96$\kHz and $16$-bit resolution. It can be noted that the raw recordings were 32 bit before being cut to size, possibly recorded at 24 bit resolution. The raw files are not published currently.
* On Grid110 trajectory, microphone 7 shows a period of particular noise overlay. This noise has been seen on other trajectories as well, mostly on microphone 7 and 9.
* The dataset does not state that individual microphone gain has been calibrated to allow signal power as an absolute distance measure. 
* It is recommended to assume that microphone locations may change between trajectories. Given locations were retrieved from the raw GT files, and calculated as the mid-point (average) of its two markers. For each trajectory the median X,Y and Z value for each microphone is thought to be a good approximate location.
* The ground truth system may be accurate, but there are occasions where a readout of a microphone location does fluctuate, which is the reason for using median position. 

* Random manual people2 is missing the recording of microphone 4 
