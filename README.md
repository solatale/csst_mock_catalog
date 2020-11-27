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

-----------

#### Method of Simulation

###### Sample and Data  

Ilbert et al. (2009) COSMOS 2-deg^2 photo-z catalog, which collaborates Subaru, CFHT, UKIRT, etc. observations in optical--NIR scope.

COSMOS ACS v2.0 mosaic images, which have pixel sizes as 0.03"/pix.



###### Outline of Procedures

1. Fit SED templates for Ilbert's catalog with fixed photo-zs given by the catalog using LePhare. Emission-lines are added automatically. When SEDs (with emission-lines) are given by the fitting, they are considered as reasonable models, and photometry data in Ilbert's catalog will be omitted in the following steps.
2. 


