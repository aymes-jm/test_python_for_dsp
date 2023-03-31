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

- Python pur : 3.4 s
- Python avec fft numpy (*numpy.fft*) : 87 ms
- Python avec fft FFTW (*pyFFTW*) : 33 ms
- Python compilé avec Numba
	- single thread : 19.3 ms
	- multithreads : 4 ms
	- sur GPU (*numba.cuda*) : 2.4 ms
- Python compilé avec Cython
	- single thread : 40 ms
	- multithreads : 95 ms
- Python et librairie CuPy (fft sur GPU) : 1.7 ms

- Julia pur :
	- single thread : 8.5 ms
	- multithreads : 1.3 ms
- Julia avec fft FFTW (*FFTW.jl*) : 18 ms
- Julia avec FFT sur GPU (*CUDA.jl*) : 2.8 ms

___

## Conclusions

- Ne pas utiliser des traitements par en Python pur !!!
- Julia est plus performant en CPU pur que Numba (compilateur JIT Python),  
le gain en vitesse d'exécution est de l'ordre de 2
- Numba apporte une réelle performance au Python  
et permet d'écrire des kernels GPU en syntaxe Python
- l'implémentation FFTW est plus efficace en Julia qu'en Python (facteur 2)
- CuPy propose une très bonne implémentation de la FFT sur GPU,  
meilleure que celle de Julia (facteur 2 quasiment)
- Cython semble peu performant (2 fois plus lent que Numba en single thread)  
en particulier en multithreads (20 fois plus lent !)  
Pb d'écriture du code probablement...
- La performance de traitement par FFT sous Cupy rattrape celle de Julia  
en multithreads CPU pour une taille de signal plus importante (2^23 par ex)

___

## TODO

- Ecrire un code C/C++ permettant d'établir une performance de référence,  
à compiler avec implémentation SIMD/SVML pour un temps d'exécution optimisé
- Investiguer le code Cython, en particulier en implémentation parallèle
- Ecrire un kernel C-like en CUDA pour test à l'aide des librairies CuPy/Python  
et CUDA/Julia pour comparaison avec la compilation GPU de Numba
