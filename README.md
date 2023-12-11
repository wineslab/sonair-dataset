# SonAIr Dataset - Real-Time Deep Learning For Underwater Acoustic Spectrum Sensing and Classification

## Introduction

This dataset is employed for the development and validation of SonAIr, a real-time system that utilizes Deep Learning techniques to classify and localize signals in the underwater channel. It comprises real-world underwater acoustic transmission recordings spanning 7 days in two different locations and multiple transceiver configurations.

## Citation

>D. Uvaydov, D. Unal, K. Enhos, E. Demirors and T. Melodia, "Sonair: Real-Time Deep Learning For Underwater Acoustic Spectrum Sensing and Classification," in Proc. of IEEE International Conference on Distributed Computing in Smart Systems and the Internet of Things (DCOSS-IoT), Pafos, Cyprus, June 2023.

Please reference the paper if you use the dataset: [bibtex entry](https://ece.northeastern.edu/wineslab/wines_bibtex/UvaydovDCOSS2023.txt)

## Repository

The dataset can be downloaded from [http://hdl.handle.net/2047/D20620623](http://hdl.handle.net/2047/D20620623)

## Dataset Structure

The compressed archive has 7 days of recording arranged in folders labeled with corresponding date codes. Recordings from off-shore deployments are located in the folder `20220708`, while the rest are sourced from marina deployments. 

File names of recordings follow "`modulation_class`_`channel_vector`.dat" format.

`modulation_class` can take the following values:
- `fsk`
- `css`
- `ofdm`
- `empty`

`channel_vector` is a 20-element binary vector with each element indicating whether a channel is in use. The system bandwidth of 50 kHz is partitioned into 2.5 kHz wide channels spanning -25 kHz to 25 kHz (i.e. leftmost bit corresponds to the first channel -25 kHz to -22.5 kHz). For instance, a recording of OFDM-modulated packets of 15kHz bandwidth occupies channels 7-12 and is labeled as `ofdm_00000001111110000000.dat`. Empty classes have all zero channel occupancy vectors.

Recordings have only one type of modulation class and transmission bandwidths align with the channel grid. There may be slight power leakage to adjacent channels. In addition, interference may be present at these deployment locations resulting from marine traffic.

In each folder, raw recording files of interleaved 32-bit float I/Q samples can be found. The sampling rate of files is 625 ksamp/s and the bandwidth of the acoustic transmissions is 50 kHz. The recordings can be decimated as performed in our work. 

The files can be read with the following NumPy code:

```
import numpy as np
data = np.fromfile(filename, dtype=np.complex64)
```
Alternatively [read_complex_binary](https://github.com/gnuradio/gnuradio/blob/main/gr-utils/octave/read_complex_binary.m) function in MATLAB/Octave and file source block in GNU Radio can be used to read the files.
