# skymap-overlap

Compute the overlap between two skymaps

## Requirements
 * scipy-stack (numpy, scipy, matplotlib, pandas)
 * astropy
 * healpy
 * ligo.skymap (only supports Python3.X)
 * ligo-gracedb (for batch downloading skymaps)
 * pycondor

## Installation
```bash
pip install .
```

## Usage
### Computing the overlap between two skymaps
To compute the overlap between two skymaps $`p(\Omega)`$ and $`q(\Omega)`$, one can use `compute_overlap` to compute the overlap. Currently the script computes three overlap statistics:

 1. Posterior overlap, which is defined as
 ```math
 \displaystyle\int_{\rm all sky} p(\Omega)q(\Omega) \; d\Omega
 ```

 2. Normalized posterior overlap, which is defined as
 ```math
 \frac{\displaystyle\int_{\rm all sky} p(\Omega)q(\Omega) \; d\Omega}{\sqrt{\displaystyle\int_{\rm all sky} p(\Omega)p(\Omega) \; d\Omega}\sqrt{\displaystyle\int_{\rm all sky} q(\Omega)q(\Omega) \; d\Omega}}
 ```
 
 3. 90% credible region overlap

Given two FITS skymaps, the simplest usage is
```
compute_overlap --skymap SKYMAP1.fits.gz --skymap SKYMAP2.fits.gz
```


### Computing the pairwise overlap between a batch of skymaps
To compute the pairwise overlap between a batch of skymaps, you can use `compute_overlap_from_skymaps_pipe` which generates a DAG file
for you to submit to a HTCondor-compatible cluster to calculate the overlap.
The simplest usage is
```
compute_overlap_from_skymaps_pipe --skymap SKYMAP1.fits.gz --skymap SKYMAP2.fits.gz --skymap SKYMAP3.fits.gz
```
so on and so forth. There are also other options for example the accounting tag (if you are running on LDG).

### Batch downloading skymaps from GraceDB
You can use `download_skymap` to download skymaps from GraceDB given the GID or SID. The simplest usage is
```
download_skymap GID_or_SID
```
By default it will download LALInference skymaps whenever possible. There is also an option `--bayestar` to only use
skymaps generated by bayestar.

## Author
Rico K. L. Lo @ka-lok.lo