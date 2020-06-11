# NEUBIAS-webinar

## Slides, resource links and custom datasets used in part 1 of the NEUBIAS@Home SMLM analysis webinar on 11 June 2020.
### Resources for part 2 of the webinar (quantification) can be found at: https://github.com/flevet/NEUBIAS_Academy

Slides can be viewed by clicking on **'A guided tour for analyzing and quantifying single-molecule_short.pdf'** in the panel above.

Custom datasets can be found as a .zip file by clicking the button above that says **'1 release'**

References, resources, datasets etc in the slides can be found below (or downloadable as a separate document, [here](https://docs.google.com/document/d/1qKyD3cJ5J0hcffg0PhAqYuvTkEznieeUOpgUnQzg9y4/edit?usp=sharing
)).

### Resources and references

**Slide 3**

Simulated NEUBIAS logo dataset is available at: https://github.com/superresolusian/NEUBIAS-webinar/releases/tag/webinar-data (logo_blinks_16bit), created using custom simulation plugin available at https://github.com/superresolusian/mypluginsbaby/releases/tag/neubias2019



**Slide 4**

Low density dataset = http://bigwww.epfl.ch/smlm/datasets/index.html?p=tubulin-af647

High density dataset = http://bigwww.epfl.ch/smlm/datasets/index.html?p=../challenge2013/datasets/Real_High_Density



**Slide 5**

Ovesný et al (2014): Martin Ovesný, Pavel Křížek, Josef Borkovec, Zdeněk Švindrych, Guy M. Hagen, ThunderSTORM: a comprehensive ImageJ plug-in for PALM and STORM data analysis and super-resolution imaging, Bioinformatics, Volume 30, Issue 16, 15 August 2014, Pages 2389–2390, https://doi.org/10.1093/bioinformatics/btu202 

ThunderSTORM Github: https://github.com/zitmen/thunderstorm

Landing page for Single Molecule Localization Microscopy Software Benchmarking: http://bigwww.epfl.ch/smlm/index.html#&panel1-2

Sage et al (2019): Sage, D., Pham, T., Babcock, H. et al. Super-resolution fight club: assessment of 2D and 3D single-molecule localization microscopy software. Nat Methods 16, 387–395 (2019). https://doi.org/10.1038/s41592-019-0364-4 



**Low-density demo**

Low density dataset (+ synthetic drift):
https://github.com/superresolusian/NEUBIAS-webinar/releases/tag/webinar-data (low-density_tublin-af647_synthetic-drift)

Perceptually uniform colormaps: https://peterkovesi.com/projects/colourmaps/ - Downloadable as a .zip file for ImageJ - the one I use in the demo is the catchily-named “CET-L3.lut” (perceptually uniform red-hot). You can get this into your Fiji LUT menu by copying the .lut file into the ‘luts’ folder within Fiji and restarting the software.



**High-density demo**

High density dataset:
http://bigwww.epfl.ch/smlm/datasets/index.html?p=../challenge2013/datasets/Real_High_Density



**Slide 10**

Batch processing macros for ThunderSTORM: https://jalink-lab.github.io/



**Slide 12**

Marsh et al (2018): Marsh, R.J., Pfisterer, K., Bennett, P. et al. Artifact-free high-density localization microscopy analysis. Nat Methods 15, 689–692 (2018). https://doi.org/10.1038/s41592-018-0072-5

HAWK Fiji plugin download: www.coxphysics.com



**Slide 13**

SOFI - Dertinger et al (2009): Fast, background-free, 3D super-resolution optical fluctuation imaging (SOFI). T. Dertinger, R. Colyer, G. Iyer, S. Weiss, J. Enderlein
Proceedings of the National Academy of Sciences Dec 2009, 106 (52) 22287-22292; https://doi.org/10.1073/pnas.0907866106 

SRRF - Gustafsson et al (2016): Gustafsson, N., Culley, S., Ashdown, G. et al. Fast live-cell conventional fluorophore nanoscopy with ImageJ through super-resolution radial fluctuations. Nat Commun 7, 12471 (2016). https://doi.org/10.1038/ncomms12471 



**Slide 15**

SQUIRREL: Culley, S., Albrecht, D., Jacobs, C. et al. Quantitative mapping and minimization of super-resolution optical imaging artifacts. Nat Methods 15, 263–266 (2018). https://doi.org/10.1038/nmeth.4605 

GPU-independent error mapping download: https://github.com/superresolusian/mypluginsbaby/releases/tag/nogpu2019 - To install, download the .jar file in the release and then copy it into the ‘plugins’ folder of your Fiji install.



**SQUIRREL demo**

Reference and super-resolution images (generated from high density dataset): https://github.com/superresolusian/NEUBIAS-webinar/releases/tag/webinar-data (squirrel)



**Slide 16**

Bead PSF stacks available at: http://bigwww.epfl.ch/smlm/challenge2016/datasets/Beads/Data/data.html
(3D quad-plane not shown in slideshow)



**3D demo**

3D astigmatism calibration bead data from: http://bigwww.epfl.ch/smlm/challenge2016/datasets/Beads/Data/data.html
(3D Astigmatism)

3D simulated microtubule imaging data:
http://bigwww.epfl.ch/smlm/challenge2016/datasets/MT1.N1.LD/Data/data.html
(3D Astigmatism)



**Slide 17**

3D fitting with SMAP: Li, Y., Mund, M., Hoess, P. et al. Real-time 3D single-molecule localization using experimental point spread functions. Nat Methods 15, 367–369 (2018). https://doi.org/10.1038/nmeth.4661

SMAP software: https://rieslab.de/#software - Can be downloaded as a standalone package (you may be prompted to install MATLAB compiler as a necessary part of this, beware that this is quite a large download) or run directly through MATLAB.
