# README – Random Sampling Galaxy SED (SMART / ESA project)

This document describes only the generated results of the random-sampling algorithm for galaxy SEDs.  
It is intended for an external reader who opens the folder and needs to understand what the files represent without reading the code.  

---

## 1. Overview of the delivered products

For each combination of AGN model family and host-galaxy type, the following files are provided:

- A data container with all simulated galaxies:  
  `random_sampling_galaxies_AGN{X}_HOST{Y}.npz`
  (available via OneDrive due to file size limitations on GitHub)

- A plot showing the ensemble of SEDs (all galaxies in the dataset):  
  `random_sed_plots/random_sampling_galaxies_AGN{X}_HOST{Y}_random_seds_plot.png`

- A synthetic photometry plot for one randomly selected galaxy from the dataset:  
  `photometric_filters_plots/random_sampling_galaxies_AGN{X}_HOST{Y}_one_random_galaxy_photometry.png`

- A metadata file with detailed physical parameters for every simulated galaxy:  
  `metadata/random_sampling_galaxies_AGN{X}_HOST{Y}_metadata.txt`
  (provided in .zip format due to file size limitations)

In total, 8 datasets are delivered:

AGN1 HOST1 → random_sampling_galaxies_AGN1_HOST1.*  
AGN1 HOST2 → random_sampling_galaxies_AGN1_HOST2.*  
AGN2 HOST1 → random_sampling_galaxies_AGN2_HOST1.*  
AGN2 HOST2 → random_sampling_galaxies_AGN2_HOST2.*  
AGN3 HOST1 → random_sampling_galaxies_AGN3_HOST1.*  
AGN3 HOST2 → random_sampling_galaxies_AGN3_HOST2.*  
AGN4 HOST1 → random_sampling_galaxies_AGN4_HOST1.*  
AGN4 HOST2 → random_sampling_galaxies_AGN4_HOST2.*

Each dataset contains 100,000 synthetic galaxies generated through random sampling of physical parameters.

---

## 2 Component activation (ON / OFF flags)

Throughout all datasets, each physical component (Host, Starburst, AGN, Polar dust) is associated with an activation flag labeled as ON or OFF.

These flags represent the physical presence (activeness) of the component in the SED construction:

- ON: the component actively contributes to the total SED.
- OFF: the component is physically absent and contributes zero flux.

Important clarifications:
- The Host galaxy and the AGN components are always ON in all datasets.
- The Starburst and Polar dust components are randomly switched ON or OFF during the sampling.
- Therefore, different galaxies may contain different combinations of components, while still belonging to the same AGN/Host configuration.

---

## 3. Meaning of AGN1, AGN2, AGN3, AGN4

Each dataset uses a fixed AGN torus model family from the SMART library. Only the physical parameters of that model are randomly sampled.

AGN1: CYGNUS
AGN2: Fritz et al. (2006)
AGN3: SKIRTOR / Stalevski et al. (2016)
AGN4: Siebenmorgen et al. (2015)

Within each dataset:
- The AGN component is always ON.
- The AGN model family is fixed.
- Only the internal parameters (geometry, optical depth, viewing angle, etc.) and the normalization are randomly sampled.

---

## 4. Meaning of HOST1 and HOST2

The HOST label refers to the stellar component (host galaxy template library) used in the synthesis.

HOST1: Spheroid – Spheroidal / bulge-dominated galaxies  
HOST2: Disc – Disc-dominated galaxies  

In all datasets:
- The host galaxy component is always ON.
- The difference between HOST1 and HOST2 is purely the stellar population and dust geometry assumed for the galaxy.

This design allows direct comparison of the impact of:
- AGN physics (AGN1–AGN4)
- Host morphology (HOST1 vs HOST2)

on the resulting SED distributions.

---

## 5. Content of the .npz files

Each file `random_sampling_galaxies_AGN{X}_HOST{Y}.npz` contains numerical arrays with:

- Wavelength grid (rest-frame, in microns)
- Total SEDs for all galaxies (host + starburst + AGN + polar dust)
- Individual component contributions (host, SB+AGN+polar)
- Physical parameters for each galaxy:
  - redshift, metallicity  
  - host parameters (optical depth, geometry, inclination, normalization)  
  - starburst parameters (if active)  
  - AGN parameters (4 parameters depending on model family)  
  - polar dust parameters (if active)  
- Component activation flags (ON/OFF for starburst and polar dust)

These files represent the scientific data products and can be used for further analysis, simulations, or machine-learning applications.

Due to their large size, the .npz files are not hosted directly on GitHub and are instead provided via OneDrive.

---

## 6. Random SED ensemble plots (*_random_seds_plot.png)

These plots show:

- The full ensemble of 100,000 SEDs per dataset  
- X-axis: wavelength (micron, logarithmic scale)  
- Y-axis: flux density (arbitrary units, logarithmic scale)  

Purpose:
- Visualize the global diversity of SED shapes  
- Highlight differences between AGN model families  
- Provide qualitative validation of the synthetic population  

Each curve corresponds to one synthetic galaxy.

---

## 7. Synthetic photometry plots (*_one_random_galaxy_photometry.png)

For each dataset, one galaxy is randomly selected and shown with:

- Black curve: the full model SED (rest-frame)
- Colored points: synthetic photometry computed through real filter transmission curves

Photometric points correspond to the following facilities/instruments:
GALEX, Pan-STARRS1, 2MASS, Spitzer, WISE, JWST, IRAS, Euclid, Herschel.

The photometry is computed by:
- Convolving the model SED with real filter curves  
- Applying the galaxy redshift  
- Computing effective wavelengths and synthetic flux densities  

Purpose:
- Demonstrate that synthetic SEDs translate into realistic observables  
- Bridge theoretical models and survey-like photometry  
- Illustrate UV–FIR wavelength coverage for a simulated galaxy  

---

## 8. Metadata files (*_metadata.txt)

For each dataset, the metadata file lists every simulated galaxy individually with:

- Redshift and metallicity  
- Component activation (Host / Starburst / AGN / Polar dust)  
- Host physical parameters  
- Starburst parameters (if active)  
- AGN model family and parameters  
- Polar dust temperature and normalization  
- Flux ranges for each component  

These files ensure:
- Full traceability  
- Reproducibility  
- Inspection of the sampled parameter space  

---

## 9. Scientific scope of the products

These products represent a controlled synthetic experiment designed to:

- Explore the impact of different AGN torus model families on galaxy SEDs  
- Quantify the effect of host morphology (spheroid vs disc)  
- Provide realistic synthetic datasets suitable for:
  - survey simulations  
  - algorithm validation  
  - machine-learning training  
  - forward modelling of multiwavelength surveys  

The outputs represent physically motivated synthetic galaxy populations.
