# Temporal Alignment of Seismic Traces in _SplitLab_ [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.5805029.svg)](https://doi.org/10.5281/zenodo.5805029)

This material addresses an error source in the code of the MATLAB based shear wave splitting software package
_SplitLab_ ([**_Wüstefeld et al., 2008_**](https://doi.org/10.1016/j.cageo.2007.08.002)). The error causes a
wrong temporal alignment of the single traces (Z, N, E components) of one earthquake _relative_ to each other.
The resulting wrong horizontal particle motion and wrong waveforms in the ray (LQT) coordinate system lead to
a wrong shear wave splitting measurement.

Here we provide a test with seismological data for your personal _SplitLab_ version and a suggested correction
of the _SplitLab_ function `getFileAndEQseconds.m` for the publicly available _SplitLab_ versions.

This modified _SplitLab_ function is also introduced by [_StackSplit_](https://github.com/michaelgrund/stacksplit)
([**_Grund, 2017_**](https://doi.org/10.1016/j.cageo.2017.04.015)) version [3.0](https://doi.org/10.5281/zenodo.5802051)
during the installation process.


## Citation

_Zenodo DOI for all versions (latest version)_: [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.5805029.svg)](https://doi.org/10.5281/zenodo.5805029)

If you make use of this material, please cite the relating publications in which this issue is described in detail:

**Peer-reviewed journal article**
- [**_Fröhlich Y., Grund M. & Ritter J. R. R. (2022)_**](https://doi.org/10.4401/ag-8781).
  On the effects of wrongly aligned seismogram components for shear wave splitting analysis.
  *Annals of Geophysics*, 66(2).
  https://doi.org/10.4401/ag-8781.

**Presentation**
- [**_Fröhlich Y. & Ritter J. R. R. (2022)_**]()
  Shear wave splitting analysis and temporal misalignment of seismogram components.
  *48th German Seismology Working Group meeting*, Münster.
  https://doi.org/10.5281/zenodo.14510987.


## Content

- [`00_SAC_files`](https://github.com/yvonnefroehlich/SplitLab-TemporalAlignment/tree/main/00_SAC_files)
  - Subfolders corresponding to some of the filename formats supported by _SplitLab_
  - Vertical (Z), North (N), East (E) components as SAC-files
  - Sampling interval: 0.05 s

- [`01_your_results`](https://github.com/yvonnefroehlich/SplitLab-TemporalAlignment/tree/main/01_your_results)
  - Until now empty
  - Output folder for your own shear wave splitting measurement results

- [`02_SL_diagnosticplots`](https://github.com/yvonnefroehlich/SplitLab-TemporalAlignment/tree/main/02_SL_diagnosticplots)
  - _SplitLab_ diagnostic plots for comparison (PDF and PNG formats)
  - Without (`*_wrong`) and with (`*_correct`) consideration of the milliseconds (msecs)

- [`03_SL_getFileAndEQseconds`](https://github.com/yvonnefroehlich/SplitLab-TemporalAlignment/tree/main/03_SL_getFileAndEQseconds)
  - Modified _SplitLab_ function `getFileAndEQseconds.m`
  - Publicly available _SplitLab_ versions (`*_SLxyz`)


## Test

### How to do

**0) Choose one of the three provided examples (see subsection "Details on earthquakes and traces")**

  - Stuttgart (STU), 2001/06/29 (2001.180) 18:35 (UTC)
  - Stuttgart (STU), 2009/11/14 (2009.318) 19:44 (UTC)
  - Échery (ECH), 2018/08/28 (2018.240) 22:35 (UTC)

**1) Set up _SplitLab_ project**

<details><summary>Click for single steps</summary>
<p>

  - General
    - Seismic data directory
	  - Go to folder `00_SAC_files`
	  - Select subfolder with preferred filename format
    - Output directory
	  - Select folder `01_your_results`
  - Station
    - Stuttgart
      - Station code: STU
      - Network code: GE
      - Latitude in deg North: 48.771
      - Longitude in deg East: 9.194
    - Échery
      - Station code: ECH
      - Network code: G
      - Latitude in deg North: 48.216
      - Longitude in deg East: 7.159
  - Event window
    - Moment magnitude: 6.00 to 9.75
    - Epicentral distance in deg: 90 to 140
    - Hypocentral depth in km: 0 to 1000
    - Start and end date: corresponding to the date of the chosen example / earthquake
  - Phases
    - Earth model: IASP91
    - Phases: (at least) SKS, SKKS, PKS
  - Find files
    - File search string: corresponding to the chosen filename format
    - Offset: 0 s
    - Tolerance: 420 s

</p>
</details>

**2) Perform shear wave splitting measurement**

  - Bandpass filter: 0.020 Hz (lower corner), 0.20 Hz or 0.15 Hz (upper corner)
  - Coordinate system: LQT
  - Phase: SKS

**3) Compare your result / _SplitLab_ diagnostic plot with the provided diagnostic plots**

  - Folder `02_SL_diagnosticplots`: diagnostic plots for wrong and correct relative temporal alignment
  - Shape of the E-N particle motion: elliptic or linear?
  - SKS phase-related signal on the transverse (T) component: yes or no?

### Details on earthquakes and traces

<details><summary>Click for more information</summary>
<p>

**Stuttgart (STU), 2001/06/29 (2001.180)**
- Earthquake
  - Date: 2001/06/29 (2001.180)
  - Time: 18:35:51 (UTC)
  - Moment magnitude: 6.1
  - Source region: Southern Bolivia
  - Hypocentral depth: 274 km
  - Backazimuth: 246.5 deg
  - Epicentral distance: 95.29 deg
- Traces
  - msecs of start times: North = 0027, East = 0927, Vertical = 0627
  - Relative msec difference: |E-N| = |900|, i.e., |18| samples

**Stuttgart (STU), 2009/11/14 (2009.318)**
- Earthquake
  - Date: 2009/11/14 (2009.318)
  - Time: 19:44:29 (UTC)
  - Moment magnitude: 6.2
  - Source region: Jujuy province, Argentina
  - Hypocentral depth: 220 km
  - Backazimuth: 244.5 deg
  - Epicentral distance: 98.15 deg
- Traces
  - msecs of start times: North = 0145, East = 0895, Vertical = 0945
  - Relative msec difference: |E-N| = |750|, i.e., |15| samples

**Échery (ECH), 2018/08/28 (2018.240)**
- Earthquake
  - Date: 2018/08/28 (2018.240)
  - Time: 22:35:13 (UTC)
  - Moment magnitude: 6.5
  - Source region: Mariana Islands
  - Hypocentral depth: 60 km
  - Backazimuth: 40.1 deg
  - Epicentral depth: 106.00 deg
- Traces
  - msecs of start times: North = 0950, East = 0000, Vertical = 0950
  - Relative msec difference: |E-N| = |950|, i.e., |19| samples

</p>
</details>


## _SplitLab_ function `getFileAndEQseconds.m`

### _SplitLab_ versions

- [`03_SL_getFileAndEQseconds`](https://github.com/yvonnefroehlich/SplitLab-TemporalAlignment/tree/main/03_SL_getFileAndEQseconds)
  - _SplitLab_ 1.0.5 (`*_SL105`) ([**_Wüstefeld et al., 2008_**](https://doi.org/10.1016/j.cageo.2007.08.002))
  - [_SplitLab_ 1.2.1](https://robporritt.wordpress.com/software/) (`*_SL121`) (**_Porritt, 2014_**)
  - [_SplitLab_ 1.3.0](https://github.com/nmcreasy/SplitLab1.3.0) (`*_SL130`) (**_Creasy, 2020_**; based on _SplitLab_ 1.2.1)
  - [_SplitLab_ 1.9.0](https://github.com/IPGP/splitlab) (`*_SL190`) (based on _SplitLab_ 1.0.5)

### How to do

- The filename part `xyz` or `x.y.z` indicates the _SplitLab_ version
- Go to the folder `~/SplitLabx.y.z/Tools/` on your computer
- Rename the existing function `getFileAndEQseconds.m`, e.g., `getFileAndEQseconds_original.m` in this folder
- Copy and past the modified function `getFileAndEQseconds_SLxyz.m` into this folder
- Remove the end of the filename `_SLxyz`
- **Assign earthquake catalogue and seismological data in your _SplitLab_ project**


## Releases

| Release | Zenodo DOI |
| --- | --- |
| dev [main branch](https://github.com/yvonnefroehlich/SplitLab-TemporalAlignment) |  |
| [v2.0](https://github.com/yvonnefroehlich/SplitLab-TemporalAlignment/releases/tag/v2.0) | [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.13760807.svg)](https://doi.org/10.5281/zenodo.13760807) |
| [v1.0](https://github.com/yvonnefroehlich/SplitLab-TemporalAlignment/releases/tag/v1.0) | [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.5805030.svg)](https://doi.org/10.5281/zenodo.5805030) |

For details on the single releases see the [changelog](https://github.com/yvonnefroehlich/SplitLab-TemporalAlignment/blob/main/changelog.md).


## Contributing

For bug reports, suggestions, or recommendationsfeel free to
[open an issue](https://github.com/yvonnefroehlich/SplitLab-TemporalAlignment/issues)
or [submit a pull request](https://github.com/yvonnefroehlich/SplitLab-TemporalAlignment/pulls)
directly here on [GitHub](https://github.com/yvonnefroehlich/SplitLab-TemporalAlignment).


## Related topics

In the table below, some other tools for measuring shear wave splitting (besides _SplitLab_)
are listed. Please note, that these tools were not checked regarding the issue
of an incorrect relative temporal alignment of the single component traces.

| Software | Language | Description | Authors |
| --- | --- | --- | --- |
| SplitLab 1.0.5 | MATLAB | Original SplitLab version | Andreas Wüstefeld, Götz Bokelmann & Christophe Zaroli |
| [SplitLab 1.2.1](https://robporritt.wordpress.com/software/) | MATLAB | Update of SplitLab 1.0.5 | Rob W. Porritt |
| [SplitLab 1.3.0](https://github.com/nmcreasy/SplitLab1.3.0) | MATLAB | Update of SplitLab 1.2.1 | Neala M. Creasy |
| [SplitLab 1.9.0](https://github.com/IPGP/splitlab) | MATLAB | Most recent SplitLab version| IPGP |
| [StackSplit](https://github.com/michaelgrund/stacksplit) | MATLAB | Plugin for multi-event analyses in SplitLab | Michael Grund & Yvonne Fröhlich |
| [SplitRacer](https://www.miriam-reiss.com/splitracer) | MATLAB | Semi-automated workflow | Miriam C. Reiss |
| [SplitPy](https://github.com/paudetseis/SplitPy) | Python | Based on SplitLab | Pascal Audet & Andrew Schaeffer |
| [SWSPy](https://github.com/TomSHudson/swspy) | Python | Automated workflow | Tom Hudson, Andrew M. Walker & Joseph Asplet|
| [STADIUM-Py](https://github.com/earthinversion/STADIUM-Py) | Python | Fully automated workflow | Utpal Kumar & Cédric Legendre |
| [Pytheas](https://github.com/ispingos/pytheas-splitting) | Python | Local shear-wave splitting studies | Ioannis Spingos & George Kaviris |
| [Sheba](https://github.com/jwookey/sheba) | Fortran |  | James Wookey |
| [SeisSplit.jl](https://github.com/anowacki/SeisSplit.jl) | Julia |  | Andy Nowacki |


## References

- [**_Bowman, J. R. & Ando, M. (1987)_**](https://doi.org/10.1111/j.1365-246X.1987.tb01367.x).
  Shear-wave splitting in the upper-mantle wedge above the Tonga subduction zone.
  *Geophysical Journal International*, volume 88, issue 1, pages 25-41.
  https://doi.org/10.1111/j.1365-246X.1987.tb01367.x.
- **_Creasy, N. M. (2020)_**. SplitLab version 1.3.0.
  available at https://github.com/nmcreasy/SplitLab1.3.0.
- **_GEOFON Data Centre (1993)_**. GEOFON (GeoForschungsNetz).
  Deutsches GeoForschungsZentrum (GFZ), Seismic Network.
  https://doi.org/10.14470/TR560404.
- **_GEOSCOPE (1982)_**. French Global Network of broad band seismic stations.
  Institut de physique du globe de Paris (IPGP) & Ecole et Observatoire des Sciences de la Terre de Strasbourg (EOST).
  https://doi.org/10.18715/GEOSCOPE.G.
- [**_Grund, M. (2017)_**](https://doi.org/10.1016/j.cageo.2017.04.015).
  StackSplit - a plugin for multi-event shear wave splitting analyses in SplitLab.
  *Computers & Geosciences*, volume 105, pages 43-50.
  https://doi.org/10.1016/j.cageo.2017.04.015.
  versions [1.0](https://doi.org/10.5281/zenodo.464385), [2.0](https://doi.org/10.5281/zenodo.7118716), and [3.0](https://doi.org/10.5281/zenodo.5802051)
  are available at https://github.com/michaelgrund/stacksplit.
- **_Porritt, R. W. (2014)_**. SplitLab version 1.2.1.
  available at https://robporritt.wordpress.com/software/.
- [**_Silver, P. G. & Chan, W. W. (1991)_**](https://doi.org/10.1029/91JB00899).
  Shear wave splitting and subcontinental mantle deformation.
  *Journal of Geophysical Research*, volume 96, issue B10, pages 16429-16454.
  https://doi.org/10.1029/91JB00899.
- [**_Walsh, E., Arnold, R. & Savage, M. K. (2013)_**](https://doi.org/10.1002/jgrb.50386).
  Silver and Chan revisited.
  *Journal of Geophysical Research: Solid Earth*, volume 118, issue 10, pages 5500-5515.
  https://doi.org/10.1002/jgrb.50386.
- [**_Wüstefeld, A., Bokelmann, G., Zaroli, C. & Barruol, G.  (2008)_**](https://doi.org/10.1016/j.cageo.2007.08.002).
  SplitLab: A shear-wave splitting environment in Matlab.
  *Computers & Geosciences*, volume 34, issue 5, pages 515-528.
  https://doi.org/10.1016/j.cageo.2007.08.002.
  version 1.0.5 **was** available at http://splitting.gm.univ-montp2.fr, version 1.9.0 is available at https://github.com/IPGP/splitlab.


## Funding

The presented research and YF received support from:

- Scholarship of the [Graduate Funding from the German States](https://www.khys.kit.edu/english/graduate_funding.php)
