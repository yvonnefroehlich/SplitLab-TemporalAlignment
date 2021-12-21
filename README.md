# Temporal Alignment of Seismic Traces in _SplitLab_

This material addresses an error source in the code of the shear wave splitting package _SplitLab_ 
([**_Wüstefeld et al., 2008_**](https://doi.org/10.1016/j.cageo.2007.08.002))
causing a wrong temporal alignment of the single traces (Z, N, E components) of one earthquake _relative_ to each other. 
The resulting wrong horizontal particle motion and wrong waveforms in the ray (LQT) coordinate system lead 
to a wrong shear wave splitting measurement.<br/>
Here a test with seismologcial data for your personal _SplitLab_ version and a suggested correction 
of the _SplitLab_ function `getFileAndEQseconds.m` for the offical _SplitLab_ versions are provided.<br/>
This modified _SplitLab_ function is also introduced by _StackSplit_
([**_Grund, 2017_**](https://doi.org/10.1016/j.cageo.2017.04.015)) 
[version 3.0](add_zenodo_link_when_available) during the installation.




## Citiation

If you make use of this material please cite the relating publication:

**_Fröhlich, Y., Grund, M. & Ritter, J. R. R. (202x)_**. 
On the effects of wrongly aligned seismogram components for shear wave splitting analysis. 
Annals of Geophysics, volume xx, issue xx, pages xxx-xxx. doi: xxx.

Futhermore you can cite the [Zenodo Doi](add_zenodo_link_when_available) given above.



## Content

- folder `00_SAC_files`
  - subfolders corresponding to some of the filename formats supported by _SplitLab_
  - Vertical (Z), North (N), East (E) components as SAC-files 
  - sampling interval: 0.05 sec 

- folder `01_your_results`
  - until now empty
  - output folder for your own shear wave splitting measurement results
  
- folder `02_SL_diagnosticplots`
  - _SplitLab_ diagnostic plots for comparison (pdf and png format)
  - without (...`_wrong`) and with (...`_correct`) consideration of the milliseconds (msec)

- folder `03_SL_getFileAndEQseconds`
  - corrected or modified _SplitLab_ function `getFileAndEQseconds.m`
  - all three _SplitLab_ versions (...`_SLxyz`)



## Test

### How to do

**0) Choose one of the three provided examples (see subsection "Details on earthquakes and traces")**

  - Stuttgart (STU), 2001/06/29 (2001.180) 18:35 (UTC)
  - Stuttgart (STU), 2009/11/14 (2009.318) 19:44 (UTC)
  - Échery (ECH), 2018/08/28 (2018.240) 22:35 (UTC)

**1) Set up _SplitLab_ project**

<details><summary>click for single steps</summary>
<p>

  - general
    - seismic data directory
	  - go to folder `00_SAC_files`
	  - select subfolder with preferred filename format
    - output directory
	  - select folder `01_your_results`
  - station
    - Stuttgart
      - station code: STU
      - network code: GE
      - latitude in deg North: 48.771
      - longitude in deg East: 9.194
    - Échery
      - station code: ECH
      - network code: G
      - latitude in deg North: 48.216
      - longitude in deg East: 7.159
  - event window
    - (moment) magnitude: 6.00 to 9.75
    - (epicentral) distance in deg: 90 to 140
    - (hypocentral) depth in km: 0 to 1000
    - start and end date: corresponding to the date of the chosen example / earthquake
  - phases
    - Earth model: IASP91
    - phases: (at least) SKS, SKKS, PKS
  - find files
    - file search string: corresponding to the chosen filename format
    - offset: 0 sec
    - tolerance: 420 sec

</p>
</details>

**2) Perform shear wave splitting measurement**

  - bandpass filter: 0.020 Hz (lower corner), 0.20 Hz or 0.15 Hz (upper corner)
  - coordinate system: LQT
  - phase: SKS

**3) Compare your result / _SplitLab_ diagnostic plot with the provided diagnostic plots**

  - folder `02_SL_diagnosticplots`: diagnostic plots for wrong and correct relative temporal alignment
  - shape of the E-N particle motion: linear or elliptic ?
  - SKS phase-related signal on the transverse (T) component: no or yes ?


### Details on earthquakes and traces

<details><summary>click for more information</summary>
<p>

**Stuttgart (STU), 2001/06/29 (2001.180)**
- earthquake
  - date: 2001/06/29 (2001.180)
  - time: 18:35:51 (UTC)
  - moment magnitude: 6.1
  - source region: Southern Bolivia
  - hypocentral depth: 274 km
  - backazimuth: 246.5 deg
  - epicentral distance: 95.29 deg
- traces
  - msecs of start times: North = 0027, East = 0927, Vertical = 0627
  - relative msec difference: |E-N| = |900| i. e. |18| samples

**Stuttgart (STU), 2009/11/14 (2009.318)**
- earthquake
  - date: 2009/11/14 (2009.318)
  - time: 19:44:29 (UTC)
  - moment magnitude: 6.2
  - source region: Jujuy province, Argentina
  - hypocentral depth: 220 km
  - backazimuth: 244.5 deg
  - epicentral distance: 98.15 deg
- traces
  - msecs of start times: North = 0145, East = 0895, Vertical = 0945
  - relative msec difference: |E-N| = |750| i. e. |15| samples

**Échery (ECH), 2018/08/28 (2018.240)**
- earthquake
  - date: 2018/08/28 (2018.240)
  - time: 22:35:13 (UTC)
  - moment magnitude: 6.5
  - source region: Mariana Islands
  - hypocentral depth: 60 km
  - backazimuth: 40.1 deg
  - epicentral depth: 106.00 deg
- traces
  - msecs of start times: North = 0950, East = 0000, Vertical = 0950
  - relative msec difference: |E-N| = |950| i. e. |19| samples

</p>
</details>



## _SplitLab_ function `getFileAndEQseconds.m`

### _SplitLab_ versions

- folder `03_SL_getFileAndEQseconds`
  - [_SplitLab_ 1.0.5](http://splitting.gm.univ-montp2.fr/) (...`_SL105`) ([**_Wüstefeld et al., 2008_**](https://doi.org/10.1016/j.cageo.2007.08.002))
  - [_SplitLab_ 1.2.1](https://robporritt.wordpress.com/software/) (...`_SL121`) (**_Porritt, 2014_**)
  - [_SplitLab_ 1.9.0](https://github.com/IPGP/splitlab) (...`_SL190`)


### How to do

- `xyz` or `x.y.z` indicates the _SplitLab_ version
- go to folder `~/SplitLabx.y.z/Tools/` on your computer
- rename the existing function `getFileAndEQseconds.m` e. g. `getFileAndEQseconds_original.m` in this folder
- copy and past the modified function `getFileAndEQseconds_SLxyz.m` into this folder
- remove the end of the filename `_SLxyz`
- **assign earthquake catalogue and seismological data in your _SplitLab_ project**



## References

**_Bowman, J. R. & Ando, M. (1987)_**. Shear-wave splitting in the upper-mantle wedge above the Tonga subduction zone.
Geophysical Journal International, volume 88, issue 1, pages 25-41. doi: https://doi.org/10.1111/j.1365-246X.1987.tb01367.x.

**_GEOFON Data Centre (1993)_**. GEOFON (GeoForschungsNetz).
Deutsches GeoForschungsZentrum (GFZ), Seismic Network. doi: https://doi.org/10.14470/TR560404.

**_GEOSCOPE (1982)_**. French Global Network of broad band seismic stations.
Institut de physique du globe de Paris (IPGP) & Ecole et Observatoire des Sciences de la Terre de Strasbourg (EOST). doi: https://doi.org/10.18715/GEOSCOPE.G.

**_Grund, M. (2017)_**. StackSplit - a plugin for multi-event shear wave splitting analyses in SplitLab.
Computers & Geosciences, volume 105, pages 43-50. doi: https://doi.org/10.1016/j.cageo.2017.04.015.
versions [1.0](https://doi.org/10.5281/zenodo.464385), 2.0, [3.0](add_zenodo_link_when_available) available at https://github.com/michaelgrund/stacksplit.

**_Porritt, R. W. (2014)_**. SplitLab version 1.2.1. available at https://robporritt.wordpress.com/software/.

**_Silver, P. G. & Chan, W. W. (1991)_**. Shear wave splitting and subcontinental mantle deformation.
Journal of Geophysical Research, volume 96, issue B10, pages 16429-16454. doi: https://doi.org/10.1029/91JB00899.

**_Walsh, E., Arnold, R. & Savage, M. K. (2013)_**. Silver and Chan revisited.
Journal of Geophysical Research: Solid Earth, volume 118, issue 10, pages 5500-5515. doi: https://doi.org/10.1002/jgrb.50386.

**_Wüstefeld, A., Bokelmann, G., Zaroli, C. & Barruol, G.  (2008)_**. SplitLab: A shear-wave splitting environment in Matlab.
Computers & Geosciences, volume 34, issue 5, pages 515-528. doi: https://doi.org/10.1016/j.cageo.2007.08.002.
version 1.0.5 available at http://splitting.gm.univ-montp2.fr/ and version 1.9.0 available at https://github.com/IPGP/splitlab.