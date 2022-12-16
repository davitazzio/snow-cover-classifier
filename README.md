<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"  
  "http://www.w3.org/TR/html4/loose.dtd">  
<html > 
<head><title>Snow cover classifier using satellite images</title> 
<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1"> 
<meta name="generator" content="TeX4ht (https://tug.org/tex4ht/)"> 
<meta name="originator" content="TeX4ht (https://tug.org/tex4ht/)"> 
<!-- html --> 
<meta name="src" content="main.tex"> 
<link rel="stylesheet" type="text/css" href="main.css"> 
</head><body 
>
   <div class="maketitle">
                                                                                       
                                                                                       
                                                                                       
                                                                                       

<h2 class="titleHead">Snow cover classifier using satellite images</h2>
    <div class="author" ><span 
class="cmr-12">Project work on Data Mining M</span>
<br /><span 
class="cmr-12">Computer Engineering Master Program</span>
<br />         <span 
class="cmr-12">Prof. Claudio Sartori</span>
<br />         <span 
class="cmr-12">University of Bologna</span>
<br />         
<br />                <span 
class="cmr-9">Student</span>
<br />            <span 
class="cmr-12">Davide Tazzioli</span>
<br />      <span 
class="cmtt-9">davide.tazzioli@studio.unibo.it</span><br /><br /></div><br />
<div class="date" ></div>
   </div>
   <div 
class="abstract" 
>
   <h3 class="abstracttitle">
<span 
class="cmbx-9">Abstract</span>
</h3>
     <!--l. 51--><p class="noindent" ><span 
class="cmr-9">This paper reports the work and the consequent consideration on a satellite images classifier, specified</span>
     <span 
class="cmr-9">on the recognition and the monitoring of land snow cove. Satellite images are from Sentinel 2 Satellite</span>
     <span 
class="cmr-9">by ESA, made available on the Sentinel Hub Platform. For the images storage and pre-processing the</span>
     <span 
class="cmr-9">library eo-learn is used. The classifier is trained and tested with different classifier, trying to obtain</span>
     <span 
class="cmr-9">the best result in terms of efficiency, scalability, and precision and accuracy of the results. Land snow</span>
     <span 
class="cmr-9">cover of an area and snow cover variation are important indicator for different environment aspect,</span>
     <span 
class="cmr-9">used for useful consideration and prevision. With the work reported in this paper, a new algorithm</span>
     <span 
class="cmr-9">is tested using images from the new European space program for the land monitoring. The resulting</span>
     <span 
class="cmr-9">classification is finally visualized on the map of the area.</span>
</div>
<!--l. 63--><p class="noindent" ><span 
class="cmbx-9">Keywords: </span><span 
class="cmr-9">Classification, Image Classification, Land Cover Classification, Visualization  </span><br 
class="newline" />
   <h3 class="sectionHead"><span class="titlemark"><span 
class="cmr-9">1   </span></span> <a 
 id="x1-10001"></a><span 
class="cmr-9">Content</span></h3>
<!--l. 68--><p class="noindent" ><span 
class="cmr-9">New technologies on airborne ground monitoring are offering lot of new possibilities, even thanks to the development and</span>
<span 
class="cmr-9">cost reduction of satellite technologies. A large-scale observation of the earth&#8217;s coverage with more and more detail of the</span>
<span 
class="cmr-9">elements and specific areas is offered, and data are made almost immediately available thanks to the new communication</span>
<span 
class="cmr-9">technologies. The potential of data collection tools, however, must be supported by equally efficient information</span>
<span 
class="cmr-9">processing, capable of managing large amounts of data, knowing how to extrapolate relevant information and then</span>
<span 
class="cmr-9">delivering it in a timely manner for proliferating use. Furthermore, a large variety of information from different sensors</span>
<span 
class="cmr-9">allows us to obtain higher-level information that takes into account not only the spatial location, but also the temporal</span>
<span 
class="cmr-9">evolution. In this project we intend to apply machine learning algorithms for the automatic classification of the soil,</span>
<span 
class="cmr-9">specific for the detection of snow-covered areas. That information, stored over long periods of time, can be used for</span>
<span 
class="cmr-9">statistical consideration or represent the data for a higher elaboration, which can lead to significant insight: the</span>
<span 
class="cmr-9">combination of precipitation, temperature and snow coverage data, for instance, could forecast abnormal</span>
<span 
class="cmr-9">events on the flow of rivers; information for the correct management of drinking water reserves, starts from</span>
<span 
class="cmr-9">the information about the snow trend during the winter; also agriculture can benefit of this information</span>
<span 
class="cmr-9">(</span><span 
class="cmbx-9">?</span><span 
class="cmr-9">).</span>
                                                                                       
                                                                                       
<!--l. 84--><p class="noindent" >
   <h4 class="subsectionHead"><span class="titlemark"><span 
class="cmr-9">1.1   </span></span> <a 
 id="x1-20001.1"></a><span 
class="cmr-9">Sentinel-Hub Project</span></h4>
<!--l. 85--><p class="noindent" ><span 
class="cmr-9">Sentinel-2 is a space mission by ESA; it is part of the Copernicus program, which intends to monitor the green areas of</span>
<span 
class="cmr-9">the planet and provide support in the management of natural disasters. It consists of two identical satellites, Sentinel-2A</span>
<span 
class="cmr-9">and Sentinel-2B (</span><span 
class="cmbx-9">?</span><span 
class="cmr-9">) It offers satellite images of the entire earth&#8217;s surface in the areas between the 84S and 84N meridians;</span>
<span 
class="cmr-9">their multi-spectrum sensors offer information from visible light to infrared. The resolution of the data allows a ground</span>
<span 
class="cmr-9">detail of 10, 20 and 60 meters depending on the spectrum band. The data is freely accessible from the portal offered by</span>
<span 
class="cmr-9">the European space agency.</span>
<!--l. 93--><p class="noindent" >
   <h4 class="subsectionHead"><span class="titlemark"><span 
class="cmr-9">1.2   </span></span> <a 
 id="x1-30001.2"></a><span 
class="cmr-9">EO-LEARN Project</span></h4>
<!--l. 94--><p class="noindent" ><span 
class="cmr-9">eo-learn is a open-source project developed to seamlessly access and process spatio-temporal image sequences acquired by</span>
<span 
class="cmr-9">any satellite. Packages are written in Python and available on github: sharing and collaboration is encouraged thank to</span>
<span 
class="cmr-9">the web site with instruction and examples of projects. Lot of tasks and utilities are available and tested, and</span>
<span 
class="cmr-9">continuously improved by the community: cloud masking, image co-registration, feature extraction, classification, etc.</span>
<span 
class="cmr-9">Eo-learn library acts as a bridge between Earth observation/Remote sensing field and Python ecosystem for data</span>
<span 
class="cmr-9">science, machine learning and visualization; it uses NumPy arrays to store and handle remote sensing data</span>
<span 
class="cmr-9">(</span><span 
class="cmbx-9">?</span><span 
class="cmr-9">).</span>
<!--l. 100--><p class="noindent" >
   <h4 class="subsectionHead"><span class="titlemark"><span 
class="cmr-9">1.3   </span></span> <a 
 id="x1-40001.3"></a><span 
class="cmr-9">Machine Learning for soil classification</span></h4>
<!--l. 101--><p class="noindent" ><span 
class="cmr-9">Research on the observation of the earth&#8217;s soil with surveying instruments installed on satellites, began in the second half</span>
<span 
class="cmr-9">of the 9th century as a part of space exploration by America and Russia. (</span><span 
class="cmbx-9">?</span><span 
class="cmr-9">) Nowadays, sensors are specific and accurate,</span>
<span 
class="cmr-9">and the work on the data collector software, allows us to have values that are mostly not influenced by the atmosphere</span>
<span 
class="cmr-9">variations. In particular, Sentinel 2 satellite acquires data in a period of observation between 17 and 32 minutes, creating</span>
<span 
class="cmr-9">a single interpolated map of the area. Bands of the Multispectral sensor are referred to the visible light and to the</span>
<span 
class="cmr-9">infrared (</span><span 
class="cmbx-9">?</span><span 
class="cmr-9">): </span><div class="table">
                                                                                       
                                                                                       
<!--l. 105--><p class="indent" >   <a 
 id="x1-4001r1"></a><hr class="float"><div class="float" 
>
                                                                                       
                                                                                       
 <div class="caption" 
><span class="id">Table&#x00A0;1: </span><span  
class="content">Band specifics captured by multyspectral instruments on <span 
class="cmti-10">Sentinel II </span>Satellites</span></div><!--tex4ht:label?: x1-4001r1 -->
<div class="tabular"> <table id="TBL-2" class="tabular" 
 
><colgroup id="TBL-2-1g"><col 
id="TBL-2-1"><col 
id="TBL-2-2"><col 
id="TBL-2-3"><col 
id="TBL-2-4"><col 
id="TBL-2-5"></colgroup><tr 
class="hline"><td><hr></td><td><hr></td><td><hr></td><td><hr></td><td><hr></td></tr><tr  
 style="vertical-align:baseline;" id="TBL-2-1-"><td  style="white-space:nowrap; text-align:center;" id="TBL-2-1-1"  
class="td11"><span 
class="cmbx-10">Sentinel-2 bands</span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-1-2"  
class="td11">     <span 
class="cmbx-10">usage       </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-1-3"  
class="td11"><span 
class="cmbx-10">Central wavelength</span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-1-4"  
class="td11"><span 
class="cmbx-10">Bandwidth</span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-1-5"  
class="td11"><span 
class="cmbx-10">Spatial resolution</span></td>
</tr><tr 
class="hline"><td><hr></td><td><hr></td><td><hr></td><td><hr></td><td><hr></td></tr><tr  
 style="vertical-align:baseline;" id="TBL-2-2-"><td  style="white-space:nowrap; text-align:center;" id="TBL-2-2-1"  
class="td11">     <span 
class="cmtt-10">Band 01     </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-2-2"  
class="td11">  <span 
class="cmti-10">Coastal aerosol   </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-2-3"  
class="td11">     442.2 <span 
class="cmti-10">nm        </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-2-4"  
class="td11">   21 <span 
class="cmti-10">nm    </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-2-5"  
class="td11">      60 <span 
class="cmti-10">m         </span></td></tr><tr  
 style="vertical-align:baseline;" id="TBL-2-3-"><td  style="white-space:nowrap; text-align:center;" id="TBL-2-3-1"  
class="td11"> <span 
class="cmtt-10">Band 02 </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-3-2"  
class="td11"> <span 
class="cmti-10">Blue </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-3-3"  
class="td11"> 492.1 <span 
class="cmti-10">nm </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-3-4"  
class="td11"> 66 <span 
class="cmti-10">nm </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-3-5"  
class="td11"> 10 <span 
class="cmti-10">m</span></td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-4-"><td  style="white-space:nowrap; text-align:center;" id="TBL-2-4-1"  
class="td11">     <span 
class="cmtt-10">Band 03     </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-4-2"  
class="td11">      <span 
class="cmti-10">Green        </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-4-3"  
class="td11">     559.0 <span 
class="cmti-10">nm        </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-4-4"  
class="td11">   36 <span 
class="cmti-10">nm    </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-4-5"  
class="td11">      10 <span 
class="cmti-10">m         </span></td></tr><tr  
 style="vertical-align:baseline;" id="TBL-2-5-"><td  style="white-space:nowrap; text-align:center;" id="TBL-2-5-1"  
class="td11"> <span 
class="cmtt-10">Band 04 </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-5-2"  
class="td11"> <span 
class="cmti-10">Red </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-5-3"  
class="td11"> 664.9 <span 
class="cmti-10">nm </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-5-4"  
class="td11"> 31 <span 
class="cmti-10">nm </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-5-5"  
class="td11"> 10 <span 
class="cmti-10">m</span></td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-6-"><td  style="white-space:nowrap; text-align:center;" id="TBL-2-6-1"  
class="td11">     <span 
class="cmtt-10">Band 05     </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-6-2"  
class="td11"><span 
class="cmti-10">Vegetation red edge</span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-6-3"  
class="td11">     703.8 <span 
class="cmti-10">nm        </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-6-4"  
class="td11">   16 <span 
class="cmti-10">nm    </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-6-5"  
class="td11">      20 <span 
class="cmti-10">m         </span></td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-7-"><td  style="white-space:nowrap; text-align:center;" id="TBL-2-7-1"  
class="td11">     <span 
class="cmtt-10">Band 06     </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-7-2"  
class="td11"><span 
class="cmti-10">Vegetation red edge</span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-7-3"  
class="td11">     739.1 <span 
class="cmti-10">nm        </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-7-4"  
class="td11">   15 <span 
class="cmti-10">nm    </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-7-5"  
class="td11">      20 <span 
class="cmti-10">m         </span></td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-8-"><td  style="white-space:nowrap; text-align:center;" id="TBL-2-8-1"  
class="td11">     <span 
class="cmtt-10">Band 07     </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-8-2"  
class="td11"><span 
class="cmti-10">Vegetation red edge</span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-8-3"  
class="td11">     779.7 <span 
class="cmti-10">nm        </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-8-4"  
class="td11">   20 <span 
class="cmti-10">nm    </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-8-5"  
class="td11">      20 <span 
class="cmti-10">m         </span></td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-9-"><td  style="white-space:nowrap; text-align:center;" id="TBL-2-9-1"  
class="td11">     <span 
class="cmtt-10">Band 08     </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-9-2"  
class="td11">      <span 
class="cmti-10">NIR         </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-9-3"  
class="td11">     832.9 <span 
class="cmti-10">nm        </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-9-4"  
class="td11">  106 <span 
class="cmti-10">nm   </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-9-5"  
class="td11">      10 <span 
class="cmti-10">m         </span></td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-10-"><td  style="white-space:nowrap; text-align:center;" id="TBL-2-10-1"  
class="td11">    <span 
class="cmtt-10">Band 08A    </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-10-2"  
class="td11">   <span 
class="cmti-10">Narrow NIR    </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-10-3"  
class="td11">     864.0 <span 
class="cmti-10">nm        </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-10-4"  
class="td11">   22 <span 
class="cmti-10">nm    </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-10-5"  
class="td11">      20 <span 
class="cmti-10">m         </span></td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-11-"><td  style="white-space:nowrap; text-align:center;" id="TBL-2-11-1"  
class="td11">     <span 
class="cmtt-10">Band 09     </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-11-2"  
class="td11">  <span 
class="cmti-10">Water vapour    </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-11-3"  
class="td11">     943.2 <span 
class="cmti-10">nm        </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-11-4"  
class="td11">   21 <span 
class="cmti-10">nm    </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-11-5"  
class="td11">      60 <span 
class="cmti-10">m         </span></td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-12-"><td  style="white-space:nowrap; text-align:center;" id="TBL-2-12-1"  
class="td11">     <span 
class="cmtt-10">Band 10     </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-12-2"  
class="td11">  <span 
class="cmti-10">SWIR &#8211; Cirrus   </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-12-3"  
class="td11">     1376.9 <span 
class="cmti-10">nm       </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-12-4"  
class="td11">   30 <span 
class="cmti-10">nm    </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-12-5"  
class="td11">      60 <span 
class="cmti-10">m         </span></td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-13-"><td  style="white-space:nowrap; text-align:center;" id="TBL-2-13-1"  
class="td11">     <span 
class="cmtt-10">Band 11     </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-13-2"  
class="td11">     <span 
class="cmti-10">SWIR        </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-13-3"  
class="td11">     1610.4 <span 
class="cmti-10">nm       </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-13-4"  
class="td11">   94 <span 
class="cmti-10">nm    </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-13-5"  
class="td11">      20 <span 
class="cmti-10">m         </span></td>
</tr><tr  
 style="vertical-align:baseline;" id="TBL-2-14-"><td  style="white-space:nowrap; text-align:center;" id="TBL-2-14-1"  
class="td11">     <span 
class="cmtt-10">Band 12     </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-14-2"  
class="td11">     <span 
class="cmti-10">SWIR        </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-14-3"  
class="td11">     2185.7 <span 
class="cmti-10">nm       </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-14-4"  
class="td11">  185 <span 
class="cmti-10">nm   </span></td><td  style="white-space:nowrap; text-align:center;" id="TBL-2-14-5"  
class="td11">      20 <span 
class="cmti-10">m         </span></td>
</tr><tr 
class="hline"><td><hr></td><td><hr></td><td><hr></td><td><hr></td><td><hr></td></tr><tr  
 style="vertical-align:baseline;" id="TBL-2-15-"><td  style="white-space:nowrap; text-align:center;" id="TBL-2-15-1"  
class="td11">                </td></tr></table></div>
                                                                                       
                                                                                       
   </div><hr class="endfloat" />
   </div>
<!--l. 140--><p class="indent" >   <span 
class="cmr-9">Over the year some parameters have been studied using earth knowledge, observation on the ground and machine</span>
<span 
class="cmr-9">learning. Among the most used parameters:</span>
     <ul class="itemize1">
     <li class="itemize"><span 
class="cmbx-9">NDVI </span><span 
class="cmti-9">(Normalized  difference  vegetation  index)</span><span 
class="cmr-9">:  Live  green  plants  absorb  solar  radiation  during  the</span>
     <span 
class="cmr-9">photosynthesis process; at the same time leaf cells re-emit solar radiation in the near-infrared spectral</span>
     <span 
class="cmr-9">region. Analyzing the re-emitted infrared and near-infrared spectral region you can conclude information</span>
     <span 
class="cmr-9">about the presence of vegetation in each area. The index is calculated normalizing the difference between</span>
     <span 
class="cmr-9">the spectral reflectance measurements acquired in the red (visible) and near-infrared regions.</span>
     </li>
     <li class="itemize"><span 
class="cmbx-9">NDWI </span><span 
class="cmti-9">(Normalized Difference Water Index)</span><span 
class="cmr-9">: it is derived from the </span><span 
class="cmti-9">Near-Infrared </span><span 
class="cmr-9">(NIR) and </span><span 
class="cmti-9">Short-Wave</span>
     <span 
class="cmti-9">Infrared </span><span 
class="cmr-9">(SWIR) channels. The SWIR reflectance reflects changes in both the vegetation water content and</span>
     <span 
class="cmr-9">the spongy mesophyll structure in vegetation canopies, while the NIR reflectance is affected by leaf internal</span>
     <span 
class="cmr-9">structure and leaf dry matter content but not by water content. The combination of the NIR with the SWIR</span>
     <span 
class="cmr-9">removes variations induced by leaf internal structure and leaf dry matter content, improving the accuracy</span>
     <span 
class="cmr-9">in retrieving the vegetation water content.</span>
     </li>
     <li class="itemize"><span 
class="cmbx-9">NDBI </span><span 
class="cmti-9">(Normalized Difference Built-Up Index)</span><span 
class="cmr-9">: This index highlights urban areas where there is typically</span>
     <span 
class="cmr-9">a higher reflectance in the </span><span 
class="cmti-9">shortwave-infrared </span><span 
class="cmr-9">(SWIR) region, compared to the </span><span 
class="cmti-9">near-infrared </span><span 
class="cmr-9">(NIR) region.</span>
     </li>
     <li class="itemize"><span 
class="cmbx-9">NDSI </span><span 
class="cmti-9">(Normalized-Difference Snow Index)</span><span 
class="cmr-9">: NDSI is a measure of the relative magnitude of the reflectance</span>
     <span 
class="cmr-9">difference between </span><span 
class="cmti-9">visible </span><span 
class="cmr-9">(green) and </span><span 
class="cmti-9">shortwave infrared </span><span 
class="cmr-9">(SWIR).</span></li></ul>
<!--l. 156--><p class="indent" >   <span 
class="cmr-9">The last index is often used to classify snow coverage from satellite images, just applying different thresholds.</span>
<span 
class="cmti-9">NASA portal for earth observation </span><span 
class="cmr-9">(</span><span 
class="cmbx-9">?</span><span 
class="cmr-9">) offers maps of the whole globe on different aspects registered by the</span>
<span 
class="cmr-9">sensors on their satellites. The snow monitoring portal, indeed, offers maps of the only NDSI pure index,</span>
<span 
class="cmr-9">and maps of a simple classification based on this index. The threshold value between </span><span 
class="cmti-9">snow </span><span 
class="cmr-9">and </span><span 
class="cmti-9">not-snow</span>
<span 
class="cmr-9">depends by the algorithm. The ground-truth values used in this project to train the classification model</span>
<span 
class="cmr-9">and to test it, are made starting from NDSI index obtained by NASA satellite, then manually merged</span>
<span 
class="cmr-9">and validated with values obtained from ground station widespread in northern Italy mountains. Snow</span>
<span 
class="cmr-9">coverage automatic classification of the soil is a field already studied also using satellite images; high level</span>
<span 
class="cmr-9">information are usually obtained by the manually work of earth scientists also on the data from NASA</span>
<span 
class="cmr-9">and ESA. Automatic classification can be useful to obtain data on the whole globe and have fast statistic</span>
<span 
class="cmr-9">information. Higher level usage of those information still requires expert intervention. The project aim is</span>
<span 
class="cmr-9">not only the evaluation of the results, but also having consideration on the machine learning algorithm:</span>
<span 
class="cmr-9">for this reason, NDSI index will not be used for the model training, but only the bands used to calculate</span>
<span 
class="cmr-9">it.</span>
   <h3 class="sectionHead"><span class="titlemark"><span 
class="cmr-9">2   </span></span> <a 
 id="x1-50002"></a><span 
class="cmr-9">Land Snow Cover Classification from Satellite Images</span></h3>
<!--l. 171--><p class="noindent" >
   <h4 class="subsectionHead"><span class="titlemark"><span 
class="cmr-9">2.1   </span></span> <a 
 id="x1-60002.1"></a><span 
class="cmr-9">Tools and Environment</span></h4>
<!--l. 172--><p class="noindent" ><span 
class="cmr-9">The project is developed using the programming language Python, compiled by the software Python 3.10; code is</span>
<span 
class="cmr-9">organised in different parts, and result are obtained working with the Jupiter Notebook Environment. Data are elaborated</span>
<span 
class="cmr-9">by EO-Learn data structure, that are based on Nunmpy Arrays, while the machine learining tools are made available by</span>
<span 
class="cmr-9">SciKit-Learn libraries. Data Visualization, finally, uses MatPlotLib functions and the library Bokeh for graphs and</span>
<span 
class="cmr-9">interaction. </span><br 
class="newline" /><span 
class="cmr-9">Libraries needed to the classification software are imported at the beginning of the code:</span>
     <ul class="itemize1">
     <li class="itemize"><span 
class="cmti-9">Built-in methods</span><span 
class="cmr-9">: </span><span 
class="cmtt-9">os, datetime, itertools, MultiValueEnum (from aenum)</span>
     </li>
     <li class="itemize"><span 
class="cmitt-10x-x-90">Python basic for data handle and visualization</span><span 
class="cmtt-9">: numpy, geopandas, pyplot (from</span>
     <span 
class="cmtt-9">matplotlib), ListedColormap and boundaryNorm (from matplotlib.color) Polygon (from</span>
     <span 
class="cmtt-9">shapely.geometry)</span>
     </li>
     <li class="itemize"><span 
class="cmitt-10x-x-90">Machine learning tools</span><span 
class="cmtt-9">: datasets (from sklearn), train</span>_<span 
class="cmtt-9">test</span>_<span 
class="cmtt-9">split and GridSearchCV (from</span>
     <span 
class="cmtt-9">sklearn.model</span>_<span 
class="cmtt-9">selection), classification</span>_<span 
class="cmtt-9">report (from sklearn.metrics) SVC, Perceptron,</span>
     <span 
class="cmtt-9">MLPClassifier, DecisionTreeClassifier, KNeighborsClassifier (from sklearn. ..)</span>
                                                                                       
                                                                                       
     </li>
     <li class="itemize"><span 
class="cmitt-10x-x-90">Tools for raster image management</span><span 
class="cmtt-9">: fiona, rasterio, pyproj, re, gdal (from osgeo)</span>
     </li>
     <li class="itemize"><span 
class="cmitt-10x-x-90">eo</span>_<span 
class="cmitt-10x-x-90">learn libraries</span><span 
class="cmtt-9">:  EOTask, EOPatch, EOWorkflow, linearly</span>_<span 
class="cmtt-9">connect</span>_<span 
class="cmtt-9">tasks, FeatureType,</span>
     <span 
class="cmtt-9">OverwritePermission, LoadTask, SaveTask, EOExecutor, MergeFeatureTask,</span>
     <span 
class="cmtt-9">SentinelHubInputTask, VectorImportTask, ExportToTiffTask, VectorToRasterTask, ErosionTask,</span>
     <span 
class="cmtt-9">LinearInterpolationTask, SimpleFilterTask, NormalizedDifferenceIndexTask, BlockSamplingTask</span>
     </li>
     <li class="itemize"><span 
class="cmitt-10x-x-90">Sentinel Hub libraries</span><span 
class="cmtt-9">: UtmZoneSplitter, DataCollection, UtmGridSplitter, OsmSplitter</span></li></ul>
<!--l. 188--><p class="noindent" >
   <h4 class="subsectionHead"><span class="titlemark"><span 
class="cmr-9">2.2   </span></span> <a 
 id="x1-70002.2"></a><span 
class="cmr-9">Obtain Satellite data</span></h4>
<!--l. 189--><p class="noindent" ><span 
class="cmr-9">Satellite images are available on the Sentinel-Hub portal after registration; data are automatically collect by a client</span>
<span 
class="cmr-9">previusly configurated. The area of interest of this project is located in the north of Italy on the Appennini&#8217;s mountain,</span>
<span 
class="cmr-9">with a focus on the Bologna and Modena&#8217;s district: a restricted area of interest meets the limitation imposed by Sentinel</span>
<span 
class="cmr-9">Hub portal on the download of data.</span>
   <h5 class="subsubsectionHead"><span class="titlemark"><span 
class="cmr-9">2.2.1   </span></span> <a 
 id="x1-80002.2.1"></a><span 
class="cmr-9">Definition of the area of interest</span></h5>
<!--l. 193--><p class="noindent" ><span 
class="cmr-9">Data on the Italian district boundaries are available freely on the portal </span><span 
class="cmti-9">openpolis </span><span 
class="cmr-9">(</span><span 
class="cmbx-9">?</span><span 
class="cmr-9">). To verify data and contextualize</span>
<span 
class="cmr-9">the work, general information are elaborated and visualizated. </span><!--l. 195-->
<div class="lstlisting" id="listing-1"><span class="label"><a 
 id="x1-8001r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">DATA_FOLDER</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">example_data</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8002r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8003r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Load</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">geojson</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">file</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8004r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">province</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">gpd</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">read_file</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">DATA_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">province</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">geojson</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8005r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">province</span><span 
class="cmtt-9">[(</span><span 
class="cmtt-9">province</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">prov_name</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]==</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">Modena</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">|</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">province</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">prov_name</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]==</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">Bologna</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8006r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">dissolve</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8007r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8008r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Plot</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">area</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8009r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">plot</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">;</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8010r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8011r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Get</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">area</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">s</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">polygon</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">format</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">size</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8012r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area_shape</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">geometry</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">values</span><span 
class="cmtt-9">[0]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8013r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area_width</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">interest_area_shape</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">bounds</span><span 
class="cmtt-9">[2]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area_shape</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">bounds</span><span 
class="cmtt-9">[0])</span><span 
class="cmtt-9">*100</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8014r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area_height</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">interest_area_shape</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">bounds</span><span 
class="cmtt-9">[3]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area_shape</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">bounds</span><span 
class="cmtt-9">[1])</span><span 
class="cmtt-9">*100</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8015r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8016r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Dimension</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">area</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">is</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">interest_area_width</span><span 
class="cmtt-9">:.2</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">interest_area_height</span><span 
class="cmtt-9">:.2</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">km2</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span>
   </div>
                                                                                       
                                                                                       
   <pre class="verbatim" id="verbatim-1">
&#x00A0;&#x00A0;&#x00A0;&#x00A0;Dimension&#x00A0;of&#x00A0;the&#x00A0;area&#x00A0;is&#x00A0;137.03&#x00A0;x&#x00A0;90.07&#x00A0;km2
</pre>
<!--l. 217--><p class="nopar" >
<!--l. 219--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                       
                                                                                       
<a 
 id="x1-8019r1"></a>
                                                                                       
                                                                                       
<!--l. 221--><p class="noindent" ><img 
src="vertopal_24a2006fe83f4b7aa33b81a457a028ff/5780d474e095efefe54d1f6bf9f3c6cbc8fd7712.png" alt="PIC"  
width="227" height="213" >
<br /> <div class="caption" 
><span class="id">Figure&#x00A0;1: </span><span  
class="content">Bologna and Modena Provinces</span></div><!--tex4ht:label?: x1-8019r1 -->
                                                                                       
                                                                                       
<!--l. 223--><p class="indent" >   </div><hr class="endfigure">
<!--l. 225--><p class="indent" >   <span 
class="cmr-9">The identified area is mostly interested by plain land: a further resizing will avoid the download of data referred to</span>
<span 
class="cmr-9">areas where snow is uncommon. A Buffer of 500 m is added to the political boundaries.</span>
   <!--l. 228-->
<div class="lstlisting" id="listing-2"><span class="label"><a 
 id="x1-8020r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">clip_shape</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Polygon</span><span 
class="cmtt-9">([(-57.35962388414055,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-0.5221310661900134)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(-57.35962388414055,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">44.7)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(79.6701812734866,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">44.7)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(79.6701812734866,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-0.5221310661900134)</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8021r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">geometry</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">clip</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">clip_shape</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8022r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8023r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Add</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">a</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">buffer</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">500</span><span 
class="cmtt-9">m</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">to</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">final</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">selected</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">area</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plot</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">it</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8024r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">buffer</span><span 
class="cmtt-9">(500)</span><span 
class="cmtt-9">;</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8025r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">plot</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8026r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8027r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Get</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">area</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">s</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">polygon</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">format</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">size</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8028r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area_shape</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">values</span><span 
class="cmtt-9">[0]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8029r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area_bounds</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area_shape</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">bounds</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8030r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area_width</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">interest_area_bounds</span><span 
class="cmtt-9">[2]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area_bounds</span><span 
class="cmtt-9">[0])</span><span 
class="cmtt-9">*100</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8031r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area_height</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">interest_area_bounds</span><span 
class="cmtt-9">[3]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area_bounds</span><span 
class="cmtt-9">[1])</span><span 
class="cmtt-9">*100</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8032r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8033r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Dimension</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">area</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">after</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">splitting</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">to</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">a</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">smaller</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">place</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">is</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">interest_area_width</span><span 
class="cmtt-9">:.2</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">interest_area_height</span><span 
class="cmtt-9">:.2</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">km2</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span>
   </div>
                                                                                       
                                                                                       
   <pre class="verbatim" id="verbatim-2">
&#x00A0;&#x00A0;&#x00A0;&#x00A0;Dimension&#x00A0;of&#x00A0;the&#x00A0;area&#x00A0;after&#x00A0;splitting&#x00A0;to&#x00A0;a&#x00A0;smaller&#x00A0;place&#x00A0;is&#x00A0;137.03&#x00A0;x&#x00A0;63.77&#x00A0;km2
</pre>
<!--l. 247--><p class="nopar" >
<!--l. 249--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                       
                                                                                       
<a 
 id="x1-8034r2"></a>
                                                                                       
                                                                                       
<!--l. 251--><p class="noindent" ><img 
src="vertopal_24a2006fe83f4b7aa33b81a457a028ff/2101b0066da1e08ba66044f0fd4fc1282f3518ad.png" alt="PIC"  
width="227" height="142" >
<br /> <div class="caption" 
><span class="id">Figure&#x00A0;2: </span><span  
class="content">Bologna and Modena Provinces reduced with a focus on the Appennini&#8217;s Mountains</span></div><!--tex4ht:label?: x1-8034r2 -->
                                                                                       
                                                                                       
<!--l. 253--><p class="indent" >   </div><hr class="endfigure">
<!--l. 255--><p class="indent" >   <span 
class="cmr-9">A eo-learn framework allows to split the Area Of Interest </span><span 
class="cmti-9">(AOI) </span><span 
class="cmr-9">into smaller patches, so they can be processed with</span>
<span 
class="cmr-9">limited computational resources. Boundaries map is then split in smaller and regular boxes thanks to </span><span 
class="cmti-9">Geopandas </span><span 
class="cmr-9">and</span>
<span 
class="cmti-9">shapely </span><span 
class="cmr-9">tools: as indicated on eo-learn documentation, the splitting choice depends on the amount of available resources,</span>
<span 
class="cmr-9">so the pipeline can be executed on a high-end scientific machine, as well as on a laptop. The output of this step is a list of</span>
<span 
class="cmr-9">bounding boxes covering the AOI.</span>
   <!--l. 260-->
<div class="lstlisting" id="listing-3"><span class="label"><a 
 id="x1-8035r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Create</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">a</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">splitter</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">to</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">obtain</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">a</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">list</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bboxes</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">with</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">5</span><span 
class="cmtt-9">km</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sides</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8036r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox_splitter</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">OsmSplitter</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">interest_area_shape</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">CRS</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">WGS84</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">zoom_level</span><span 
class="cmtt-9">=11)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8037r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox_list</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">array</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">bbox_splitter</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">get_bbox_list</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8038r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">info_list</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">array</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">bbox_splitter</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">get_info_list</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8039r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8040r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Prepare</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">info</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">selected</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPatches</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8041r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">geometry</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">Polygon</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">bbox</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">get_polygon</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox_list</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8042r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">idxs</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">p</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">enumerate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">bbox_list</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8043r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">idxs_x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">info</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">index_x</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">info</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">info_list</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8044r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">idxs_y</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">info</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">index_y</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">info</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">info_list</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8045r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8046r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox_gdf</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">gpd</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">GeoDataFrame</span><span 
class="cmtt-9">({</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">idxs</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">index_x</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">idxs_x</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">index_y</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">idxs_y</span><span 
class="cmtt-9">},</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">crs</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">interest_area</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">crs</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">geometry</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">geometry</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8047r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8048r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Display</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bboxes</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">over</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">country</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8049r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplots</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">figsize</span><span 
class="cmtt-9">=(30,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">30)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8050r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_title</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Interest</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">area</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">split</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fontsize</span><span 
class="cmtt-9">=25)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8051r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interest_area</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">plot</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">facecolor</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">w</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">edgecolor</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">b</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">alpha</span><span 
class="cmtt-9">=0.5)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8052r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox_gdf</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">plot</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">facecolor</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">w</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">edgecolor</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">r</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">alpha</span><span 
class="cmtt-9">=0.5,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">aspect</span><span 
class="cmtt-9">=1)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8053r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8054r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">zip</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">idxs</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox_list</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8055r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">geo</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">geometry</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8056r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">text</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">geo</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">centroid</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">geo</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">centroid</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ha</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">center</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">va</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">center</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span>
   </div>
<!--l. 285--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                       
                                                                                       
<a 
 id="x1-8059r3"></a>
                                                                                       
                                                                                       
<!--l. 288--><p class="noindent" ><img 
src="vertopal_24a2006fe83f4b7aa33b81a457a028ff/d72957c6903fd346325735e9efe526ff81c1aee1.png" alt="PIC"  
width="369" height="256" >
<br /> <div class="caption" 
><span class="id">Figure&#x00A0;3: </span><span  
class="content">Work area split in boxes</span></div><!--tex4ht:label?: x1-8059r3 -->
                                                                                       
                                                                                       
<!--l. 290--><p class="indent" >   </div><hr class="endfigure">
<!--l. 292--><p class="indent" >   <span 
class="cmr-9">For a better visualization, boxes outside a regular shape are ignored: the focus is manually setted on a rectangular</span>
<span 
class="cmr-9">area centered on the previusly defined one.</span>
   <!--l. 295-->
<div class="lstlisting" id="listing-4"><span class="label"><a 
 id="x1-8060r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Manually</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">select</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">a</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">rectangular</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">area</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">where</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">focus</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">attention</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-8061r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">focus_list</span><span 
class="cmtt-9">=[9,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">11,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">17,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">19,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">28,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">30,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">8,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">10,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">16,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">18,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">27,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">29,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">5,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">7,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">13,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">15,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">24,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">26,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">4,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">6,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">12,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">14,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">23,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">25]</span>
   </div>
   <h5 class="subsubsectionHead"><span class="titlemark"><span 
class="cmr-9">2.2.2   </span></span> <a 
 id="x1-90002.2.2"></a><span 
class="cmr-9">Prepare Sentinel-hub request</span></h5>
<!--l. 302--><p class="noindent" ><span 
class="cmr-9">With the bounding boxes of the empty patches in place, eo-learn enables the automatic download of Sentinel image data.</span>
<span 
class="cmr-9">In addition to data, eo-learn makes it possible to seamlessly access cloud masks and cloud probabilities: the Python</span>
<span 
class="cmr-9">package </span><span 
class="cmti-9">s2cloudless </span><span 
class="cmr-9">provides automated cloud detection in Sentinel-2 L1C imagery, based on a single-scene pixel-based</span>
<span 
class="cmr-9">classification. (</span><span 
class="cmbx-9">?</span><span 
class="cmr-9">)</span>
   <!--l. 306-->
<div class="lstlisting" id="listing-5"><span class="label"><a 
 id="x1-9001r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Define</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">classes</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">who</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">build</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">a</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">functional</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">valid</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">invalid</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pixels</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">on</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">satellite</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">images</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9002r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">@author</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">https</span><span 
class="cmtt-9">://</span><span 
class="cmtt-9">github</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">com</span><span 
class="cmtt-9">/</span><span 
class="cmtt-9">sentinel</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">hub</span><span 
class="cmtt-9">/</span><span 
class="cmtt-9">eo</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">learn</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">examples</span><span 
class="cmtt-9">/</span><span 
class="cmtt-9">tree</span><span 
class="cmtt-9">/</span><span 
class="cmtt-9">main</span><span 
class="cmtt-9">/</span><span 
class="cmtt-9">land</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">cover</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">map</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9003r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9004r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">class</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SentinelHubValidDataTask</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOTask</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9005r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"""</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9006r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Combine</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Sen2Cor</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">s</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">classification</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">map</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">with</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8216;</span><span 
class="cmtt-9">IS_DATA</span><span 
class="cmtt-9">&#8216;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">to</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">define</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">a</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8216;</span><span 
class="cmtt-9">VALID_DATA_SH</span><span 
class="cmtt-9">&#8216;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9007r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">The</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SentinelHub</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">s</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cloud</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">is</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">asumed</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">to</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">be</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">found</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">[&#8217;</span><span 
class="cmtt-9">CLM</span><span 
class="cmtt-9">&#8217;]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9008r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"""</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9009r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9010r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">def</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">__init__</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">output_feature</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9011r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">output_feature</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">output_feature</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9012r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9013r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">def</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">execute</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9014r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">output_feature</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">IS_DATA</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">].</span><span 
class="cmtt-9">astype</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">bool</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&amp;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(~</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">CLM</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">].</span><span 
class="cmtt-9">astype</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">bool</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9015r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">return</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9016r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9017r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9018r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">class</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">AddValidCountTask</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOTask</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9019r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"""</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9020r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">The</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">task</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">counts</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">number</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">valid</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">observations</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">time</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">series</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">stores</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">results</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">timeless</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9021r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"""</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9022r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9023r23"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">def</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">__init__</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">count_what</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">feature_name</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9024r24"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">what</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">count_what</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9025r25"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">feature_name</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9026r26"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9027r27"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">def</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">execute</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9028r28"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">MASK_TIMELESS</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">count_nonzero</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">what</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">axis</span><span 
class="cmtt-9">=0)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9029r29"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">return</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span>
   </div>
<!--l. 338--><p class="indent" >   <span 
class="cmr-9">The request for S2 bands </span><span 
class="cmti-9">B02, B03, B04, B06, B08, B11 </span><span 
class="cmr-9">and </span><span 
class="cmti-9">B12</span><span 
class="cmr-9">. This Bands allows us to calculate new useful</span>
<span 
class="cmr-9">features </span><span 
class="cmti-9">NDVI </span><span 
class="cmr-9">and </span><span 
class="cmti-9">NDWI</span><span 
class="cmr-9">. </span><span 
class="cmti-9">NDSI </span><span 
class="cmr-9">is calculated but not used in the project. The time period chosen is the </span><span 
class="cmti-9">winter</span>
<span 
class="cmti-9">2019-2020</span><span 
class="cmr-9">, from the First of November to the First of May.</span>
   <!--l. 342-->
<div class="lstlisting" id="listing-6"><span class="label"><a 
 id="x1-9030r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Add</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">a</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">request</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">S2</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bands</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">adding</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pre</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">built</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">filter</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cloudy</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">scenes</span><span 
class="cmtt-9">;</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9031r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">The</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">s2cloudless</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">masks</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">probabilities</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">are</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">requested</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">via</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">additional</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9032r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">@author</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">https</span><span 
class="cmtt-9">://</span><span 
class="cmtt-9">github</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">com</span><span 
class="cmtt-9">/</span><span 
class="cmtt-9">sentinel</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">hub</span><span 
class="cmtt-9">/</span><span 
class="cmtt-9">eo</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">learn</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">examples</span><span 
class="cmtt-9">/</span><span 
class="cmtt-9">tree</span><span 
class="cmtt-9">/</span><span 
class="cmtt-9">main</span><span 
class="cmtt-9">/</span><span 
class="cmtt-9">land</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">cover</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">map</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9033r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">band_names</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">B02</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">B03</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">B04</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">B06</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">B08</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">B11</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">B12</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9034r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">add_data</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SentinelHubInputTask</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9035r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bands_feature</span><span 
class="cmtt-9">=(</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">DATA</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">BANDS</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9036r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bands</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">band_names</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9037r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">resolution</span><span 
class="cmtt-9">=50,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9038r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">maxcc</span><span 
class="cmtt-9">=0.8,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9039r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">time_difference</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">datetime</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">timedelta</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">minutes</span><span 
class="cmtt-9">=120)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9040r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">data_collection</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">DataCollection</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">SENTINEL2_L1C</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9041r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">additional_data</span><span 
class="cmtt-9">=[(</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">MASK</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">dataMask</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">IS_DATA</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">MASK</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">CLM</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">DATA</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">CLP</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9042r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">max_threads</span><span 
class="cmtt-9">=5,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9043r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9044r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9045r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">CALCULATING</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NEW</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">FEATURES</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9046r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NDVI</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">B08</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">B04</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">/(</span><span 
class="cmtt-9">B08</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">B04</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9047r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NDWI</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">B03</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">B08</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">/(</span><span 
class="cmtt-9">B03</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">B08</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9048r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NDSI</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">B04</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">B06</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">/(</span><span 
class="cmtt-9">B04</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">B06</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9049r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9050r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NormalizedDifferenceIndexTask</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9051r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">DATA</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">BANDS</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">DATA</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">NDVI</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">band_names</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">B08</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">band_names</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">B04</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9052r23"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9053r24"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndwi</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NormalizedDifferenceIndexTask</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9054r25"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">DATA</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">BANDS</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">DATA</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">NDWI</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">band_names</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">B03</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">band_names</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">B08</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9055r26"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9056r27"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndsi</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NormalizedDifferenceIndexTask</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9057r28"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">DATA</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">BANDS</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">DATA</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">NDSI</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">band_names</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">B04</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">band_names</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">B06</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9058r29"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9059r30"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9060r31"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">DEFINE</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EO</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">LEAND</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">TASKS</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">AND</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">THE</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">WORFLOW</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9061r32"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">VALIDITY</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">MASK</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Validate</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pixels</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">using</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SentinelHub</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">s</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cloud</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">detection</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">region</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">acquisition</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9062r33"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">add_sh_validmask</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SentinelHubValidDataTask</span><span 
class="cmtt-9">((</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">MASK</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">IS_VALID</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9063r34"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">COUNTING</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">VALID</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">PIXELS</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Count</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">number</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">valid</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">observations</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">per</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pixel</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">using</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">valid</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9064r35"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">add_valid_count</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">AddValidCountTask</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">IS_VALID</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">VALID_COUNT</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9065r36"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SAVING</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">TO</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">OUTPUT</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">if</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">needed</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9066r37"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">save</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SaveTask</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOPATCH_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">overwrite_permission</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">OverwritePermission</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">OVERWRITE_PATCH</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9067r38"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9068r39"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">WORKFLOW</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9069r40"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">workflow_nodes</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">linearly_connect_tasks</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9070r41"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">add_data</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndwi</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndbi</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndsi</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">add_sh_validmask</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">add_valid_count</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">save</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9071r42"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9072r43"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">workflow</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOWorkflow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">workflow_nodes</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9073r44"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9074r45"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EXECUTE</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EO</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">LEARN</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">WORKFLOW</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9075r46"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%%</span><span 
class="cmtt-9">time</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9076r47"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">time_interval</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">2019-11-01</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">2020-05-31</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9077r48"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">input_node</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">workflow_nodes</span><span 
class="cmtt-9">[0]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9078r49"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">save_node</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">workflow_nodes</span><span 
class="cmtt-9">[-1]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9079r50"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">execution_args</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9080r51"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">enumerate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">bbox_list</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9081r52"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">execution_args</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">append</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9082r53"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9083r54"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">input_node</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">bbox</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">time_interval</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">time_interval</span><span 
class="cmtt-9">},</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9084r55"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">save_node</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_folder</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">},</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9085r56"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9086r57"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9087r58"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">executor</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOExecutor</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">workflow</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">execution_args</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">save_logs</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9088r59"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">executor</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">run</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9089r60"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9090r61"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">executor</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">make_report</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9091r62"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9092r63"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">failed_ids</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">executor</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">get_failed_executions</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9093r64"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">if</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">failed_ids</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9094r65"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">raise</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">RuntimeError</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9095r66"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Execution</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">failed</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPatches</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">with</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">IDs</span><span 
class="cmtt-9">:\</span><span 
class="cmtt-9">n</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">failed_ids</span><span 
class="cmtt-9">}\</span><span 
class="cmtt-9">n</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9096r67"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">For</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">more</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">info</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">check</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">report</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">at</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">executor</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">get_report_path</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-9097r68"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">)</span>
   </div>
<!--l. 413--><p class="noindent" >
   <h5 class="subsubsectionHead"><span class="titlemark"><span 
class="cmr-9">2.2.3   </span></span> <a 
 id="x1-100002.2.3"></a><span 
class="cmr-9">Visualize the data</span></h5>
<!--l. 414--><p class="noindent" ><span 
class="cmr-9">Data are visualized to contestualize the work. Firt of all the </span><span 
class="cmti-9">RGB </span><span 
class="cmr-9">image where the AOI land is shown.</span>
   <!--l. 416-->
<div class="lstlisting" id="listing-7"><span class="label"><a 
 id="x1-10001r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">axs</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplots</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">nrows</span><span 
class="cmtt-9">=4,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ncols</span><span 
class="cmtt-9">=6,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">figsize</span><span 
class="cmtt-9">=(20,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">15)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10002r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10003r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">date</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">datetime</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">datetime</span><span 
class="cmtt-9">(2020,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">14)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10004r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">patchID</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">enumerate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">focus_list</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10005r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch_path</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOPATCH_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">patchID</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10006r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch_path</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lazy_loading</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10007r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10008r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dates</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">array</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">replace</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">tzinfo</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">None</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10009r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">argsort</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">abs</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">date</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dates</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">[0]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10010r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10011r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">axs</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">//</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">6][</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">6]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10012r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">imshow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">clip</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">BANDS</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">][...,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0]]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">*</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">3.5,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10013r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_xticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10014r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_yticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10015r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_aspect</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">auto</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10016r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">del</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10017r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10018r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplots_adjust</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">wspace</span><span 
class="cmtt-9">=0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">hspace</span><span 
class="cmtt-9">=0)</span>
   </div>
<!--l. 437--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                       
                                                                                       
<a 
 id="x1-10019r4"></a>
                                                                                       
                                                                                       
<!--l. 439--><p class="noindent" ><img 
src="vertopal_24a2006fe83f4b7aa33b81a457a028ff/8655fd998f1f54b4681468deefd44d52b1d6c089.png" alt="PIC"  
width="341" height="284" >
<br /> <div class="caption" 
><span class="id">Figure&#x00A0;4: </span><span  
class="content">RGB image of the Area of Intrest</span></div><!--tex4ht:label?: x1-10019r4 -->
                                                                                       
                                                                                       
<!--l. 441--><p class="indent" >   </div><hr class="endfigure">
<!--l. 443--><p class="indent" >   <span 
class="cmr-9">Automatic cloud cleaning is applied as a eo-learn task: pixels considered as a cloud are labeled as </span><span 
class="cmti-9">INVALID</span><span 
class="cmr-9">. To</span>
<span 
class="cmr-9">appreciate effects of cloud cleaning, let&#8217;s analyze the mean of the </span><span 
class="cmti-9">NDVI </span><span 
class="cmr-9">index: it represents the mean of the</span>
<span 
class="cmr-9">amount of vegetation of the area; we expect a linear trend over the time period, just lower during the</span>
<span 
class="cmr-9">winter.</span>
   <!--l. 447-->
<div class="lstlisting" id="listing-8"><span class="label"><a 
 id="x1-10020r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eID</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">16</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10021r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOPATCH_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lazy_loading</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10022r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10023r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">NDVI</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10024r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">IS_VALID</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10025r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">time</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">array</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10026r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">t</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">w</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">h</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">_</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10027r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10028r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi_clean</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">copy</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10029r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi_clean</span><span 
class="cmtt-9">[~</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">nan</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Set</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">values</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">invalid</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pixels</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">to</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NaN</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">s</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10030r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10031r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Calculate</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">means</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">remove</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NaN</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">s</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">from</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">means</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10032r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi_mean</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">nanmean</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">ndvi</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">reshape</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">t</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">w</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">*</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">h</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">axis</span><span 
class="cmtt-9">=1)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10033r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi_mean_clean</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">nanmean</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">ndvi_clean</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">reshape</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">t</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">w</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">*</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">h</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">axis</span><span 
class="cmtt-9">=1)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10034r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">time_clean</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">time</span><span 
class="cmtt-9">[~</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">isnan</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">ndvi_mean_clean</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10035r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi_mean_clean</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi_mean_clean</span><span 
class="cmtt-9">[~</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">isnan</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">ndvi_mean_clean</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10036r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10037r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">figure</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">figsize</span><span 
class="cmtt-9">=(20,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">5)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10038r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">plot</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">time_clean</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi_mean_clean</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">s</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">label</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Mean</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NDVI</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">with</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cloud</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cleaning</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10039r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">plot</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">time</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi_mean</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">o</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">label</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Mean</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NDVI</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">without</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cloud</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cleaning</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10040r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">xlabel</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Time</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fontsize</span><span 
class="cmtt-9">=15)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10041r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">ylabel</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Mean</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NDVI</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">over</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">patch</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fontsize</span><span 
class="cmtt-9">=15)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10042r23"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">xticks</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">fontsize</span><span 
class="cmtt-9">=15)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10043r24"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">yticks</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">fontsize</span><span 
class="cmtt-9">=15)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10044r25"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10045r26"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">legend</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">loc</span><span 
class="cmtt-9">=2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">prop</span><span 
class="cmtt-9">={</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">size</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">15})</span><span 
class="cmtt-9">;</span>
   </div>
                                                                                       
                                                                                       
   <pre class="verbatim" id="verbatim-3">
&#x00A0;&#x00A0;&#x00A0;&#x00A0;ndvi_mean_clean&#x00A0;=&#x00A0;np.nanmean(ndvi_clean.reshape(t,&#x00A0;w&#x00A0;*&#x00A0;h),&#x00A0;axis=1)
</pre>
<!--l. 478--><p class="nopar" >
<!--l. 480--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                       
                                                                                       
<a 
 id="x1-10046r5"></a>
                                                                                       
                                                                                       
<!--l. 482--><p class="noindent" ><img 
src="vertopal_24a2006fe83f4b7aa33b81a457a028ff/bf67eec1b85ca850604682cb2c05d2327b960098.png" alt="PIC"  
width="455" height="113" >
<br /> <div class="caption" 
><span class="id">Figure&#x00A0;5: </span><span  
class="content">NDVI mean value over boxes applied to original images and to cloud-cleaned images</span></div><!--tex4ht:label?: x1-10046r5 -->
                                                                                       
                                                                                       
<!--l. 484--><p class="indent" >   </div><hr class="endfigure">
<!--l. 486--><p class="indent" >   <span 
class="cmr-9">Without cloud cleaning, values are highly variable from month to month, while this trend is a little corrected with the</span>
<span 
class="cmr-9">cloud cleaning. </span><br 
class="newline" />
<!--l. 488--><p class="indent" >   <span 
class="cmr-9">It is relevant and interesting to visualize the NDVI map for the vegetation and the NDSI map for the snow:</span>
<!--l. 489-->
<div class="lstlisting" id="listing-9"><span class="label"><a 
 id="x1-10047r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">axs</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplots</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">nrows</span><span 
class="cmtt-9">=4,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ncols</span><span 
class="cmtt-9">=6,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">figsize</span><span 
class="cmtt-9">=(20,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">15)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10048r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10049r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">patchID</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">enumerate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">focus_list</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10050r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch_path</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOPATCH_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">patchID</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10051r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch_path</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lazy_loading</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10052r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">NDVI</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NDSI</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10053r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">IS_VALID</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10054r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi</span><span 
class="cmtt-9">[~</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">nan</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10055r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ndvi_mean</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">nanmean</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">ndvi</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">axis</span><span 
class="cmtt-9">=0)</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">squeeze</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10056r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10057r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">axs</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">//</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">6][</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">6]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10058r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">im</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">imshow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">ndvi_mean</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">vmin</span><span 
class="cmtt-9">=0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">vmax</span><span 
class="cmtt-9">=0.8,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cmap</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">get_cmap</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">YlGn</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10059r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_xticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10060r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_yticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10061r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_aspect</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">auto</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10062r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">del</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10063r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10064r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplots_adjust</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">wspace</span><span 
class="cmtt-9">=0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">hspace</span><span 
class="cmtt-9">=0)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10065r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10066r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cb</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">colorbar</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">im</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">axs</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">ravel</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">tolist</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">orientation</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">horizontal</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pad</span><span 
class="cmtt-9">=0.01,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">aspect</span><span 
class="cmtt-9">=100)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10067r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cb</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">tick_params</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">labelsize</span><span 
class="cmtt-9">=20)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10068r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">show</span><span 
class="cmtt-9">()</span>
   </div>
<!--l. 514--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                       
                                                                                       
<a 
 id="x1-10069r6"></a>
                                                                                       
                                                                                       
<!--l. 516--><p class="noindent" ><img 
src="vertopal_24a2006fe83f4b7aa33b81a457a028ff/80d6d234bcdef4047da3682eb1820f19628cfc9d.png" alt="PIC"  
width="213" height="184" > <img 
src="vertopal_24a2006fe83f4b7aa33b81a457a028ff/f0a227dd971d47ab8a0ae2f9c339cdac1da50704.png" alt="PIC"  
width="213" height="184" >
<br /> <div class="caption" 
><span class="id">Figure&#x00A0;6: </span><span  
class="content">NDVI (left) and NDSI (right) maps</span></div><!--tex4ht:label?: x1-10069r6 -->
                                                                                       
                                                                                       
<!--l. 519--><p class="indent" >   </div><hr class="endfigure">
<!--l. 521--><p class="indent" >   <span 
class="cmr-9">Finally the cloud probability map, calculated using values defined as cloud by the </span><span 
class="cmti-9">s2cloudless </span><span 
class="cmr-9">software.</span>
   <!--l. 523-->
<div class="lstlisting" id="listing-10"><span class="label"><a 
 id="x1-10070r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cloud</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">probability</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10071r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">axs</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplots</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">nrows</span><span 
class="cmtt-9">=4,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ncols</span><span 
class="cmtt-9">=6,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">figsize</span><span 
class="cmtt-9">=(20,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">15)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10072r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10073r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">patchID</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">enumerate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">focus_list</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10074r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch_path</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOPATCH_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">patchID</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10075r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch_path</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lazy_loading</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10076r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">clp</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">CLP</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">].</span><span 
class="cmtt-9">astype</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">float</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">/</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">255</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10077r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">IS_VALID</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10078r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">clp</span><span 
class="cmtt-9">[~</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">nan</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10079r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">clp_mean</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">nanmean</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">clp</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">axis</span><span 
class="cmtt-9">=0)</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">squeeze</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10080r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10081r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">axs</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">//</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">6][</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">6]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10082r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">im</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">imshow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">clp_mean</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">vmin</span><span 
class="cmtt-9">=0.0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">vmax</span><span 
class="cmtt-9">=0.3,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cmap</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">cm</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">inferno</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10083r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_xticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10084r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_yticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10085r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_aspect</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">auto</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10086r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">del</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10087r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10088r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplots_adjust</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">wspace</span><span 
class="cmtt-9">=0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">hspace</span><span 
class="cmtt-9">=0)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10089r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10090r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cb</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">colorbar</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">im</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">axs</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">ravel</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">tolist</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">orientation</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">horizontal</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pad</span><span 
class="cmtt-9">=0.01,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">aspect</span><span 
class="cmtt-9">=100)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10091r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cb</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">tick_params</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">labelsize</span><span 
class="cmtt-9">=20)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-10092r23"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">show</span><span 
class="cmtt-9">()</span>
   </div>
<!--l. 549--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                       
                                                                                       
<a 
 id="x1-10093r7"></a>
                                                                                       
                                                                                       
<!--l. 551--><p class="noindent" ><img 
src="vertopal_24a2006fe83f4b7aa33b81a457a028ff/976a1170d0f9100315bc20fb8007818a6ef04693.png" alt="PIC"  
width="227" height="199" >
<br /> <div class="caption" 
><span class="id">Figure&#x00A0;7: </span><span  
class="content">Cloud probability map</span></div><!--tex4ht:label?: x1-10093r7 -->
                                                                                       
                                                                                       
<!--l. 553--><p class="indent" >   </div><hr class="endfigure">
   <h4 class="subsectionHead"><span class="titlemark"><span 
class="cmr-9">2.3   </span></span> <a 
 id="x1-110002.3"></a><span 
class="cmr-9">Obtain ground truth Data</span></h4>
<!--l. 556--><p class="noindent" ><span 
class="cmr-9">Ground truth data are obtained by the validation work of NASA maps (</span><span 
class="cmbx-9">?</span><span 
class="cmr-9">): from NASA satellite data NDSI map is</span>
<span 
class="cmr-9">calculated thought a validation work using ground station values, a specific threshold is calculated to distinguish snow</span>
<span 
class="cmr-9">areas, iced cloud and areas without snow.</span><br 
class="newline" /><span 
class="cmr-9">The ground truth maps are referred to the whole Emilia Romagna, and saved as </span><span 
class="cmti-9">geotiff  </span><span 
class="cmr-9">images; the reference</span>
<span 
class="cmr-9">system is different from the one used to obtain data from Sentinel Hub portal, and definition is lower.</span>
<hr class="figure"><div class="figure" 
>
                                                                                       
                                                                                       
<a 
 id="x1-11001r8"></a>
                                                                                       
                                                                                       
<!--l. 562--><p class="noindent" ><img 
src="vertopal_24a2006fe83f4b7aa33b81a457a028ff/NDSI_Snow_Cover_2020093_32632.png" alt="PIC"  
width="227" height="184" >
<br /> <div class="caption" 
><span class="id">Figure&#x00A0;8: </span><span  
class="content">Ground truth map of Emilia Romagna</span></div><!--tex4ht:label?: x1-11001r8 -->
                                                                                       
                                                                                       
<!--l. 564--><p class="indent" >   </div><hr class="endfigure">
<!--l. 566--><p class="indent" >   <span 
class="cmr-9">First of all, we define utility functions to work with the maps: coordinates are translate to the reference system</span>
<span 
class="cmti-9">EPSG:32632 WGS:84</span><span 
class="cmr-9">.</span>
   <!--l. 568-->
<div class="lstlisting" id="listing-11"><span class="label"><a 
 id="x1-11002r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">def</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">translateCoordinate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">geometry</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11003r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">proj</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pyproj</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">Transformer</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">from_crs</span><span 
class="cmtt-9">(4326,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">32632,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">always_xy</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11004r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">shape_points</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11005r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">xx</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">yy</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">geometry</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">exterior</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">coords</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11006r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">shape_points</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">append</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">proj</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">transform</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">xx</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">yy</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11007r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">return</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">MultiPolygon</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">Polygon</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">shape_points</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">])</span>
   </div>
<!--l. 577--><p class="indent" >   <span 
class="cmr-9">Another funcion applies a mask to Geotiff images and defines the new image dimension.</span>
   <!--l. 579-->
<div class="lstlisting" id="listing-12"><span class="label"><a 
 id="x1-11008r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NoDataValue</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-9999.0</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11009r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">def</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">applyMask</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">raster_file</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">shape_mask</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">size_x</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">size_y</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11010r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">with</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">rasterio</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">open</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">raster_file</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">as</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">src</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11011r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">out_image</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">out_transform</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">src</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">shape_mask</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">crop</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">nodata</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">None</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11012r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">out_meta</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">src</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">meta</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">copy</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11013r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11014r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">out_meta</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">update</span><span 
class="cmtt-9">({</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">driver</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">GTiff</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11015r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">height</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">size_y</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11016r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">width</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">size_x</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11017r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">transform</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">out_transform</span><span 
class="cmtt-9">})</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11018r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11019r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">return</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">out_image</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">out_meta</span>
   </div>
<!--l. 594--><p class="indent" >   <span 
class="cmr-9">The funcions are now applied to files: we will obtain a map for every boxes previusly defined, for every day in the time</span>
<span 
class="cmr-9">window of interest. To obtain a pixel-to-pixel correspondence between the ground truth map and the eo-learn bands,</span>
<span 
class="cmr-9">pixels of real data maps are manually replicated for an area of 8x8 pixels. A filler pad is added when dimensions do not</span>
<span 
class="cmr-9">correspond: it will be left out during the training phase.</span>
   <!--l. 598-->
<div class="lstlisting" id="listing-13"><span class="label"><a 
 id="x1-11020r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11021r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">path_file</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">ground_truth_data</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11022r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">path_out</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">output</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11023r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11024r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">File</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">elaboration</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11025r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11026r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">filename</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x003C;</span><span 
class="cmtt-9">real_data_file_list</span><span 
class="cmtt-9">&#x003E;:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11027r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11028r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">output_path</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">path_out</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">real_data_</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">filename</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">rsplit</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,6)</span><span 
class="cmtt-9">[1].</span><span 
class="cmtt-9">rsplit</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">A</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1)</span><span 
class="cmtt-9">[1])</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11029r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">makedirs</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">output_path</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">exist_ok</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11030r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11031r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">focus_list</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11032r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">shape_mask</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">translateCoordinate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">bbox_gdf</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">bbox_gdf</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]==</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">].</span><span 
class="cmtt-9">geometry</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">item</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">translate</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">real</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">coordinates</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11033r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sample_path</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">eopatches_sampled</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11034r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox_meta</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">sample_path</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lazy_loading</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">meta_info</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">coordinates</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11035r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11036r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">raster_img</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">raster_img_meta</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">applyMask</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">filename</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">shape_mask</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">geoms</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox_meta</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">size_x</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox_meta</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">size_y</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11037r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11038r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pad_width</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">int</span><span 
class="cmtt-9">((</span><span 
class="cmtt-9">bbox_meta</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">size_x</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">raster_img</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">[1]*8)</span><span 
class="cmtt-9">-1)</span><span 
class="cmtt-9">/2)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">padding</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11039r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pad_height</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">int</span><span 
class="cmtt-9">((</span><span 
class="cmtt-9">bbox_meta</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">size_y</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">raster_img</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">[2]*8)</span><span 
class="cmtt-9">-1)</span><span 
class="cmtt-9">/2)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11040r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11041r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">raster_out</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">full</span><span 
class="cmtt-9">((1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox_meta</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">size_x</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bbox_meta</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">size_y</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-1)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-1</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NO</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">DATA</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11042r23"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11043r24"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">value</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">ndenumerate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">raster_img</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11044r25"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">if</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">value</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">==</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11045r26"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">c</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">8)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11046r27"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">r</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">8)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11047r28"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">raster_out</span><span 
class="cmtt-9">[(</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">[0],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pad_width</span><span 
class="cmtt-9">+(</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">[1]*8)</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">c</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pad_height</span><span 
class="cmtt-9">+(</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">[2]*8)</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">r</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">]=1</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11048r29"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11049r30"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">elif</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">vale</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">==</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-1:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NO_DATA</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">cloud</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11050r31"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">c</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">8)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11051r32"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">r</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">8)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11052r33"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">raster_out</span><span 
class="cmtt-9">[(</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">[0],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pad_width</span><span 
class="cmtt-9">+(</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">[1]*8)</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">c</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pad_height</span><span 
class="cmtt-9">+(</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">[2]*8)</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">r</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">]=2</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11053r34"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">else</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">no</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11054r35"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">c</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">8)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11055r36"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">r</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">8)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11056r37"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">raster_out</span><span 
class="cmtt-9">[(</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">[0],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pad_width</span><span 
class="cmtt-9">+(</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">[1]*8)</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">c</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pad_height</span><span 
class="cmtt-9">+(</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">[2]*8)</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">r</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">]=0</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">land</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11057r38"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11058r39"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">with</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">rasterio</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">open</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">output_path</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">bbox_</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">tiff</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">w</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">**</span><span 
class="cmtt-9">raster_img_meta</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">as</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dest</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11059r40"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dest</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">write</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">raster_out</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11060r41"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11061r42"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Done</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span>
   </div>
<!--l. 643--><p class="indent" >   <span 
class="cmr-9">The new map of real values is added to the eo-learn data structures.</span>
   <!--l. 645-->
<div class="lstlisting" id="listing-14"><span class="label"><a 
 id="x1-11062r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Add</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">real</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">to</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eo_patches</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11063r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-1</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NO</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">DATA</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11064r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">LAND</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11065r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SNOW</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11066r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ICE</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">CLOUD</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11067r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11068r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">focus_list</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11069r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sample_path</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOPATCH_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11070r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">sample_path</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lazy_loading</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11071r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">LABEL</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">full</span><span 
class="cmtt-9">((</span><span 
class="cmtt-9">len</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">meta_info</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">size_y</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">meta_info</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">size_x</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11072r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">mask_timeless</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">REAL_DATA_SNOW_COUNT</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">full</span><span 
class="cmtt-9">((</span><span 
class="cmtt-9">len</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11073r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day_index</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">enumerate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11074r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day_of_year</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">timetuple</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">tm_yday</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11075r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11076r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">if</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day_of_year</span><span 
class="cmtt-9">&#x003E;106:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11077r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">continue</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11078r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11079r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">year</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">year</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11080r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">raster_folder</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">real_data_</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">year</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">day_of_year</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">zfill</span><span 
class="cmtt-9">(3)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11081r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">with</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">rasterio</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">open</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">output</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">raster_folder</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">bbox_</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">tiff</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">r</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">as</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">src</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11082r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">labels</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">src</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">read</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11083r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">LABEL</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">day_index</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">transpose</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">labels</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11084r23"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">mask_timeless</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">REAL_DATA_SNOW_COUNT</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">day_index</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">count_nonzero</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">labels</span><span 
class="cmtt-9">==1)</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11085r24"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11086r25"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">save</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">NEW_EOPATCH_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">overwrite_permission</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">OverwritePermission</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">OVERWRITE_PATCH</span><span 
class="cmtt-9">)</span>
   </div>
   <!--l. 673-->
<div class="lstlisting" id="listing-15"><span class="label"><a 
 id="x1-11087r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">LOAD</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EXISTING</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPATCHES</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11088r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">LoadTask</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">NEW_EOPATCH_FOLDER</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11089r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11090r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">FEATURE</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">CONCATENATION</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11091r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">concatenate</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">MergeFeatureTask</span><span 
class="cmtt-9">({</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">DATA</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">BANDS</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">NDBI</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">NDVI</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">NDWI</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]},</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">DATA</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">FEATURES</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11092r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11093r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SAVING</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11094r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">save</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SaveTask</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOPATCH_SAMPLES_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">overwrite_permission</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">OverwritePermission</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">OVERWRITE_PATCH</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11095r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11096r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Define</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">workflow</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11097r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">workflow_nodes</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">linearly_connect_tasks</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">concatenate</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">save</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11098r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">workflow</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOWorkflow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">workflow_nodes</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11099r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11100r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%%</span><span 
class="cmtt-9">time</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EXECUTION</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11101r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11102r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">...</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">]</span>
   </div>
<!--l. 691--><p class="indent" >   <span 
class="cmr-9">Sampling data can help training algoritm to be more efficient; in the work contest of this project, particularly,</span>
<span 
class="cmr-9">most of data are cloud or land, with just a little percent of snow, centered in the Appennini&#8217;s mountain.</span>
<span 
class="cmr-9">A first data cleaning consists of deleteing all the parts of maps in all the time spots where there is no</span>
<span 
class="cmr-9">snow: the effect of this operation is to obtain a smaller dataset, where snow, cloud and land pixels are more</span>
<span 
class="cmr-9">balanced.</span>
   <!--l. 696-->
<div class="lstlisting" id="listing-16"><span class="label"><a 
 id="x1-11103r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Keep</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">only</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">days</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">with</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">at</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">least</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">500</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">pixels</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11104r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">focus_list</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11105r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sample_path</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOPATCH_SAMPLES_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11106r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">sample_path</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lazy_loading</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11107r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11108r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_pixels_index</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">reversed</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">len</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">mask_timeless</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">REAL_DATA_SNOW_COUNT</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11109r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">if</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">mask_timeless</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">REAL_DATA_SNOW_COUNT</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">snow_pixels_index</span><span 
class="cmtt-9">][0][0]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x003C;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">500:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11110r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">FEATURES</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">delete</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">FEATURES</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_pixels_index</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11111r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">LABEL</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">delete</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">LABEL</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_pixels_index</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11112r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">save</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOPATCH_TRAINING_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">overwrite_permission</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">OverwritePermission</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">OVERWRITE_PATCH</span><span 
class="cmtt-9">)</span>
   </div>
<!--l. 709--><p class="indent" >   <span 
class="cmr-9">A further sampling with no criteria on the selected images.</span>
   <!--l. 711-->
<div class="lstlisting" id="listing-17"><span class="label"><a 
 id="x1-11113r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">LOAD</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EXISTING</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPATCHES</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11114r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">load_2</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">LoadTask</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOPATCH_TRAINING_FOLDER</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11115r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11116r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SPATIAL</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SAMPLIG</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">OF</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">60%</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">OF</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">DATA</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11117r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">spatial_sampling</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">BlockSamplingTask</span><span 
class="cmtt-9">([(</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">DATA</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">FEATURES</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">FEATURES_SAMPLED</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">FeatureType</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">DATA</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">LABEL</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">LABEL_SAMPLED</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0.6)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11118r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11119r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">SAVING</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11120r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">save_2</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SaveTask</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOPATCH_TRAINING_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">overwrite_permission</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">OverwritePermission</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">OVERWRITE_PATCH</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11121r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11122r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">define</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">a</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">new</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">workflow</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11123r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">workflow_nodes_2</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">linearly_connect_tasks</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">load_2</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">spatial_sampling</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">save_2</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11124r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">workflow_2</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOWorkflow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">workflow_nodes_2</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11125r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11126r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%%</span><span 
class="cmtt-9">time</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EXECUTION</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-11127r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">...</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">]</span>
   </div>
   <h4 class="subsectionHead"><span class="titlemark"><span 
class="cmr-9">2.4   </span></span> <a 
 id="x1-120002.4"></a><span 
class="cmr-9">Training the classification Algoritm</span></h4>
<!--l. 730--><p class="noindent" >
   <h5 class="subsubsectionHead"><span class="titlemark"><span 
class="cmr-9">2.4.1   </span></span> <a 
 id="x1-130002.4.1"></a><span 
class="cmr-9">Prepare traning and test dataset</span></h5>
<!--l. 731--><p class="noindent" ><span 
class="cmr-9">Data previusly prepared are now splittend in two dataset, for train and test the model.</span>
   <!--l. 735-->
                                                                                       
                                                                                       
<div class="lstlisting" id="listing-18"><span class="label"><a 
 id="x1-13001r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Load</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sampled</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatches</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13002r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sampled_eopatches</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13003r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13004r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">focus_list</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13005r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sample_path</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOPATCH_TRAINING_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13006r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sampled_eopatches</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">append</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOPatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">sample_path</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lazy_loading</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13007r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13008r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Set</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">features</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">labels</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">train</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">test</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sets</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13009r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">features</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13010r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">labels</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13011r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">num_data</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13012r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sampled_eopatches</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13013r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">len</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">FEATURES_SAMPLED</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13014r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">num_data</span><span 
class="cmtt-9">+=1</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13015r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">features</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">append</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">FEATURES_SAMPLED</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13016r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">labels</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">append</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">LABEL_SAMPLED</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13017r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13018r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">X</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">concatenate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">features</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13019r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">concatenate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">labels</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13020r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13021r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">X</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13022r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">)</span>
   </div>
                                                                                       
                                                                                       
   <pre class="verbatim" id="verbatim-4">
&#x00A0;&#x00A0;&#x00A0;&#x00A0;(992866,&#x00A0;1,&#x00A0;10)
&#x00A0;&#x00A0;&#x00A0;&#x00A0;(992866,&#x00A0;1,&#x00A0;1)
</pre>
<!--l. 762--><p class="nopar" > <!--l. 763-->
<div class="lstlisting" id="listing-19"><span class="label"><a 
 id="x1-13023r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">X</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">X</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">reshape</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">X</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">[0],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">X</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">[-1])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13024r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">reshape</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">[0],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">[-1])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13025r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">Shape</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">features</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dataset</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">after</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">reshaping</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">\</span><span 
class="cmtt-9">t</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">X</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13026r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">Shape</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">labels</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dataset</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">after</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">reshaping</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">\</span><span 
class="cmtt-9">t</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span>
   </div>
                                                                                       
                                                                                       
   <pre class="verbatim" id="verbatim-5">
&#x00A0;&#x00A0;&#x00A0;&#x00A0;Shape&#x00A0;of&#x00A0;features&#x00A0;dataset&#x00A0;after&#x00A0;reshaping:&#x00A0; (992866,&#x00A0;10)
&#x00A0;&#x00A0;&#x00A0;&#x00A0;Shape&#x00A0;of&#x00A0;labels&#x00A0;dataset&#x00A0;after&#x00A0;reshaping:&#x00A0; (992866,&#x00A0;1)
</pre>
<!--l. 772--><p class="nopar" >
<!--l. 774--><p class="indent" >   <span 
class="cmr-9">Any of the satellite images from Sentinel 2 have missing data; labels contain a filling pad, previously added, containing</span>
<span 
class="cmr-9">the value </span><span 
class="cmti-9">-1</span><span 
class="cmr-9">: data have to be cleaned from invalid entries before the training phase.</span>
   <!--l. 778-->
<div class="lstlisting" id="listing-20"><span class="label"><a 
 id="x1-13027r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">rows_with_NaN</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">X</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">isnan</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">X</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">any</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">axis</span><span 
class="cmtt-9">=1)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">:])</span><span 
class="cmtt-9">[0]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13028r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">labels_NaN</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">==-1])</span><span 
class="cmtt-9">[0]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13029r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13030r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">There</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">are</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{:.0</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">rows</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">containing</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NaN</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">value</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">features</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dataset</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">format</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">rows_with_NaN</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13031r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">There</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">are</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{:.0</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">rows</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">containing</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-1</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">labels</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">training</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dataset</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">format</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">labels_NaN</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span>
   </div>
                                                                                       
                                                                                       
   <pre class="verbatim" id="verbatim-6">
&#x00A0;&#x00A0;&#x00A0;&#x00A0;There&#x00A0;are&#x00A0;274186&#x00A0;rows&#x00A0;containing&#x00A0;NaN&#x00A0;value&#x00A0;in&#x00A0;the&#x00A0;features&#x00A0;dataset
&#x00A0;&#x00A0;&#x00A0;&#x00A0;There&#x00A0;are&#x00A0;177957&#x00A0;rows&#x00A0;containing&#x00A0;-1&#x00A0;in&#x00A0;labels&#x00A0;in&#x00A0;the&#x00A0;training&#x00A0;dataset
</pre>
<!--l. 788--><p class="nopar" > <!--l. 789-->
<div class="lstlisting" id="listing-21"><span class="label"><a 
 id="x1-13032r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Remove</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">rows</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">containing</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NaN</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">values</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13033r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ds_complete_</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">append</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">X</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13034r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ds_complete_</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ds_complete_</span><span 
class="cmtt-9">[~</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">isnan</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">ds_complete_</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">any</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">axis</span><span 
class="cmtt-9">=1)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">:]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13035r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ds_complete_</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ds_complete_</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">ds_complete_</span><span 
class="cmtt-9">[:,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-1]!=-1]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13036r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13037r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">X</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">delete</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">ds_complete_</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13038r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ds_complete_</span><span 
class="cmtt-9">[:,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-1]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13039r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13040r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">rows_with_NaN</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">X</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">isnan</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">X</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">any</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">axis</span><span 
class="cmtt-9">=1)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">:])</span><span 
class="cmtt-9">[0]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13041r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">labels_NaN</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">==-1])</span><span 
class="cmtt-9">[0]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13042r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13043r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">After</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cleaning</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">there</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">are</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{:.0</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">rows</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">containing</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NaN</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">value</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">features</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dataset</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">format</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">rows_with_NaN</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13044r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">After</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cleaning</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">there</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">are</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{:.0</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">rows</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">containing</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-1</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">label</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">training</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dataset</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">format</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">labels_NaN</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span>
   </div>
                                                                                       
                                                                                       
   <pre class="verbatim" id="verbatim-7">
&#x00A0;&#x00A0;&#x00A0;&#x00A0;After&#x00A0;cleaning,&#x00A0;there&#x00A0;are&#x00A0;0&#x00A0;rows&#x00A0;containing&#x00A0;NaN&#x00A0;value&#x00A0;in&#x00A0;the&#x00A0;features&#x00A0;dataset
&#x00A0;&#x00A0;&#x00A0;&#x00A0;After&#x00A0;cleaning,&#x00A0;there&#x00A0;are&#x00A0;0&#x00A0;rows&#x00A0;containing&#x00A0;-1&#x00A0;in&#x00A0;label&#x00A0;of&#x00A0;the&#x00A0;training&#x00A0;dataset
</pre>
<!--l. 807--><p class="nopar" > <!--l. 808-->
<div class="lstlisting" id="listing-22"><span class="label"><a 
 id="x1-13045r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">X_train</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">X_test</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">y_train</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">y_test</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">train_test_split</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">X</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">test_size</span><span 
class="cmtt-9">=1/5.0,</span><span 
class="cmtt-9">random_state</span><span 
class="cmtt-9">=8)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-13046r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">The</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">training</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dataset</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">contains</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{:.2</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">}%</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">total</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">entries</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">format</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">X_train</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">[0]*100/(</span><span 
class="cmtt-9">X_train</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">[0]+</span><span 
class="cmtt-9">X_test</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">[0])</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span>
   </div>
                                                                                       
                                                                                       
   <pre class="verbatim" id="verbatim-8">
&#x00A0;&#x00A0;&#x00A0;&#x00A0;The&#x00A0;training&#x00A0;dataset&#x00A0;contains&#x00A0;80.00%&#x00A0;of&#x00A0;total&#x00A0;entries.
</pre>
<!--l. 814--><p class="nopar" >
<!--l. 816--><p class="noindent" >
   <h5 class="subsubsectionHead"><span class="titlemark"><span 
class="cmr-9">2.4.2   </span></span> <a 
 id="x1-140002.4.2"></a><span 
class="cmr-9">Train and Test the model</span></h5>
<!--l. 817--><p class="noindent" ><span 
class="cmr-9">The optimal choice of a classifier and the correct parameters heavily depends on the application and the specific case of</span>
<span 
class="cmr-9">interest. In order to optimise these choices, several experiments are now performed, trying to find the best classifier and</span>
<span 
class="cmr-9">tune the parameters to obtain the best results. The choice of the best classifier will be done manually,</span>
<span 
class="cmr-9">exploring the precision and f1-score: a useful function prints the results and the scikit-learn classification</span>
<span 
class="cmr-9">report.</span>
   <!--l. 821-->
<div class="lstlisting" id="listing-23"><span class="label"><a 
 id="x1-14001r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">model_lbls</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14002r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">dt</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Decisio</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Tree</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14003r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">nb</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Gaussian</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Naive</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Bayes</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14004r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">lp</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Linear</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Perceptron</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14005r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14006r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14007r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Set</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">parameters</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">to</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">be</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">explored</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">by</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">grid</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">each</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">classifier</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14008r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">tuned_param_dt</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[{</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">max_depth</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">list</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">12)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">}]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14009r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">tuned_param_nb</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[{</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">var_smoothing</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[10,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1</span><span 
class="cmtt-9">e</span><span 
class="cmtt-9">-1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1</span><span 
class="cmtt-9">e</span><span 
class="cmtt-9">-2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1</span><span 
class="cmtt-9">e</span><span 
class="cmtt-9">-3,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1</span><span 
class="cmtt-9">e</span><span 
class="cmtt-9">-4,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1</span><span 
class="cmtt-9">e</span><span 
class="cmtt-9">-5,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1</span><span 
class="cmtt-9">e</span><span 
class="cmtt-9">-6,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1</span><span 
class="cmtt-9">e</span><span 
class="cmtt-9">-07,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1</span><span 
class="cmtt-9">e</span><span 
class="cmtt-9">-8,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1</span><span 
class="cmtt-9">e</span><span 
class="cmtt-9">-9,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1</span><span 
class="cmtt-9">e</span><span 
class="cmtt-9">-10]}]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14010r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">tuned_param_lp</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[{</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">early_stopping</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">]}]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14011r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14012r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">set</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">models</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">to</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">be</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fitted</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">specifying</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">estimator</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">parameter</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">structure</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14013r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">models</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14014r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">dt</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">Decision</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Tree</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14015r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">estimator</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">DecisionTreeClassifier</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14016r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">param</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">tuned_param_dt</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14017r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">},</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14018r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">nb</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">Gaussian</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Naive</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Bayes</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14019r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">estimator</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">GaussianNB</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14020r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">param</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">tuned_param_nb</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14021r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">},</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14022r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">lp</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">Linear</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Perceptron</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14023r23"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">estimator</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Perceptron</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14024r24"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">param</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">tuned_param_lp</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14025r25"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14026r26"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14027r27"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14028r28"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">scores</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">to</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">be</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">explored</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14029r29"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">scores</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14030r30"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">precision</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14031r31"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">recall</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14032r32"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">]</span>
   </div>
   <!--l. 856-->
<div class="lstlisting" id="listing-24"><span class="label"><a 
 id="x1-14035r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">def</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print_results</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">model</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14036r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Best</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">parameters</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">set</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">found</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">on</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">train</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">set</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14037r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14038r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">if</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">best</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">is</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">linear</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">there</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">is</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">no</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">gamma</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">parameter</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14039r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">model</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">best_params_</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14040r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14041r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Grid</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">scores</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">on</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">train</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">set</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14042r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14043r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">means</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">model</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">cv_results_</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">mean_test_score</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14044r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">stds</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">model</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">cv_results_</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">std_test_score</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14045r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">params</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">model</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">cv_results_</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">params</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14046r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">mean</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">std</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">params_tuple</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">zip</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">means</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">stds</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">params</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14047r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">%0.3</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(+/-%0.03</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">r</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14048r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">mean</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">std</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">*</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">params_tuple</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14049r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14050r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Detailed</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">classification</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">report</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">best</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">parameter</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">set</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14051r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14052r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">The</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">model</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">is</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">trained</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">on</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">full</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">train</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">set</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14053r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">The</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">scores</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">are</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">computed</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">on</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">full</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">test</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">set</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14054r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14055r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y_true</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y_pred</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y_test</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">model</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">predict</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">X_test</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14056r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">classification_report</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">y_true</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y_pred</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14057r23"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">()</span>
   </div>
   <!--l. 881-->
<div class="lstlisting" id="listing-25"><span class="label"><a 
 id="x1-14058r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">results_short</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{}</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14059r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14060r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">score</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">scores</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14061r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">*40)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14062r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Tuning</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">hyper</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">parameters</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">s</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">score</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14063r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14064r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14065r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#8217;%</span><span 
class="cmtt-9">s_macro</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">score</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">##</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">is</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">a</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">string</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">formatting</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">expression</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14066r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">parameter</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">after</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">is</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">substituted</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">string</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">placeholder</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">s</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14067r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">m</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">model_lbls</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14068r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">*40)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14069r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Trying</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">model</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">format</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">models</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">m</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14070r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">clf</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">GridSearchCV</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">models</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">m</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">estimator</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">models</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">m</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">param</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cv</span><span 
class="cmtt-9">=5,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14071r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">scoring</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">s_macro</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">score</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14072r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">iid</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">False</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14073r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">return_train_score</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">False</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14074r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">n_jobs</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">this</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">allows</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">using</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">multi</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">cores</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14075r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14076r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">clf</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">fit</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">X_train</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y_train</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14077r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print_results</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">clf</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14078r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">results_short</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">m</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">clf</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">best_score_</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14079r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Summary</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">of</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">results</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">format</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">score</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14080r23"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Estimator</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14081r24"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">m</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">results_short</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">keys</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14082r25"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">{}\</span><span 
class="cmtt-9">t</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">score</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{:5.2</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">}%</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">format</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">models</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">m</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">results_short</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">m</span><span 
class="cmtt-9">]*100)</span><span 
class="cmtt-9">)</span>
   </div>
                                                                                       
                                                                                       
   <pre class="verbatim" id="verbatim-9">
&#x00A0;&#x00A0;&#x00A0;&#x00A0;========================================
&#x00A0;&#x00A0;&#x00A0;&#x00A0;#&#x00A0;Tuning&#x00A0;hyper-parameters&#x00A0;for&#x00A0;precision

&#x00A0;&#x00A0;&#x00A0;&#x00A0;----------------------------------------
&#x00A0;&#x00A0;&#x00A0;&#x00A0;Trying&#x00A0;model&#x00A0;Decision&#x00A0;Tree
&#x00A0;&#x00A0;&#x00A0;&#x00A0;Best&#x00A0;parameters&#x00A0;set&#x00A0;found&#x00A0;on&#x00A0;train&#x00A0;set:

&#x00A0;&#x00A0;&#x00A0;&#x00A0;{&#8217;max_depth&#8217;:&#x00A0;6}

&#x00A0;&#x00A0;&#x00A0;&#x00A0;Grid&#x00A0;scores&#x00A0;on&#x00A0;train&#x00A0;set:

&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.242&#x00A0;(+/-0.000)&#x00A0;for&#x00A0;{&#8217;max_depth&#8217;:&#x00A0;1}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.433&#x00A0;(+/-0.001)&#x00A0;for&#x00A0;{&#8217;max_depth&#8217;:&#x00A0;2}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.454&#x00A0;(+/-0.003)&#x00A0;for&#x00A0;{&#8217;max_depth&#8217;:&#x00A0;3}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.839&#x00A0;(+/-0.004)&#x00A0;for&#x00A0;{&#8217;max_depth&#8217;:&#x00A0;4}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.809&#x00A0;(+/-0.010)&#x00A0;for&#x00A0;{&#8217;max_depth&#8217;:&#x00A0;5}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.856&#x00A0;(+/-0.012)&#x00A0;for&#x00A0;{&#8217;max_depth&#8217;:&#x00A0;6}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.845&#x00A0;(+/-0.020)&#x00A0;for&#x00A0;{&#8217;max_depth&#8217;:&#x00A0;7}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.847&#x00A0;(+/-0.007)&#x00A0;for&#x00A0;{&#8217;max_depth&#8217;:&#x00A0;8}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.748&#x00A0;(+/-0.009)&#x00A0;for&#x00A0;{&#8217;max_depth&#8217;:&#x00A0;9}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.744&#x00A0;(+/-0.010)&#x00A0;for&#x00A0;{&#8217;max_depth&#8217;:&#x00A0;10}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.740&#x00A0;(+/-0.012)&#x00A0;for&#x00A0;{&#8217;max_depth&#8217;:&#x00A0;11}

&#x00A0;&#x00A0;&#x00A0;&#x00A0;Detailed&#x00A0;classification&#x00A0;report&#x00A0;for&#x00A0;the&#x00A0;best&#x00A0;parameter&#x00A0;set:

&#x00A0;&#x00A0;&#x00A0;&#x00A0;The&#x00A0;model&#x00A0;is&#x00A0;trained&#x00A0;on&#x00A0;the&#x00A0;full&#x00A0;train&#x00A0;set.
&#x00A0;&#x00A0;&#x00A0;&#x00A0;The&#x00A0;scores&#x00A0;are&#x00A0;computed&#x00A0;on&#x00A0;the&#x00A0;full&#x00A0;test&#x00A0;set.

&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;precision&#x00A0;&#x00A0;&#x00A0;&#x00A0;recall&#x00A0;&#x00A0;f1-score&#x00A0;&#x00A0;&#x00A0;support

&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.0&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.79&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.94&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.86&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;85605
&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;1.0&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.57&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.13&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.21&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;6753
&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;2.0&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.62&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.35&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.44&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;24999

&#x00A0;&#x00A0;&#x00A0;&#x00A0;accuracy&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.77&#x00A0;&#x00A0;&#x00A0;&#x00A0;117357
&#x00A0;&#x00A0;&#x00A0;&#x00A0;macro&#x00A0;avg&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.66&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.47&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.51&#x00A0;&#x00A0;&#x00A0;&#x00A0;117357
&#x00A0;&#x00A0;&#x00A0;&#x00A0;weighted&#x00A0;avg&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.74&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.77&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.73&#x00A0;&#x00A0;&#x00A0;&#x00A0;117357


&#x00A0;&#x00A0;&#x00A0;&#x00A0;----------------------------------------
&#x00A0;&#x00A0;&#x00A0;&#x00A0;Trying&#x00A0;model&#x00A0;Gaussian&#x00A0;Naive&#x00A0;Bayes
&#x00A0;&#x00A0;&#x00A0;&#x00A0;Best&#x00A0;parameters&#x00A0;set&#x00A0;found&#x00A0;on&#x00A0;train&#x00A0;set:

&#x00A0;&#x00A0;&#x00A0;&#x00A0;{&#8217;var_smoothing&#8217;:&#x00A0;1}

&#x00A0;&#x00A0;&#x00A0;&#x00A0;Grid&#x00A0;scores&#x00A0;on&#x00A0;train&#x00A0;set:

&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.335&#x00A0;(+/-0.029)&#x00A0;for&#x00A0;{&#8217;var_smoothing&#8217;:&#x00A0;10}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.691&#x00A0;(+/-0.006)&#x00A0;for&#x00A0;{&#8217;var_smoothing&#8217;:&#x00A0;1}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.682&#x00A0;(+/-0.005)&#x00A0;for&#x00A0;{&#8217;var_smoothing&#8217;:&#x00A0;0.1}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.678&#x00A0;(+/-0.005)&#x00A0;for&#x00A0;{&#8217;var_smoothing&#8217;:&#x00A0;0.01}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.676&#x00A0;(+/-0.004)&#x00A0;for&#x00A0;{&#8217;var_smoothing&#8217;:&#x00A0;0.001}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.676&#x00A0;(+/-0.004)&#x00A0;for&#x00A0;{&#8217;var_smoothing&#8217;:&#x00A0;0.0001}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.676&#x00A0;(+/-0.004)&#x00A0;for&#x00A0;{&#8217;var_smoothing&#8217;:&#x00A0;1e-05}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.676&#x00A0;(+/-0.004)&#x00A0;for&#x00A0;{&#8217;var_smoothing&#8217;:&#x00A0;1e-06}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.676&#x00A0;(+/-0.004)&#x00A0;for&#x00A0;{&#8217;var_smoothing&#8217;:&#x00A0;1e-07}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.676&#x00A0;(+/-0.004)&#x00A0;for&#x00A0;{&#8217;var_smoothing&#8217;:&#x00A0;1e-08}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.676&#x00A0;(+/-0.004)&#x00A0;for&#x00A0;{&#8217;var_smoothing&#8217;:&#x00A0;1e-09}
&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.676&#x00A0;(+/-0.004)&#x00A0;for&#x00A0;{&#8217;var_smoothing&#8217;:&#x00A0;1e-10}

                                                                                       
                                                                                       
&#x00A0;&#x00A0;&#x00A0;&#x00A0;Detailed&#x00A0;classification&#x00A0;report&#x00A0;for&#x00A0;the&#x00A0;best&#x00A0;parameter&#x00A0;set:

&#x00A0;&#x00A0;&#x00A0;&#x00A0;The&#x00A0;model&#x00A0;is&#x00A0;trained&#x00A0;on&#x00A0;the&#x00A0;full&#x00A0;train&#x00A0;set.
&#x00A0;&#x00A0;&#x00A0;&#x00A0;The&#x00A0;scores&#x00A0;are&#x00A0;computed&#x00A0;on&#x00A0;the&#x00A0;full&#x00A0;test&#x00A0;set.

&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;precision&#x00A0;&#x00A0;&#x00A0;&#x00A0;recall&#x00A0;&#x00A0;f1-score&#x00A0;&#x00A0;&#x00A0;support

&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.0&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.78&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.95&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.86&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;85605
&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;1.0&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.43&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.20&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.27&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;6753
&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;2.0&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.57&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.24&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.34&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;24999

&#x00A0;&#x00A0;&#x00A0;&#x00A0;accuracy&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.75&#x00A0;&#x00A0;&#x00A0;&#x00A0;117357
&#x00A0;&#x00A0;&#x00A0;&#x00A0;macro&#x00A0;avg&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.59&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.46&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.49&#x00A0;&#x00A0;&#x00A0;&#x00A0;117357
&#x00A0;&#x00A0;&#x00A0;&#x00A0;weighted&#x00A0;avg&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.72&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.75&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.71&#x00A0;&#x00A0;&#x00A0;&#x00A0;117357


&#x00A0;&#x00A0;&#x00A0;&#x00A0;----------------------------------------
&#x00A0;&#x00A0;&#x00A0;&#x00A0;Trying&#x00A0;model&#x00A0;Linear&#x00A0;Perceptron
&#x00A0;&#x00A0;&#x00A0;&#x00A0;Best&#x00A0;parameters&#x00A0;set&#x00A0;found&#x00A0;on&#x00A0;train&#x00A0;set:

&#x00A0;&#x00A0;&#x00A0;&#x00A0;{&#8217;early_stopping&#8217;:&#x00A0;True}

&#x00A0;&#x00A0;&#x00A0;&#x00A0;Grid&#x00A0;scores&#x00A0;on&#x00A0;train&#x00A0;set:

&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.575&#x00A0;(+/-0.163)&#x00A0;for&#x00A0;{&#8217;early_stopping&#8217;:&#x00A0;True}

&#x00A0;&#x00A0;&#x00A0;&#x00A0;Detailed&#x00A0;classification&#x00A0;report&#x00A0;for&#x00A0;the&#x00A0;best&#x00A0;parameter&#x00A0;set:

&#x00A0;&#x00A0;&#x00A0;&#x00A0;The&#x00A0;model&#x00A0;is&#x00A0;trained&#x00A0;on&#x00A0;the&#x00A0;full&#x00A0;train&#x00A0;set.
&#x00A0;&#x00A0;&#x00A0;&#x00A0;The&#x00A0;scores&#x00A0;are&#x00A0;computed&#x00A0;on&#x00A0;the&#x00A0;full&#x00A0;test&#x00A0;set.

&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;precision&#x00A0;&#x00A0;&#x00A0;&#x00A0;recall&#x00A0;&#x00A0;f1-score&#x00A0;&#x00A0;&#x00A0;support

&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.0&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.84&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.99&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.85&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;85605
&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;1.0&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.63&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.01&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.03&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;6753
&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;2.0&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.61&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.06&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.11&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;24999

&#x00A0;&#x00A0;&#x00A0;&#x00A0;accuracy&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.74&#x00A0;&#x00A0;&#x00A0;&#x00A0;117357
&#x00A0;&#x00A0;&#x00A0;&#x00A0;macro&#x00A0;avg&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.69&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.36&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.33&#x00A0;&#x00A0;&#x00A0;&#x00A0;117357
&#x00A0;&#x00A0;&#x00A0;&#x00A0;weighted&#x00A0;avg&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.78&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.74&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;0.64&#x00A0;&#x00A0;&#x00A0;&#x00A0;117357

</pre>
<!--l. 1010--><p class="nopar" >
<!--l. 1012--><p class="indent" >   <span 
class="cmr-9">The training phase was strongly influenced by limitated CPU and memory resources. The obtained results are almost</span>
<span 
class="cmr-9">equivalents for the best parameters in each classifies; among them, Decision Tree classifier was chosen, also for a better</span>
<span 
class="cmr-9">performance in terms of execution time.</span>
   <!--l. 1016-->
<div class="lstlisting" id="listing-26"><span class="label"><a 
 id="x1-14083r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">model</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">DecisionTreeClassifier</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">max_dept</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">6)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-14084r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">model</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">fit</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">X_train</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y_train</span><span 
class="cmtt-9">)</span>
   </div>
<!--l. 1021--><p class="noindent" >
   <h4 class="subsectionHead"><span class="titlemark"><span 
class="cmr-9">2.5   </span></span> <a 
 id="x1-150002.5"></a><span 
class="cmr-9">Validate the model</span></h4>
<!--l. 1023--><p class="noindent" ><span 
class="cmr-9">In order to undestand the behavior of the seleced model, and to increase the value of the classifier, an in depth analyzes is</span>
<span 
class="cmr-9">applied to the classification results.</span>
   <!--l. 1026-->
<div class="lstlisting" id="listing-27"><span class="label"><a 
 id="x1-15001r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Predict</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">test</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">labels</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15002r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y_test_predicted</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">model</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">predict</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">X_test</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15003r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">class_labels</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">unique</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">y_test</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15004r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">class_names</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">land</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">snow</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">ice</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cloud</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15005r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">in1d</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">y_test_predicted</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y_test</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15006r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">predictions</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y_test_predicted</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15007r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">true_labels</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y_test</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15008r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15009r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Extract</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">display</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">metrics</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15010r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f1_scores</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">metrics</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">f1_score</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">true_labels</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">predictions</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">labels</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">class_labels</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">average</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">None</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15011r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">avg_f1_score</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">metrics</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">f1_score</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">true_labels</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">predictions</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">average</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">weighted</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15012r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">recall</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">metrics</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">recall_score</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">true_labels</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">predictions</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">labels</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">class_labels</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">average</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">None</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15013r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">precision</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">metrics</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">precision_score</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">true_labels</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">predictions</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">labels</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">class_labels</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">average</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">None</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15014r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">accuracy</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">metrics</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">accuracy_score</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">true_labels</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">predictions</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15015r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15016r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Classification</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">accuracy</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{:.1</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">}%</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">format</span><span 
class="cmtt-9">(100</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">*</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">accuracy</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15017r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Classification</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">F1</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">score</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{:.1</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">}%</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">format</span><span 
class="cmtt-9">(100</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">*</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">avg_f1_score</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15018r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15019r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Class</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">F1</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">|</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Recall</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">|</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Precision</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15020r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">--------------------------------------------------</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15021r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lulctype</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">enumerate</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">class_names</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">len</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">class_labels</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15022r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">line_data</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">lulctype</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f1_scores</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">*</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">100,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">recall</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">*</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">100,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">precision</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">*</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">100)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15023r23"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">print</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">*</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{0:20</span><span 
class="cmtt-9">s</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{1:2.1</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">|</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{2:2.1</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">|</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{3:2.1</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">format</span><span 
class="cmtt-9">(*</span><span 
class="cmtt-9">line_data</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span>
   </div>
                                                                                       
                                                                                       
   <pre class="verbatim" id="verbatim-10">
&#x00A0;&#x00A0;&#x00A0;&#x00A0;Classification&#x00A0;accuracy&#x00A0;84.2%
&#x00A0;&#x00A0;&#x00A0;&#x00A0;Classification&#x00A0;F1-score&#x00A0;79.0%

&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;Class&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;=&#x00A0;&#x00A0;F1&#x00A0;&#x00A0;|&#x00A0;Recall&#x00A0;|&#x00A0;Precision
&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;--------------------------------------------------
&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;*&#x00A0;land&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;=&#x00A0;86.9&#x00A0;|&#x00A0;&#x00A0;93.1&#x00A0;&#x00A0;|&#x00A0;81.4
&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;*&#x00A0;snow&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;=&#x00A0;54.4&#x00A0;|&#x00A0;&#x00A0;24.6&#x00A0;&#x00A0;|&#x00A0;56.9
&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;*&#x00A0;ice&#x00A0;cloud&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;&#x00A0;=&#x00A0;70.2&#x00A0;|&#x00A0;&#x00A0;41.7&#x00A0;&#x00A0;|&#x00A0;63.1
</pre>
<!--l. 1060--><p class="nopar" >
<!--l. 1062--><p class="indent" >   <span 
class="cmr-9">Confusion matrices are a very expresive instrument about the model performance. They show the number of correctly</span>
<span 
class="cmr-9">and incorrectly predicted labels for each label from the reference map or vice versa. This shows if the classifier has a bias</span>
<span 
class="cmr-9">towards wrongly classifying certain types of land cover.</span>
   <!--l. 1066-->
<div class="lstlisting" id="listing-28"><span class="label"><a 
 id="x1-15024r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Define</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plotting</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">function</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15025r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">def</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plot_confusion_matrix</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15026r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">confusion_matrix</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15027r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">classes</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15028r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">normalize</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">False</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15029r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">title</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Confusion</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">matrix</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15030r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cmap</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">cm</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">Blues</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15031r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ylabel</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">label</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15032r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">xlabel</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Predicted</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">label</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15033r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">filename</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">None</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15034r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15035r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"""</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15036r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">This</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">function</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">prints</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plots</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">confusion</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">matrix</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15037r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Normalization</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">can</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">be</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">applied</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">by</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">setting</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8216;</span><span 
class="cmtt-9">normalize</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">&#8216;.</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15038r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"""</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15039r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_printoptions</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">precision</span><span 
class="cmtt-9">=2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">suppress</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15040r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15041r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">if</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">normalize</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15042r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">normalisation_factor</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">confusion_matrix</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">sum</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">axis</span><span 
class="cmtt-9">=1)</span><span 
class="cmtt-9">[:,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">newaxis</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">finfo</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">float</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">eps</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15043r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">confusion_matrix</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">confusion_matrix</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">astype</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">float</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">/</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">normalisation_factor</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15044r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15045r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">imshow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">confusion_matrix</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interpolation</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">nearest</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cmap</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">cmap</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">vmin</span><span 
class="cmtt-9">=0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">vmax</span><span 
class="cmtt-9">=1)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15046r23"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">title</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">title</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fontsize</span><span 
class="cmtt-9">=20)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15047r24"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">tick_marks</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">arange</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">len</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">classes</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15048r25"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">xticks</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">tick_marks</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">classes</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">rotation</span><span 
class="cmtt-9">=90,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fontsize</span><span 
class="cmtt-9">=20)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15049r26"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">yticks</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">tick_marks</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">classes</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fontsize</span><span 
class="cmtt-9">=20)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15050r27"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15051r28"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fmt</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">.2</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">if</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">normalize</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">else</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">d</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15052r29"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">threshold</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">confusion_matrix</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">max</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">/</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2.0</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15053r30"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">j</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">itertools</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">product</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">confusion_matrix</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">[0])</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">confusion_matrix</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">[1])</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15054r31"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">text</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15055r32"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">j</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15056r33"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15057r34"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">format</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">confusion_matrix</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">j</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fmt</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15058r35"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">horizontalalignment</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">center</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15059r36"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">color</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">white</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">if</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">confusion_matrix</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">j</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x003E;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">threshold</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">else</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">black</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15060r37"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fontsize</span><span 
class="cmtt-9">=12,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15061r38"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15062r39"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15063r40"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">tight_layout</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15064r41"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">ylabel</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">ylabel</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fontsize</span><span 
class="cmtt-9">=20)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15065r42"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">xlabel</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">xlabel</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fontsize</span><span 
class="cmtt-9">=20)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15066r43"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15067r44"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">figure</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">figsize</span><span 
class="cmtt-9">=(20,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">20)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15068r45"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15069r46"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplot</span><span 
class="cmtt-9">(1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15070r47"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">confusion_matrix_gbm</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">metrics</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">confusion_matrix</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">true_labels</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">predictions</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15071r48"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plot_confusion_matrix</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15072r49"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">confusion_matrix_gbm</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15073r50"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">classes</span><span 
class="cmtt-9">=[</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">enumerate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">class_names</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">if</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">class_labels</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15074r51"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">normalize</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15075r52"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ylabel</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Truth</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">LAND</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">COVER</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15076r53"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">xlabel</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Predicted</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">GBM</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15077r54"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">title</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Confusion</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">matrix</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15078r55"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15079r56"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15080r57"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplot</span><span 
class="cmtt-9">(1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15081r58"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">confusion_matrix_gbm</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">metrics</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">confusion_matrix</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">predictions</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">true_labels</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15082r59"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plot_confusion_matrix</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15083r60"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">confusion_matrix_gbm</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15084r61"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">classes</span><span 
class="cmtt-9">=[</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">enumerate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">class_names</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">if</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">class_labels</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15085r62"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">normalize</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15086r63"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">xlabel</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Truth</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">LAND</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">COVER</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15087r64"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ylabel</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Predicted</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">GBM</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15088r65"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">title</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Transposed</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Confusion</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">matrix</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15089r66"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15090r67"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15091r68"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">tight_layout</span><span 
class="cmtt-9">()</span>
   </div>
<!--l. 1137--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                       
                                                                                       
<a 
 id="x1-15092r9"></a>
                                                                                       
                                                                                       
<!--l. 1139--><p class="noindent" ><img 
src="vertopal_24a2006fe83f4b7aa33b81a457a028ff/d55a85cf8e245ead0bb2714c13525a7685168a0a.png" alt="PIC"  
width="341" height="170" >
<br /> <div class="caption" 
><span class="id">Figure&#x00A0;9: </span><span  
class="content">Confusion Matrix for the model</span></div><!--tex4ht:label?: x1-15092r9 -->
                                                                                       
                                                                                       
<!--l. 1141--><p class="indent" >   </div><hr class="endfigure">
<!--l. 1143--><p class="indent" >   <span 
class="cmr-9">The ROC curve shows the diagnostic ability of a classifier as its discrimination threshold is varied: indeed the</span>
<span 
class="cmr-9">threshold for the prediction of a certain label can be manipulated. The x-axis shows the false positive rate (we want it to</span>
<span 
class="cmr-9">be small), and the y-axis shows the true positive rate (we want it to be large) at different thresholds. Good classifier</span>
<span 
class="cmr-9">performance is characterised by a curve, which has a large integral value, also known as the area under curve (AUC).</span>
<span 
class="cmr-9">The snow labels ROC curve is shown in the graph: the curve has not the expected trend, symptom of</span>
<span 
class="cmr-9">a not optimal classifier. The snow classifictaion, probably, resents of an under-representation in the the</span>
<span 
class="cmr-9">dataset.</span>
   <!--l. 1150-->
<div class="lstlisting" id="listing-29"><span class="label"><a 
 id="x1-15093r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">scores_test</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">model</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">predict_proba</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">X_test</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15094r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">labels_binarized</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">preprocessing</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">label_binarize</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">y_test</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">classes</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">class_labels</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15095r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15096r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fpr</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">tpr</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">roc_auc</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{},</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{},</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{}</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15097r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15098r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lbl</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">enumerate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">class_labels</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15099r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fpr</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">tpr</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">_</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">metrics</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">roc_curve</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">labels_binarized</span><span 
class="cmtt-9">[:,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-1],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">scores_test</span><span 
class="cmtt-9">[:,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-1])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15100r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">roc_auc</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">metrics</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">auc</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">fpr</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">tpr</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">])</span>
   </div>
<!--l. 1160--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                       
                                                                                       
<a 
 id="x1-15101r10"></a>
                                                                                       
                                                                                       
<!--l. 1162--><p class="noindent" ><img 
src="vertopal_24a2006fe83f4b7aa33b81a457a028ff/cfc45cd24d08e722a0d380c2a2fb9d2b0c73459a.png" alt="PIC"  
width="284" height="199" >
<br /> <div class="caption" 
><span class="id">Figure&#x00A0;10: </span><span  
class="content">ROC curve</span></div><!--tex4ht:label?: x1-15101r10 -->
                                                                                       
                                                                                       
<!--l. 1164--><p class="indent" >   </div><hr class="endfigure">
<!--l. 1166--><p class="indent" >   <span 
class="cmr-9">Working with maps and images, the best validation method is probably visualization. For each pixel the</span>
<span 
class="cmr-9">defined model has to be applied, in order to obtain a new map that defines areas with snow, land and cloud.</span>
<br 
class="newline" /><span 
class="cmr-9">The following function computes the map and adds it to the eo-learn dataset.</span>
   <!--l. 1170-->
<div class="lstlisting" id="listing-30"><span class="label"><a 
 id="x1-15102r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">focus_list</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15103r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sample_path</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">EOPATCH_SAMPLES_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15104r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">sample_path</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lazy_loading</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15105r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15106r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">input_data</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">concatenate</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">FEATURES</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15107r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">t</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">w</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">h</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">l</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">input_data</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15108r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">input_data</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">input_data</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">reshape</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">t</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">*</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">w</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">*</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">h</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">l</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15109r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y_predicted</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">model</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">predict</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">input_data</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15110r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15111r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">LABEL_PREDICTED</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y_predicted</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">reshape</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">t</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">w</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">h</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15112r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15113r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">save</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">RESULTS_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">overwrite_permission</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">OverwritePermission</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">OVERWRITE_PATCH</span><span 
class="cmtt-9">)</span>
   </div>
<!--l. 1185--><p class="indent" >   <span 
class="cmr-9">The map of a generic winter day is visualized with the following code lines: the color map </span><span 
class="cmti-9">SNOW</span>_<span 
class="cmti-9">CLOUD</span>_<span 
class="cmti-9">MAP</span>
<span 
class="cmr-9">defines land areas as </span><span 
class="cmti-9">green</span><span 
class="cmr-9">, snow areas as </span><span 
class="cmti-9">white </span><span 
class="cmr-9">and cloud area as </span><span 
class="cmti-9">red</span><span 
class="cmr-9">.</span>
   <!--l. 1188-->
<div class="lstlisting" id="listing-31"><span class="label"><a 
 id="x1-15114r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">class</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SNOW_CLOUD_MAP</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">MultiValueEnum</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15115r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"""</span><span 
class="cmtt-9">Enum</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">class</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">containing</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">basic</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">LULC</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">types</span><span 
class="cmtt-9">"""</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15116r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NO_SNOW</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Land</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">#0</span><span 
class="cmtt-9">DAE26</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15117r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SNOW_AND_ICE</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Snow</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Ice</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">ffffff</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15118r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">CLOUD</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">cloud</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">ff0000</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15119r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">@property</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15120r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">def</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">id</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15121r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">return</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">values</span><span 
class="cmtt-9">[1]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15122r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">@property</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15123r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">def</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">color</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15124r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">return</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">values</span><span 
class="cmtt-9">[2]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15125r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15126r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Reference</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">colormap</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">things</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15127r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_cloud_cmap</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ListedColormap</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">color</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SNOW_CLOUD_MAP</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">snow_cloud_cmap</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15128r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_cloud_norm</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">BoundaryNorm</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0.5</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">len</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">SNOW_CLOUD_MAP</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1)</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_cloud_cmap</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">N</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15129r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15130r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">#####################################################################################################################</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15131r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15132r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">axs</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplots</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">nrows</span><span 
class="cmtt-9">=4,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ncols</span><span 
class="cmtt-9">=6,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">figsize</span><span 
class="cmtt-9">=(20,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">15)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15133r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15134r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">date</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">datetime</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">datetime</span><span 
class="cmtt-9">(2020,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">29)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15135r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15136r23"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">patchID</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">enumerate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">focus_list</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15137r24"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch_path</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">RESULTS_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">patchID</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15138r25"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch_path</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lazy_loading</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15139r26"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15140r27"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dates</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">array</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">replace</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">tzinfo</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">None</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15141r28"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">argsort</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">abs</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">date</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dates</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">[0]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15142r29"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15143r30"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">axs</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">//</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">6][</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">6]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15144r31"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">imshow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">clip</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">BANDS</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">][...,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0]]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">*</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">3.5,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15145r32"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">imshow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">LABEL_PREDICTED</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">].</span><span 
class="cmtt-9">astype</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">float</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cmap</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_cloud_cmap</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15146r33"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15147r34"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_xticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15148r35"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_yticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15149r36"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_aspect</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">auto</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15150r37"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">del</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15151r38"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15152r39"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplots_adjust</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">wspace</span><span 
class="cmtt-9">=0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">hspace</span><span 
class="cmtt-9">=0)</span>
   </div>
<!--l. 1230--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                       
                                                                                       
<a 
 id="x1-15153r11"></a>
                                                                                       
                                                                                       
<!--l. 1232--><p class="noindent" ><img 
src="vertopal_24a2006fe83f4b7aa33b81a457a028ff/mappa_2.png" alt="PIC"  
width="341" height="284" >
<br /> <div class="caption" 
><span class="id">Figure&#x00A0;11: </span><span  
class="content">Snow (white) and Cloud (red) prediction</span></div><!--tex4ht:label?: x1-15153r11 -->
                                                                                       
                                                                                       
<!--l. 1234--><p class="indent" >   </div><hr class="endfigure">
<!--l. 1236--><p class="indent" >   <span 
class="cmr-9">Even more significant could be a comparison between official snow cover data with automatically classified</span>
<span 
class="cmr-9">data.</span>
   <!--l. 1238-->
<div class="lstlisting" id="listing-32"><span class="label"><a 
 id="x1-15154r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">figure</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">figsize</span><span 
class="cmtt-9">=(20,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">20)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15155r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15156r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">random</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">choice</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">focus_list</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15157r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">inspect_size</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">100</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15158r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15159r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">RESULTS_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">idx</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lazy_loading</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15160r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15161r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">date</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">datetime</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">datetime</span><span 
class="cmtt-9">(2020,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">29)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15162r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dates</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">array</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">replace</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">tzinfo</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">None</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15163r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">argsort</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">abs</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">date</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dates</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">[0]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15164r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15165r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">t</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">p</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">LABEL_PREDICTED</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">].</span><span 
class="cmtt-9">shape</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15166r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15167r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">w_min</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">random</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">choice</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">y</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">inspect_size</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15168r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">w_max</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">w_min</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">inspect_size</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15169r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">h_min</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">random</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">choice</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">inspect_size</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15170r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">h_max</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">h_min</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">inspect_size</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15171r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15172r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplot</span><span 
class="cmtt-9">(2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15173r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">imshow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">LABEL_PREDICTED</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">w_min</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">w_max</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">h_min</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">h_max</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cmap</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">lulc_cmap</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">norm</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">lulc_norm</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15174r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">xticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15175r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">yticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15176r23"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_aspect</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">auto</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15177r24"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">title</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Ground</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Truth</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fontsize</span><span 
class="cmtt-9">=20)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15178r25"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15179r26"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplot</span><span 
class="cmtt-9">(2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15180r27"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">imshow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">LABEL</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">w_min</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">w_max</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">h_min</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">h_max</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cmap</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">lulc_cmap</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">norm</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">lulc_norm</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15181r28"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">xticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15182r29"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">yticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15183r30"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_aspect</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">auto</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15184r31"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">title</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Prediction</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fontsize</span><span 
class="cmtt-9">=20)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15185r32"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15186r33"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplot</span><span 
class="cmtt-9">(2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">3)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15187r34"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">LABEL_PREDICTED</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">!=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">LABEL</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15188r35"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">imshow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">mask</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">w_min</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">w_max</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">h_min</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">h_max</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cmap</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">gray</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15189r36"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">xticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15190r37"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">yticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15191r38"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_aspect</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">auto</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15192r39"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">title</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Difference</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fontsize</span><span 
class="cmtt-9">=20)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15193r40"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15194r41"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplot</span><span 
class="cmtt-9">(2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">4)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15195r42"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">image</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">clip</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">FEATURES</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">][...,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0]]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">*</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">3.5,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15196r43"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">imshow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">image</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">w_min</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">w_max</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">h_min</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">h_max</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15197r44"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">xticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15198r45"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">yticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15199r46"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_aspect</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">auto</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15200r47"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">title</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Color</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fontsize</span><span 
class="cmtt-9">=20)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15201r48"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-15202r49"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplots_adjust</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">wspace</span><span 
class="cmtt-9">=0.1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">hspace</span><span 
class="cmtt-9">=0.1)</span>
   </div>
<!--l. 1289--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                       
                                                                                       
<a 
 id="x1-15203r12"></a>
                                                                                       
                                                                                       
<!--l. 1291--><p class="noindent" ><img 
src="vertopal_24a2006fe83f4b7aa33b81a457a028ff/differenze_2.png" alt="PIC"  
width="398" height="398" >
<br /> <div class="caption" 
><span class="id">Figure&#x00A0;12: </span><span  
class="content">A comparison between ground truth data and predicted data.</span></div><!--tex4ht:label?: x1-15203r12 -->
                                                                                       
                                                                                       
<!--l. 1293--><p class="indent" >   </div><hr class="endfigure">
   <h4 class="subsectionHead"><span class="titlemark"><span 
class="cmr-9">2.6   </span></span> <a 
 id="x1-160002.6"></a><span 
class="cmr-9">Visualization</span></h4>
<!--l. 1297--><p class="noindent" ><span 
class="cmr-9">Data visualization is an important part of data science: it can help the data interpretation, make data more</span>
<span 
class="cmr-9">undestandable, allowing a view on different levels, and integrate human knowledge to slim data insight. In the specific</span>
<span 
class="cmr-9">case of the project, working with maps and geographical images, data visualization is an integrated part of the</span>
<span 
class="cmr-9">classification process, needed for reading the results. </span><br 
class="newline" /><span 
class="cmr-9">The consultation screen will contains all the relevant information to have a clear reference in space and in time of the</span>
<span 
class="cmr-9">snow coverage of the AOI.</span>
     <ul class="itemize1">
     <li class="itemize"><span 
class="cmbx-9">A bar graph </span><span 
class="cmr-9">shows the amount of snow among the time, to have a rapid view on periods with more snow</span>
     <span 
class="cmr-9">coverage;</span>
     </li>
     <li class="itemize"><span 
class="cmbx-9">A map </span><span 
class="cmr-9">shows the details of snow coverage for a single day;</span>
     </li>
     <li class="itemize"><span 
class="cmbx-9">Interactive controls </span><span 
class="cmr-9">allows the selection of a specific day for the detailed visualization on the map;</span>
     <span 
class="cmr-9">different modality of visualization are allowed, with the possibility to view the snow coverage, the cloud</span>
     <span 
class="cmr-9">coverage and both the coverages.</span></li></ul>
<!--l. 1309--><p class="indent" >   <span 
class="cmr-9">The following functions create a dictionary that relates the amount of snow for each day of the year.</span>
   <!--l. 1311-->
<div class="lstlisting" id="listing-33"><span class="label"><a 
 id="x1-16001r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day_list</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16002r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">focus_list</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16003r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sample_path</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">RESULTS_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16004r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">sample_path</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lazy_loading</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16005r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day_list</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">append</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16006r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">del</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16007r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day_list</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">concatenate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">day_list</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">;</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16008r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_amount</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">{}</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16009r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day_list</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16010r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16011r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">daily_amount</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16012r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">focus_list</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16013r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sample_path</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">RESULTS_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">box</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16014r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">sample_path</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lazy_loading</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16015r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16016r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dates</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">array</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">replace</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">tzinfo</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">None</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16017r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">argsort</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">abs</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">day</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dates</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">[0]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16018r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16019r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">daily_amount</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">+=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">mask_timeless</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">REAL_DATA_SNOW_COUNT</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">][0][0].</span><span 
class="cmtt-9">astype</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">float</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16020r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_amount</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">update</span><span 
class="cmtt-9">({</span><span 
class="cmtt-9">day</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">strftime</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">daily_amount</span><span 
class="cmtt-9">})</span>
   </div>
<!--l. 1333--><p class="indent" >   <span 
class="cmr-9">New color maps are defined, to meet the visualization modality specifics. </span><!--l. 1334-->
<div class="lstlisting" id="listing-34"><span class="label"><a 
 id="x1-16021r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">class</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SNOW_MAP</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">MultiValueEnum</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16022r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"""</span><span 
class="cmtt-9">Enum</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">class</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">containing</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">basic</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">LULC</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">types</span><span 
class="cmtt-9">"""</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16023r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NO_SNOW</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Land</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">#0</span><span 
class="cmtt-9">DAE26</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16024r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SNOW_AND_ICE</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Snow</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Ice</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">ffffff</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16025r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">CLOUD</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">cloud</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">#0</span><span 
class="cmtt-9">DAE25</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16026r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">@property</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16027r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">def</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">id</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16028r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">return</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">values</span><span 
class="cmtt-9">[1]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16029r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">@property</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16030r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">def</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">color</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16031r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">return</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">self</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">values</span><span 
class="cmtt-9">[2]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16032r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16033r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Reference</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">colormap</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">things</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16034r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_cmap</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ListedColormap</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">color</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SNOW_MAP</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">snow_cmap</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16035r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_norm</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">BoundaryNorm</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0.5</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">len</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">SNOW_MAP</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1)</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_cmap</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">N</span><span 
class="cmtt-9">)</span>
   </div>
   <!--l. 1351-->
<div class="lstlisting" id="listing-35"><span class="label"><a 
 id="x1-16036r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">class</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">CLOUD_MAP</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">MultiValueEnum</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16037r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NO_SNOW</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Land</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">#0</span><span 
class="cmtt-9">DAE26</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16038r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SNOW_AND_ICE</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Snow</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Ice</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">#0</span><span 
class="cmtt-9">DAE25</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16039r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">CLOUD</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">cloud</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">ff0000</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16040r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">@property</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16041r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">...</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16042r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">class</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SNOW_CLOUD_MAP</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">MultiValueEnum</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16043r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16044r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">NO_SNOW</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Land</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">#0</span><span 
class="cmtt-9">DAE26</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16045r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SNOW_AND_ICE</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">Snow</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">and</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Ice</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">ffffff</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16046r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">CLOUD</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">cloud</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">2,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">ff0000</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16047r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">@property</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16048r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">...</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16049r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16050r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cloud_cmap</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ListedColormap</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">color</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">CLOUD_MAP</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">cloud_cmap</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16051r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cloud_norm</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">BoundaryNorm</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0.5</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">len</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">CLOUD_MAP</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1)</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cloud_cmap</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">N</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16052r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_cloud_cmap</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ListedColormap</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">color</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">SNOW_CLOUD_MAP</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">name</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">snow_cloud_cmap</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16053r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_cloud_norm</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">BoundaryNorm</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">0.5</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">len</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">SNOW_CLOUD_MAP</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">1)</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_cloud_cmap</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">N</span><span 
class="cmtt-9">)</span>
   </div>
<!--l. 1372--><p class="indent" >   <span 
class="cmr-9">To make the Visualization application interactive, the bokeh package was chosen: bokeh is an open source, flexible and</span>
<span 
class="cmr-9">interactive library, that easily allows to create graphs and controls (</span><span 
class="cmbx-9">?</span><span 
class="cmr-9">).</span><br 
class="newline" /><!--l. 1374-->
<div class="lstlisting" id="listing-36"><span class="label"><a 
 id="x1-16054r1"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">from</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">tkinter</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">import</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">colorchooser</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16055r2"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">from</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ipywidgets</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">import</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interact</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16056r3"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">import</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">matplotlib</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">image</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">as</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">mpimg</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16057r4"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">from</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bokeh</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">io</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">import</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">output_notebook</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">show</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">push_notebook</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16058r5"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">from</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bokeh</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">models</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">widgets</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">import</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Div</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16059r6"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">from</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bokeh</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">application</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">import</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Application</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16060r7"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">from</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">bokeh</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">application</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">handlers</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">import</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">FunctionHandler</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16061r8"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16062r9"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">makedirs</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">RESULTS_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">images</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">exist_ok</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16063r10"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">output_notebook</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16064r11"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16065r12"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">desc</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Div</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">text</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">open</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">description</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">html</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">read</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sizing_mode</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">stretch_width</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16066r13"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16067r14"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">#</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Create</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Column</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Data</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Source</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">that</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">will</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">be</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">used</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">by</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plot</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16068r15"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">source</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ColumnDataSource</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">dict</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">date</span><span 
class="cmtt-9">=[</span><span 
class="cmtt-9">d</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">d</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_amount</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">keys</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">amount</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">v</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">v</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_amount</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">values</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">colors</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">green</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">len</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">snow_amount</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">keys</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16069r16"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">k</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">k</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_amount</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">keys</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16070r17"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16071r18"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">p</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">figure</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">x_range</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">FactorRange</span><span 
class="cmtt-9">(*</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plot_height</span><span 
class="cmtt-9">=300,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plot_width</span><span 
class="cmtt-9">=1000,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">title</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">toolbar_location</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">None</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">tools</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16072r19"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">p</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">xaxis</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">major_label_orientation</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">vertical</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16073r20"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">p</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">vbar</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">date</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">top</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">amount</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">width</span><span 
class="cmtt-9">=0.9,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">source</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">source</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">color</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">colors</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16074r21"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16075r22"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">image</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Div</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">text</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sizing_mode</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">stretch_width</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16076r23"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16077r24"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">def</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">update</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">day</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">modality</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16078r25"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day_selected</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">enumerate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">day_list</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16079r26"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">if</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day_selected</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">strftime</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">==</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16080r27"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">break</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16081r28"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16082r29"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">axs</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">plt</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplots</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">nrows</span><span 
class="cmtt-9">=4,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ncols</span><span 
class="cmtt-9">=6,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">figsize</span><span 
class="cmtt-9">=(15,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">10)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">;</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16083r30"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16084r31"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">patchID</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">enumerate</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">focus_list</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16085r32"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch_path</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">RESULTS_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">f</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">eopatch_</span><span 
class="cmtt-9">{</span><span 
class="cmtt-9">patchID</span><span 
class="cmtt-9">}</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16086r33"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">EOPatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">load</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch_path</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">lazy_loading</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16087r34"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16088r35"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dates</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">array</span><span 
class="cmtt-9">([</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">replace</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">tzinfo</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">None</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">timestamp</span><span 
class="cmtt-9">])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16089r36"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">np</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">argsort</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">abs</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">day_selected</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">-</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dates</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">[0]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16090r37"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16091r38"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">axs</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">//</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">6][</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">6]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16092r39"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">if</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">modality</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">==</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">snow</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16093r40"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">imshow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">LABEL_PREDICTED</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">].</span><span 
class="cmtt-9">astype</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">float</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cmap</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_cmap</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">;</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16094r41"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">elif</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">modality</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">==</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">cloud</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16095r42"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">imshow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">LABEL_PREDICTED</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">].</span><span 
class="cmtt-9">astype</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">float</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cmap</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cloud_cmap</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">;</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16096r43"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">elif</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">modality</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">==</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">snow</span><span 
class="cmtt-9">&amp;</span><span 
class="cmtt-9">cloud</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16097r44"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">imshow</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">LABEL_PREDICTED</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">][</span><span 
class="cmtt-9">closest_date_id</span><span 
class="cmtt-9">].</span><span 
class="cmtt-9">astype</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">float</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">cmap</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_cloud_cmap</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">;</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16098r45"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16099r46"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_xticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16100r47"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_yticks</span><span 
class="cmtt-9">([])</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16101r48"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">ax</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">set_aspect</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">auto</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16102r49"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">del</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">eopatch</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16103r50"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">subplots_adjust</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">wspace</span><span 
class="cmtt-9">=0,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">hspace</span><span 
class="cmtt-9">=0)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16104r51"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">fig</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">savefig</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">RESULTS_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">images</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">temp_image</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">png</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16105r52"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16106r53"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">p</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">title</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">text</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">modality</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">map</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">the</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day</span><span 
class="cmtt-9">:</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">+</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">str</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">day</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16107r54"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">color_selected</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">green</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">i</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">range</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">len</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">snow_amount</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">keys</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16108r55"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">color_selected</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">index</span><span 
class="cmtt-9">]</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">red</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16109r56"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">source</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">data</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">dict</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16110r57"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">date</span><span 
class="cmtt-9">=[</span><span 
class="cmtt-9">d</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">d</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_amount</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">keys</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16111r58"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">amount</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">v</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">v</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">snow_amount</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">values</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16112r59"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">colors</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">color_selected</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16113r60"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16114r61"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16115r62"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">image</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">Div</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">text</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">open</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">RESULTS_FOLDER</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">os</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">path</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">join</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">images</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">temp_image</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">png</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">encoding</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">utf8</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">errors</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">ignore</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">read</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">sizing_mode</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">stretch_width</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16116r63"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">push_notebook</span><span 
class="cmtt-9">()</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16117r64"></a></span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16118r65"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">show</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">column</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">desc</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">p</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">image</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">notebook_handle</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">True</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><br /><span class="label"><a 
 id="x1-16119r66"></a></span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">interact</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">update</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">day</span><span 
class="cmtt-9">.</span><span 
class="cmtt-9">strftime</span><span 
class="cmtt-9">(</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">%</span><span 
class="cmtt-9">x</span><span 
class="cmtt-9">"</span><span 
class="cmtt-9">)</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">for</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">in</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">day_list</span><span 
class="cmtt-9">],</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">modality</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">=</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">[</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">snow</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">cloud</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">,</span><span 
class="cmtt-9">&#x00A0;</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">snow</span><span 
class="cmtt-9">&amp;</span><span 
class="cmtt-9">cloud</span><span 
class="cmtt-9">&#8217;</span><span 
class="cmtt-9">])</span>
   </div>
<!--l. 1444--><p class="indent" >   <hr class="figure"><div class="figure" 
>
                                                                                       
                                                                                       
<a 
 id="x1-16122r13"></a>
                                                                                       
                                                                                       
<!--l. 1446--><p class="noindent" ><img 
src="vertopal_24a2006fe83f4b7aa33b81a457a028ff/Cattura_applicazione.png" alt="PIC"  
width="455" height="540" >
<br /> <div class="caption" 
><span class="id">Figure&#x00A0;13: </span><span  
class="content">Interactive application for prediction visualization</span></div><!--tex4ht:label?: x1-16122r13 -->
                                                                                       
                                                                                       
<!--l. 1449--><p class="indent" >   </div><hr class="endfigure">
   <h4 class="subsectionHead"><span class="titlemark"><span 
class="cmr-9">2.7   </span></span> <a 
 id="x1-170002.7"></a><span 
class="cmr-9">Conclusion</span></h4>
<!--l. 1452--><p class="noindent" ><span 
class="cmr-9">The project described did not fully lead to the expected results due to the low quality and low definition of the</span>
<span 
class="cmr-9">ground truth data. Furthermore, in the chosen area of interest, the Appennini&#8217;s Mountain in the north of</span>
<span 
class="cmr-9">Italy, snow happens to be scarcely represented. More variated data could be obtained considering a larger</span>
<span 
class="cmr-9">temporal scale, but data access on the sentinel hub portal is limited. However, besides a less than optimal</span>
<span 
class="cmr-9">precision and accuracy, the algorithm works and data are accessible intuitively and clearly. The use of el-learn</span>
<span 
class="cmr-9">instrument has been put into practice, integrated with a variety of package for machine learing and data</span>
<span 
class="cmr-9">visualization.</span>
<!--l. 1461--><p class="noindent" >
   <h4 class="subsectionHead"><span class="titlemark"><span 
class="cmr-9">2.8   </span></span> <a 
 id="x1-180002.8"></a><span 
class="cmr-9">Future project</span></h4>
<!--l. 1462--><p class="noindent" ><span 
class="cmr-9">Besides the low quality of the results, snow cover monitoring remains a usefull and full of potential activity. The machine</span>
<span 
class="cmr-9">learining approach on data satellite images, allows a low cost global monitoring on lare time intervals: the potential</span>
<span 
class="cmr-9">insight we can obtain are multiple, with a huge social impact. This project, in particular, can be easily improved and</span>
<span 
class="cmr-9">made more powerful using a larger dataset, with a more balanced data of snow and not-snow in space and time.</span>
<span 
class="cmr-9">The requested amount of data requires an higher computational power, and a larger data exchange: for a</span>
<span 
class="cmr-9">better performance and for avoinding the overhead for data downloading, the application with the machine</span>
<span 
class="cmr-9">learining training phase should be ported on a cloud application. Finally, a more interactive data visualization</span>
<span 
class="cmr-9">application can be easily obtained, eventualy integrating a web client to automatically obtain data from</span>
<span 
class="cmr-9">cloud.</span>
                                                                                       
                                                                                       
<!--l. 1471--><p class="indent" >
                                                                                       
                                                                                       
    
</body></html> 

                                                                                       



