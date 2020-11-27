# csst_mock_catalog

#### Columns Definition

- ID  
  ID in Ilbert's (2009) COSMOS catalog.

- Z_BEST  
  Photo-z in Ilbert's (2009) catalog.

- FluxSim_*  
  Simulated mock fluxes for CSST's bands through image simulation from Meng. The fluxes are not intended to enclose total fluxes for objects. Apertures are set to give higher SNR than total flux apertures.

- ErrFlux_*  
  Corresponding errors for mock fluxes.

- Npix  
  Number of pixels inside the aperture within which fluxes are measured. For a certain object, every band are measured with the same aperture.

- Drms_sec  
  The measure of galaxies' size in arcsec, using the equation (11) in Leauthaud et al. (2007) which measures the second-order moment of each galaxy.

The code names NUV1, NUV2 actually means the same NUV band of CSST. Each denotes measurement on 2 NUV frames' stacking. Actually NUV band has 4 chips and should stack 4 frames, but in this simulation we split them into two groups. When running our photo-z code, we can throw in two files of filter curves named as NUV1.res and NUV2.res, assuming the code can deal them as two bands.

The same for y1 and y2 bands.

-----------

#### Method of Simulation

###### Sample and Data  

Ilbert et al. (2009) COSMOS 2-deg^2 photo-z catalog, which collaborates Subaru, CFHT, UKIRT, etc. observations in optical--NIR scope.

COSMOS ACS v2.0 mosaic images, which have pixel sizes as 0.03"/pix. 16 tiles are used currently, with each tile FOV 10'x10'. 

Totally, 62,300 galaxy samples are obtained.



###### Outline of Procedures

1. Fit SED templates for Ilbert's catalog with fixed photo-zs given by the catalog using LePhare. Emission-lines are added automatically. When SEDs (with emission-lines) are given by the fitting, they are considered as reasonable models, and photometry data in Ilbert's catalog will be omitted in the following steps.
1. Do image convolution for COSMOS ACS F814W images with a Gaussian Kernel to simulate CSST z-band resolution (80% energy enclosed within 0.165" radius circle). Before convolution, each 0.03" pixel was split to four 0.015" sub-pixels; after convolution, 5x5 0.015" sub-pixels were combined as a single 0.075" pixel, which is approximate to CSST pixel size. As an effect of convolution, high frequency noises are smoothed more significant rather than low frequency patterns such as galaxies.

2. Image stamps are cut out for each galaxy, and are scaled to match SED in terms of electrons for each band. Then, sky background and dark current are added. Poisson randomization are performed to the stamp image. After these, read-out noise is added. Apply Gain=1.5 e-/ADU, and perform quantization. 
   Such, mock image stamps are generated for CSST bands. 

3. Do force photometry. 
   Stack g,r,i,z band images as detection image. Extract the central object and mask surrounding objects, and calculate the photometry aperture. Then, fix the aperture and perform force photometry for each band. Electrons --> photons --> Flux can be measured and converted within the aperture. Flux may be negative or positive, both will be used in photo-z test. Errors of Fluxes are calculated through noises and number of pixels within the aperture.
   ![image-20201127165614324](/home/sola/.config/Typora/typora-user-images/image-20201127165614324.png)

   The samples have no detection limit criterion, as long as they can be detected on the stacked image.







