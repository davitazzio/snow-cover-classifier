
# Snow Cover Classifier from Satellite Images
  ##### Project work on Data Mining M - Computer Engineering Master Program - University of Bologna
  
  \
  Student: Davide Tazzioli\
  `davide.tazzioli@studio.unibo.it`
  \
  \
**Version mismatch between code and project report:** _the use of __Support Vector Classifier__ and __Random Forest Classifier__ to train the model is not present in the report and is not include in final evaluation, because it was added to the project after the report redaction._

## Usage: 

Sentinel-hub data are not uploaded on github: to use the visualization web application is necessary to execute the whole code, including the images download.\ 
Ground truth data are available here: **(only people in University of Bologna)**\ https://liveunibo-my.sharepoint.com/:f:/g/personal/davide_tazzioli_studio_unibo_it/EjvXFvW31GRDjofT59b1NZQBpWclOEBas9A7Mf7V_aZ7Rw?e=dDXEnJ 

The original size report is available here: **(only people in University of Bologna)**\
https://liveunibo-my.sharepoint.com/:b:/g/personal/davide_tazzioli_studio_unibo_it/EZ21idXcF6hBm84vpWoLiJUBXgd8IUA5rPE31hGINeUcdQ?e=Usyik1


## Abstract: 
  This paper reports the work and the consequent consideration on a
  satellite images classifier, specified on the recognition and the
  monitoring of land snow cove. Satellite images are from Sentinel 2
  Satellite by ESA, made available on the Sentinel Hub Platform. For the
  images storage and pre-processing the library eo-learn is used. The
  classifier is trained and tested with different classifier, trying to
  obtain the best result in terms of efficiency, scalability, and
  precision and accuracy of the results. Land snow cover of an area and
  snow cover variation are important indicator for different environment
  aspect, used for useful consideration and prevision. With the work
  reported in this paper, a new algorithm is tested using images from
  the new European space program for the land monitoring. The resulting
  classification is finally visualized on the map of the area.

**Keywords:** Classification, Image Classification, Land Cover
Classification, Visualization

## Content

New technologies on airborne ground monitoring are offering lot of new
possibilities, even thanks to the development and cost reduction of
satellite technologies. A large-scale observation of the earth's
coverage with more and more detail of the elements and specific areas is
offered, and data are made almost immediately available thanks to the
new communication technologies. The potential of data collection tools,
however, must be supported by equally efficient information processing,
capable of managing large amounts of data, knowing how to extrapolate
relevant information and then delivering it in a timely manner for
proliferating use. Furthermore, a large variety of information from
different sensors allows us to obtain higher-level information that
takes into account not only the spatial location, but also the temporal
evolution. In this project we intend to apply machine learning
algorithms for the automatic classification of the soil, specific for
the detection of snow-covered areas. That information, stored over long
periods of time, can be used for statistical consideration or represent
the data for a higher elaboration, which can lead to significant
insight: the combination of precipitation, temperature and snow coverage
data, for instance, could forecast abnormal events on the flow of
rivers; information for the correct management of drinking water
reserves, starts from the information about the snow trend during the
winter; also agriculture can benefit of this information [1].

## Sentinel-Hub Project

Sentinel-2 is a space mission by ESA; it is part of the Copernicus
program, which intends to monitor the green areas of the planet and
provide support in the management of natural disasters. It consists of
two identical satellites, Sentinel-2A and Sentinel-2B
[2] It offers satellite images of the entire earth's
surface in the areas between the 84S and 84N meridians; their
multi-spectrum sensors offer information from visible light to infrared.
The resolution of the data allows a ground detail of 10, 20 and 60
meters depending on the spectrum band. The data is freely accessible
from the portal offered by the European space agency.

## EO-LEARN Project

eo-learn is a open-source project developed to seamlessly access and
process spatio-temporal image sequences acquired by any satellite.
Packages are written in Python and available on github: sharing and
collaboration is encouraged thank to the web site with instruction and
examples of projects. Lot of tasks and utilities are available and
tested, and continuously improved by the community: cloud masking, image
co-registration, feature extraction, classification, etc. Eo-learn
library acts as a bridge between Earth observation/Remote sensing field
and Python ecosystem for data science, machine learning and
visualization; it uses NumPy arrays to store and handle remote sensing
data [3].

## Machine Learning for soil classification

Research on the observation of the earth's soil with surveying
instruments installed on satellites, began in the second half of the 9th
century as a part of space exploration by America and Russia.
[4] Nowadays, sensors are specific and accurate,
and the work on the data collector software, allows us to have values
that are mostly not influenced by the atmosphere variations. In
particular, Sentinel 2 satellite acquires data in a period of
observation between 17 and 32 minutes, creating a single interpolated
map of the area. Bands of the Multispectral sensor are referred to the
visible light and to the infrared:

    **Sentinel-2 bands**         **usage**         **Central wavelength**   **Bandwidth**   **Spatial resolution**
  ---------------------- ----------------------- ------------------------ --------------- ------------------------
       `Band 01`` `         *Coastal aerosol*           442.2 *nm*            21 *nm*              60 *m*
       `Band 02`` `              *Blue*                 492.1 *nm*            66 *nm*              10 *m*
       `Band 03`` `              *Green*                559.0 *nm*            36 *nm*              10 *m*
       `Band 04`` `               *Red*                 664.9 *nm*            31 *nm*              10 *m*
       `Band 05`` `       *Vegetation red edge*         703.8 *nm*            16 *nm*              20 *m*
       `Band 06`` `       *Vegetation red edge*         739.1 *nm*            15 *nm*              20 *m*
       `Band 07`` `       *Vegetation red edge*         779.7 *nm*            20 *nm*              20 *m*
       `Band 08`` `               *NIR*                 832.9 *nm*           106 *nm*              10 *m*
      `Band 08A`` `           *Narrow NIR*              864.0 *nm*            22 *nm*              20 *m*
       `Band 09`` `          *Water vapour*             943.2 *nm*            21 *nm*              60 *m*
       `Band 10`` `         *SWIR -- Cirrus*           1376.9 *nm*            30 *nm*              60 *m*
       `Band 11`` `              *SWIR*                1610.4 *nm*            94 *nm*              20 *m*
       `Band 12`` `              *SWIR*                2185.7 *nm*           185 *nm*              20 *m*

  : Band specifics captured by multyspectral instruments on *Sentinel
  II* Satellites

Over the year some parameters have been studied using earth knowledge,
observation on the ground and machine learning. Among the most used
parameters:

-   **NDVI** *(Normalized difference vegetation index)*: Live green
    plants absorb solar radiation during the photosynthesis process; at
    the same time leaf cells re-emit solar radiation in the
    near-infrared spectral region. Analyzing the re-emitted infrared and
    near-infrared spectral region you can conclude information about the
    presence of vegetation in each area. The index is calculated
    normalizing the difference between the spectral reflectance
    measurements acquired in the red (visible) and near-infrared
    regions.

-   **NDWI** *(Normalized Difference Water Index)*: it is derived from
    the *Near-Infrared* (NIR) and *Short-Wave Infrared* (SWIR) channels.
    The SWIR reflectance reflects changes in both the vegetation water
    content and the spongy mesophyll structure in vegetation canopies,
    while the NIR reflectance is affected by leaf internal structure and
    leaf dry matter content but not by water content. The combination of
    the NIR with the SWIR removes variations induced by leaf internal
    structure and leaf dry matter content, improving the accuracy in
    retrieving the vegetation water content.

-   **NDBI** *(Normalized Difference Built-Up Index)*: This index
    highlights urban areas where there is typically a higher reflectance
    in the *shortwave-infrared* (SWIR) region, compared to the
    *near-infrared* (NIR) region.

-   **NDSI** *(Normalized-Difference Snow Index)*: NDSI is a measure of
    the relative magnitude of the reflectance difference between
    *visible* (green) and *shortwave infrared* (SWIR).

The last index is often used to classify snow coverage from satellite
images, just applying different thresholds. *NASA portal for earth
observation* [5] offers maps of the whole globe on different
aspects registered by the sensors on their satellites. The snow
monitoring portal, indeed, offers maps of the only NDSI pure index, and
maps of a simple classification based on this index. The threshold value
between *snow* and *not-snow* depends by the algorithm. The ground-truth
values used in this project to train the classification model and to
test it, are made starting from NDSI index obtained by NASA satellite,
then manually merged and validated with values obtained from ground
station widespread in northern Italy mountains. Snow coverage automatic
classification of the soil is a field already studied also using
satellite images; high level information are usually obtained by the
manually work of earth scientists also on the data from NASA and ESA.
Automatic classification can be useful to obtain data on the whole globe
and have fast statistic information. Higher level usage of those
information still requires expert intervention. The project aim is not
only the evaluation of the results, but also having consideration on the
machine learning algorithm: for this reason, NDSI index will not be used
for the model training, but only the bands used to calculate it.

## Tools and Environment

The project is developed using the programming language Python, compiled
by the software Python 3.10; code is organised in different parts, and
result are obtained working with the Jupiter Notebook Environment. Data
are elaborated by EO-Learn data structure, that are based on Nunmpy
Arrays, while the machine learining tools are made available by
SciKit-Learn libraries. Data Visualization, finally, uses MatPlotLib
functions and the library Bokeh for graphs and interaction.\

## Satellite data

Satellite images are available on the Sentinel-Hub portal after
registration; data are automatically collect by a client previusly
configurated. The area of interest of this project is located in the
north of Italy on the Appennini's mountain, with a focus on the Bologna
and Modena's district: a restricted area of interest meets the
limitation imposed by Sentinel Hub portal on the download of data.


## Ground truth Data

Ground truth data are obtained by the validation work of NASA maps
[6]: from NASA satellite data NDSI map is calculated thought a
validation work using ground station values, a specific threshold is
calculated to distinguish snow areas, iced cloud and areas without
snow.\


## Future project

Besides the low quality of the results, snow cover monitoring remains a
usefull and full of potential activity. The machine learining approach
on data satellite images, allows a low cost global monitoring on lare
time intervals: the potential insight we can obtain are multiple, with a
huge social impact. This project, in particular, can be easily improved
and made more powerful using a larger dataset, with a more balanced data
of snow and not-snow in space and time. The requested amount of data
requires an higher computational power, and a larger data exchange: for
a better performance and for avoinding the overhead for data
downloading, the application with the machine learining training phase
should be ported on a cloud application. Finally, a more interactive
data visualization application can be easily obtained, eventualy
integrating a web client to automatically obtain data from cloud.

# References 

[1]  High resolution snow and ice monitoring. (n.d.). https://land.copernicus.eu/pan-european/biophysical-parameters/high-resolution-snow-and-ice-monitoring. \
[2]  Wikipedia Contributors. (2022). Sentinel-2 — Wikipedia, the free encyclopedia. https://en.wikipedia.org/w/index.php?title=Sentinel-2&oldid=1105470108. ([Online; accessed 19-September- 2022]) \
[3]  Eo-learn Contributors. (2018). Introduction – eo-learn documentation. https://eo-learn.readthedocs.io/en/latest/index.html#introduction. \
[4]  Lubej, M. (2018). Land cover classification with eo-learn: Part 1. Sentinel Hub Blog. \
[5]  Earth observatory. (n.d.). https://earthobservatory.nasa.gov. \
[6]  Magnani, C. (2022). Sviluppo e validazione di mappe di copertura nevosa per lo studio di variabilit`a del
manto nevoso in emilia romagna nel periodo 2000-2020.

