# ASAP-Hankel
This is the Matlab code repo for a fast provable non-convex spectrally sparse signal recovery algorithm introduced in [1], which has theoretical global linear convergence guarantee and high robustness in practice. 

###### To display math symbols properly, one may have to install a MathJax plugin. For example, [MathJax Plugin for Github](https://chrome.google.com/webstore/detail/mathjax-plugin-for-github/ioemnmodlmafdkllaclgeombjnmnbima?hl=en).


## Installation
Our algorithm uses the full size truncated SVD exactly once, during its initialization. However, this one-time usage has become the bottleneck of our speed comparing to the speed of the rest parts. We choose to use PROPACK to speed up this one-time full size truncated SVD. 

For running our code successfully, the user should download and install the "PROPACK for Matlab" package from http://sun.stanford.edu/~rmunk/PROPACK/. 

PROPACK should be installed under the same directory with the other AccAltProj codes. After installation, your directory should read like:
```
|-PROPACK
	|- Afunc.m
 	|- AtAfunc.m
	...
|- AAP_Hankel_1D.m
|- AAP_Hankel_2D.m
...
```
  
\*  If user wish not to install PROPACK, they may change "lansvd" to "svds" on line 105 and 110 of *AccAltProj.m*, as well as on line 4 of *get_mu_kappa.m*. This will allow the user to run the algorithm without PROPACK installation, but may significantly impact the speed.

\*\* User may download a completed AccAltProj package from my personal website, which includes all neccessary parts for running the algorithm directly, without extra installations.

## Demo
Clone the codes and install PROPACK.

You may run the two demo files *test_AAP_Hankel_1D.m* and *test_AAP_Hankel_2D.m* directly now, where *test_AAP_Hankel_1D.m* runs demo test on 1D signals, and *test_AAP_Hankel_2D.m* runs demo tests on 2D signals.

## Warning for AMD CPU User
We found this code runs very slow on AMD CPUs with earlier versions of Matlab. For best experience, please use this code on Intel CPU based computer, and update Matlab to the latest version.

We suspect earier Matlab versions didn't optimize for the AVX instruction sets of AMD CUPs. We welcome you to provide more data points of running AccAltProj on AMD CPUs with different Matlab versions, so we can figure out exactly why there is latency with AMD CPUs. 

Update: We learned that, Matlab calls AVX2 instruction sets for Intel CPU, but calls legacy SSE instruction sets for AMD CPU. While the QR decomp steps in our method have significate prefermence drop with SSE instruction sets, the workaround for AMD user is to active AVX2 for matlab. Read https://www.mathworks.com/matlabcentral/answers/396296-what-if-anything-can-be-done-to-optimize-performance-for-modern-amd-cpu-s?s_tid=ab_old_mlc_ans_email_view for more details.


## Reference
[1] HanQin Cai, Jian-Feng Cai, Tianming Wang, and Guojian Yin. Accelerated Structured Alternating Projections for Robust Spectrally Sparse Signal Recovery. *IEEE Transactions on Signal Processing*, In Press
