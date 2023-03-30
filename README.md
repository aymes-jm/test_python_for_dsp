# Utilisation Python et Julia sur un cas de traitement DSP simple
___

## Cas d'étude

Il s'agit d'une recherche d'un mot unique (UW) de 32 symboles dans un signal de 1 Méchantillons.

- par recherche naïve (symbole par symbole)
- ou recherche globale par corrélation via FFT
___

## Configuration PC utilisée

CPU = 11th Gen Intel® Core™ i9-11950H @ 2.60GHz × 16

GPU = NVIDIA Corporation GA104GLM (RTX A5000 Mobile), 16 Go/256 bits, 6144 cores, PCIe x16 Gen4
___

## Solutions avec Python

- Python pur
- Python avec fft numpy (*numpy.fft*)
- Python avec fft FFTW (*pyFFTW*)
- Python compilé avec Numba
	- single thread
	- multithreads
	- sur GPU (*numba.cuda*)
- Python compilé avec Cython
	- single thread
	- multithreads
- Python et librairie CuPy (GPU)
___

## Solutions avec Julia

- Julia pur
	- single thread
	- multithreads
- Julia avec fft FFTW (*FFTW.jl*)
- Julia sur GPU (*CUDA.jl*)
___

## Résultats

**TODO**
