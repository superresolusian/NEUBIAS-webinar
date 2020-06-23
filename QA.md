# Table of contents
* [General SMLM acquisition and analysis](#generalSMLM)
  * [How does the frame rate affect the final image?](#timescale)
  * [What is the dimensionality of the test data used in the webinar?](#testdata)
  * [How do you know if your data is high or low density?](#highlowdensity)
  * [Why not always use multi-emitter fitting, even for sparse data?](#multiemitter1)
  * [How do you acquire calibration data for 3D imaging?](#calibration)
  * [Where can I learn more about image filtering and spot detection?](#filteringdetection)
* [ThunderSTORM-specific questions](#thunderstorm)
  * [What computer specs are needed to run ThunderSTORM?](#thunderstormspecs)
  * [What is a 'good' uncertainty value?](#uncertainty)
  * [How does the ThunderSTORM drift correction work?](#driftcorrection)
  * [How does ThunderSTORM multi-emitter fitting choose between e.g. one bright molecule and two dim molecules close together?](#multiemitter2)
  * [How do you analyse multi-colour SMLM data?](#chromatic)
* [SQUIRREL-specific questions](#squirrel)
  * [How should SQUIRREL error maps be interpreted?](#errormap)
  * [Can SQUIRREL be used to do colocalization analysis?](#colocalization)
* [Cluster analysis](#tesseler)
  * [Why is a Voronoi diagram preferable to Delaunay triangulation?](#delaunay)
  * [How does cluster shape affect cluster analysis?](#shape)
  * [How does polygon area affect cluster analysis in SR-Tesseler?](#polygonarea)
  * [Can you use Voronoi methods on top of DBSCAN results?](#dbscan)
  * [When will 3D SR-Tesseler be available?](#3dtesseler)
  * [What are the computer specs for 3D Tesseler analysis?](#tesselerspecs)
  

# General SMLM acquisition and analysis <a name="generalSMLM"></a>

## How does the timescale in between frames matter in producing the super-resolved image? <a name="timescale"></a>
Here, it is more a question of the acquisition setup. The frame rate is a tradeoff between the number of blinking emitters that appear in one frame and the total time of the experiment. Usually, we want to keep a low density of emitters in frame to avoid overlapping, and at the same time we want to collect a large number of blinking spots to best reconstruct the structure.

The ideal frame rate will also depend on the identity of the fluorophore being used to label the sample, the interaction of this fluorophore with the buffer being used, and the laser intensity. Important parameters to consider are the brightness of a blinking event and the kinetics of the transitions between ‘on’ and ‘off’ states.

As a general rule (for fixed samples) you want to image as fast as possible (to minimise overlapping) without losing too many photons from each blink event (as localization uncertainty is inversely proportional to blink intensity).

## Is this tubulin data acquired in a single plane? And it’s a 2D data set right? [[dataset in question]](http://bigwww.epfl.ch/smlm/datasets/index.html?p=tubulin-conjal647) <a name="testdata"></a>
These tubulins live in a 3D world, but yes, here, the SMLM modality is 2D, we can not recover the Z position. SMLM acquisition is performed overwhelmingly in widefield or TIRF modalities; the latter will enable a small focal depth but at the cost of being constrained to imaging structures near the coverslip.
Recovering axial information via SMLM requires additional optics to break the axial symmetry of the PSF (e.g. using a cylindrical lens to introduce astigmatism, two relatively defocused detection paths for biplane imaging, or a phase mask to engineer a double helix-shaped PSF). In general, the depth over which these axial localization techniques are effective is <5 microns.

## What is the cut-off between low and high density data? <a name="highlowdensity"></a>
There is no hard cut off between low and high density data, and often a single dataset may contain regions that are of different densities. There is an animation available [here](https://twitter.com/SuperResoluSian/status/1273654948174221316) showing a continuum of increasing data density and the effect on detected molecules.

## When an image is borderline between high and low density, is there a problem to use the multi emitter fitting in these datasets? In other words, besides time, is there a downside to use multi emitter mode in sparsely dense datasets? <a name="multiemitter1"></a>
The other downside to using multi emitter fitting, other than time, is that you may get over-fitting of your localizations. For example, one true single molecule may end up being fitted by two Gaussians a very small distance (e.g. 5nm) apart. This would be especially problematic for molecule counting/stoichiometry. This problem can be somewhat ‘fixed’ in ThunderSTORM using the ‘Remove duplicates’ tab, whereby you can filter out molecules within the same frame that are closer together than a user-defined threshold (e.g. uncertainty_xy, to filter molecules that are within the error of each other within a frame). However, I still recommend keeping the analysis as straightforward as possible for sparse data to avoid introducing additional uncertainties arising from filtering etc.

## For the (3D) calibration, what is a good product/approach DNA rulers, beads, etc? <a name="calibration"></a>
Sub-resolution multi-colored beads like Tetraspeck beads (0.1 micrometer) are ideal for this purpose. DNA rulers should work as well. The major considerations are that the objects are well-separated, and they do not photobleach or move during the calibration acquisition.

## The 1st talk of this seminar was more focused on localization than on detection. What is the best source to learn about image filtering and detection? <a name="filteringdetection"></a>
For the filtering and detection specific to ThunderSTORM, the supplementary information of the paper has thorough explanations, and also the blue question marks next to the options in the GUI. Also exploring different options using the 'Preview' button of the ThunderSTORM GUI can be quite educational. For a general primer on image filtering, [this might be a useful video](https://www.youtube.com/watch?v=LT8L3vSLQ2Q). Detection is almost always done via a 'local maximum' search over the image. For context, this is fairly similar to what happens within e.g. Fiji's native Process>Find Maxima... function.

# Running ThunderSTORM analysis <a name="thunderstorm"></a>

## Can you say something about how computer specs affect the processing? <a name="thunderstormspecs"></a>
That depends on the program and algorithm that you use. ThunderSTORM uses all CPU cores, so the more the better. Quality should be the same regardless of computer specs. Settings that greatly affect the processing time are multi-emitter fitting, and using Maximum Likelihood instead of (Weighted) Gaussian fit. The example analysis in the webinar was run on a Microsoft Surface Book laptop with inbuilt i7-8650U CPU processor.

## What is a “good” value in the uncertainty column? <a name="uncertainty"></a>
That depends very much on the quality of the acquisition, blinking properties of the fluorophores, density of emitters per frame, size of PSF, level of background noise.... ‘Good’ localizations tend to have uncertainties <20nm, and ideally the histogram of uncertainty values should be symmetrically distributed in a peak around this region. The longer and stronger the tail of the distribution of this histogram of uncertainties, and the more shifted it is towards higher values, the worst the localizations are. Exploring different filters for uncertainty values within some test data can help you get a feel for what is ‘good’.

## What images are cross-correlated to perform drift correction? Final renderings that are made from only the subset of frames? <a name="driftcorrection"></a>
ThunderSTORM generates a series of 'super-resolved images' with low magnification from subsets of frames of size (total number of frames / number of bins). These images are cross-correlated to calculate the drift.
Further information can be found by pressing the blue question mark button in the ‘Drift correction’ tab; the original paper describing this method, upon which the ThunderSTORM analysis is based can be found [here](https://doi.org/10.1364/OE.19.015009)

## With High density data, you get some "fat Gaussian"s but I guess you also get good Gaussians but that are really intense (multiple emitter) if the 2 source points are really close to each other. Does the multi emitter fitting also correct for this? <a name="multiemitter2"></a>
In high density, the probability of overlapping is becoming high. Of course, the localization algorithms have a hard time distinguishing overlapping emitters. In this case, some software have multiple-fitting methods to try to solve the overlapping, like ThunderSTORM. The multiple emitter fitting within ThunderSTORM runs an appropriate statistical test (depending on whether least squares fitting or maximum likelihood estimation was used) to determine between cases such as described in the question. For the specific question of intensity, there are options within the multi emitter fitting analysis fitting panel of ThunderSTORM for forcing all molecules to have the same intensity, or to limit the number of photons permissible from a single molecule. Detailed information on this, and references therein, can be found by clicking the blue question mark button in the ‘Sub-pixel localization of molecules’ panel of ThunderSTORM and following the link to ‘Multiple-emitter fitting analysis’.

Other software have integrated other methods to solve the overlapping, like DAOSTORM (detect one and remove) or FALCON (links to these software packages and papers available [here](http://bigwww.epfl.ch/smlm/software/index.html)). You can also preprocess the data using [HAWK](https://doi.org/10.1038/s41592-018-0072-5).

## Is analyzing two-color images the same as one-color with ThunderStorm? Is it possible to share some chromatic correction fiji plugin/algorithms for dual color STORM imaging before feeding into cluster analysis? <a name="chromatic"></a>
ThunderSTORM doesn't support multi-color images. You should just process the images sequentially, and merge the channels afterwards in Fiji. If you need to correct for chromatic aberrations between the colors (in most cases you do), you can find our [Bram’s] solution [here](https://jalink-lab.github.io/). This uses an affine transformation to transform localizations of one color onto another color. To construct the matrices for these transformations you need to image multicolor beads and create a table with matching positions of these beads. More information can be found [here](https://jalink-lab.github.io/). 

(Small disclaimer: for now our solution is a bit limited, in the sense that a few things are still hardcoded, and may not work in your particular case. Work is in progress to make the plugin more general!)

# SQUIRREL analysis <a name="squirrel"></a>

## Can SQUIRREL be used to check for artifacts after deconvolution of ordinary widefield/confocal data? And if yes, how do I read the resulting error maps, i.e. what is a "High" error and what is a "low" error? <a name="errormap"></a>
Yes, SQUIRREL can be used to check for artefacts in any image where a higher-confidence (but lower resolution) image of the same region is available. The error maps made by SQUIRREL are mainly designed to highlight areas that may contain errors, and thus they are more relative measures within the context of the image rather than values that correspond to objectively ‘good’ or ‘bad’. The error maps produced by SQUIRREL are the absolute value of the difference between the true reference (widefield, confocal etc) image and a convolved version of the super-resolution image; therefore they display errors on the same intensity scale as the original reference image. It can be quite intuitive to resize the reference image to be the same size as the error maps, then use Process>Image Calculator to divide the error map by the resized reference image. This will normalize the values in the error map to show how large the error was relative to the original intensity.

## Can this algorithm [SQUIRREL] be used as a basis for the colocalization analysis? Basically, to detect single-molecule colocalizations? <a name="colocalization"></a>
I have never tried this before, but in principle it could work, especially if one channel had a different resolution to the other. However, there are more elegant solutions for SMLM colocalization analysis - indeed, Florian recently published a version of SR-Tesseler that performs colocalization analysis (available [here](https://doi.org/10.1038/s41467-019-10007-4)).

# Cluster analysis of SMLM data <a name="tesseler"></a>

## Since the Voronoi is the dual of Delaunay triangulation, can we not formulate the same methods with the Delaunay graph? <a name="delaunay"></a>
It’s indeed certainly possible to formulate the same method for Delaunay triangulation. Still, I don’t think this is as straightforward as it seems: for Tesseler we are using the density at rank 1, i.e. by using the direct neighbors. For Delaunay triangulation, one would need to define the neighborhood: will it be the direct neighbors of the triangle (then 3 triangles) or of the triangle’s vertices (then n triangles)? When using rank 0, I would think that “normalizing” the triangles by a distribution of the average area of the triangles may work.

## Do the clustering techniques shown (and in particular Voronoi) work with non circular shapes? <a name="shape"></a>
Clustering techniques (K-Ripley, Pair correlation, …) usually compute some kind of density using a radius, and then report an aggregation size. They therefore don’t cope very well with non-circular clusters.
Segmentation techniques on the other hand (DBSCAN, Voronoi, …) don’t assume any (circular) shape for the objects/clusters they segment.


## What happens to the localizations that are spatially located near to a cluster BUT have a large polygon area? Would they be counted as “part of the cluster” or “not part of the cluster”? <a name="polygonarea"></a>
It depends on the experimental data you have. If the clusters are well separated (with low background), the polygons in the clusters’ border will indeed have a big area and the odds are that they will be discarded from the clusters when applying the threshold. In this case, one solution is to use a cutting distance (as in for the Delaunay triangulation) instead of a density-based threshold.
In the case where the background density is higher, the border polygons will be smaller and therefore they may still be kept in the segmented clusters.

## So, I have seen DBSCAN used to preanalyze data to attribute a group of localizations to a single emitter, can you use previously processed DBSCAN data for the Voronoi analysis or should this technique be performed on the original data? <a name="dbscan"></a>
Yes, why not! but remember that DBSCAN is really dependent on the 2 hard parameters as was shown by Florian in the webinar. You will have to properly choose these 2 parameters.

## [SR-Tesseler in 3D] looks great. And would be really useful. When will this become available? <a name="3dtesseler"></a>
Hopefully, in a few months.

## Are there specific requirements/recommendations for computing hardware to run 3D segmentation using SR Tesseler? <a name="tesselerspecs"></a>
A NVidia card will be needed as CUDA is used for the 3D Voronoi generation.
