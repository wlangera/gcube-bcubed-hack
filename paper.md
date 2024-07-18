---
title: 'Unveiling ecological dynamics through simulation and visualization of biodiversity data cubes'
tags:
  - simulation
  - data cubes
  - biodiversity
  - B-Cubed
  - Monte-Carlo
  - R package
output:
  pdf_document: default
  word_document: default
  html_document:
    df_print: paged
  rmarkdown::pdf_document:
    fig_caption: yes        
    includes:  
      in_header: header.tex
editor_options:
  markdown:
    wrap: 72
authors:
  - name: Ward Langeraert
    orcid: 0000-0002-5900-8109
    affiliation: 1
  - name: Wissam Barhdadi
    orcid: 0000-0001-9304-3971
    affiliation: 2
  - name: Dimitri Brosens
    orcid: 0000-0002-0846-9116
    affiliation: 1
  - name: Rocìo Cortès
    orcid: 0009-0004-8440-958X
    affiliation: 3
  - name: Peter Desmet
    orcid: 0000-0002-8442-8025
    affiliation: 1
  - name: Michele Di Musciano
    orcid: 0000-0002-3130-7270
    affiliation: 4
  - name: Chandra Earl
    orcid: 0000-0001-9850-882X
    affiliation: 5
  - name: Sanne Govaert
    orcid: 0000-0002-8939-1305
    affiliation: 1
  - name: Pieter Huybrechts
    orcid: 0000-0002-6658-6062
    affiliation: 1
  - name: Matilde Martini
    orcid: 0009-0003-5612-925X
    affiliation: 3
  - name: Arthur Rodrigues
    orcid: 0000-0003-2656-558X
    affiliation: 6
  - name: Annegreet Veeken
    orcid: 0000-0003-4291-5981
    affiliation: 7
  - name: Mukhtar Muhammed Yahaya
    orcid: 0009-0008-9200-0863
    affiliation: 8
  - name: Toon Van Daele
    orcid: 0000-0002-1362-853X
    affiliation: 1
affiliations:
 - name: Research Institute for Nature and Forest (INBO), Havenlaan 88, 1000 Brussels, Belgium
   index: 1
 - name: Department of Data Analysis and Mathematical Modelling, Ghent University, Coupure links 653, 9000 Ghent, Belgium
   index: 2
 - name: Department of Biological, Geological and Environmental Sciences, University of Bologna, Via Irnerio 42, 40126 Bologna, Italy
   index: 3
 - name: Department of Life Health and Environmental Sciences, University of L’Aquila, Via Vetoio 1, 67100 Coppito, Italy
   index: 4
 - name: Department of Natural Sciences, Bernice Pauahi Bishop Museum, 1525 Bernice St, Honolulu, HI 96817, United States 
   index: 5
 - name: Organismal and Evolutionary Biology Research Programme, University of Helsinki, Viikinkaari 1, 00790 Helsinki, Finland
   index: 6
 - name: Copernicus Institute of Sustainable Development, Utrecht University, Princetonlaan 8a, 3584 CB Utrecht, The Netherlands
   index: 7
 - name: Department of Mathematical Sciences, Stellenbosch University, Stellenbosch Central, Stellenbosch, South Africa
   index: 8
date: 18 July 2024
bibliography: paper.bib
authors_short: Langeraert et al.
group: Projects 2+8
event: Hacking Biodiversity Data Cubes for Policy, Brussels, Belgium, 2024
biohackathon_name: Hacking Biodiversity Data Cubes for Policy
biohackathon_url: https://b-cubed.eu/b-cubed-hackathon
biohackathon_location: Brussels, Belgium
---

------------------------------------------------------------------------

\* Corresponding author:
[ward.langeraert\@inbo.be](mailto:ward.langeraert@inbo.be){.email}

#### Keywords:

Simulation, Data cubes, Biodiversity, B-Cubed, Monte-Carlo, R package

------------------------------------------------------------------------

## Abstract


## Introduction
Simulation studies offer numerous benefits due to their ability to mimic real-world scenarios in controlled and customizable environments. Ecosystems and biodiversity data are very complex and involve a multitude of interacting factors. Simulations allow researchers to model and understand the complexity of ecological systems by varying parameters such as spatial and/or temporal clustering, species prevalence, etc.

During the B-Cubed Hackathon (Hacking Biodiversity Data Cubes for Policy), we aimed to create a practical simulation framework for biodiversity data cubes based on Monte Carlo methods (= based on repeated random sampling). This framework is composed of three steps ([Fig. 1](#Figure_1)):

1. The occurrence process: Simulating occurrences of multiple species distributed in a landscape over a temporal scope. This will depend on the **rarity**, which can differ between species and over time, and their **spatial clustering**, which can differ between species. A challenge for this part is to implement a consistent **spatial and temporal autocorrelation** for simulated species trends.
2. The detection process: Simulation of a variety of observation processes can generate actual occurrence datasets. Each species has a different **detection probability**. The detection process will also depend on the **sampling effort** which can be different among spatial and temporal dimensions. We can also assign a spatial uncertainty to each observation.
3. The grid designation process: Based on their spatial uncertainty, occurrences can be designated to grid cells of a larger grid to form a data cube.

The simulation framework can be used to assess multiple research questions under different parameter settings, such as the effect of clustering on occurrence-to-grid designation and the effect of different patterns of missingness on data quality and indicator robustness. Simulation studies can incorporate scenarios with missing data, enabling researchers to assess the impact of data gaps on analyses. Understanding how missing data influences results is crucial for improving data collection strategies and addressing potential biases. With this, the secondary objective of the simulation study is to develop a visualisation tool for the simulated cubes. This tool aims to enhance the understanding of data clustering and missingness within the simulated environment. By creating a visual representation, researchers can effectively analyse and interpret patterns of clustered data as well as identify areas where data is missing. This visualization capability contributes to a more comprehensive exploration of the simulated scenarios, allowing for deeper insights into the behaviour of data within the context of the study.

The B-Cubed Hackathon took place from 2-5 April 2024. This paper describes the methods and results of projects 2+8 during this hackathon unless mentioned otherwise.

![Simulation framework for biodiversity data cubes. An example of three species that differ in rarity, clustering and detection probability/sampling effort.](./figures/visual_proposal.png){#Figure_1
.Figure}

## Materials and Methods
### Technical setup
It was *a priori* decided by the first author to build the simulation framework using the R programming language as an R package, where participants could collaborate efficiently with each other via GitHub (https://github.com/).
A repository for this package was prepared under the name 'simcuber' and a code structure was proposed for the framework (see next section).

### Coding structure
General coding structure of the package was proposed following preparation of the hackathon by the first author.
As indicated in the introduction, the simulation framework and thus the R package can be divided into three different processes related to different variables that depend on *species*, *observation*, *space* and *time*.

1. occurrence process
2. detection process
3. grid designation process

For grid designation, R code was already available as the function `grid_designation()`. The focus of the hackathon was thus on the occurrence and detection processes.

|   Process  |        Variable        |   Dependency  |
|------------|------------------------|---------------|
| occurrence | rarity                 | species, time |
| occurrence | spatial clustering     | species       |
| detection  | detection probability  | species       |
| detection  | sampling effort        | space, time   |
| detection  | spatial uncertainty    | observation   |

The three processes can be described in three main functions respectively `simulate_occurrences()`, `sample_observations()` and `grid_designation()`. These can depend on multiple supporting functions for example per variable mentioned above or for specific subprocesses (e.g. temporal autocorrelation).

Some (pseudo)code and ideas for implementation were provided by the first author for `simulate_occurrences()` and `sample_observations()`:

``` {#Code_1 .r .Code}
simulate_occurrences(
  polygon,
  initial_average_abundance = 50,
  spatial_autocorr = c("random", "clustered", "regular"),
  n_time_points = 10,
  temporal_autocorr = ifelse(time_points ==  1, NA, "random_walk"),
  spatiotemporal_autocorr = NA,
  seed = NA
)
```

- **polygon**:

An sf object with POLYGON geometry indicating the spatial extend to simulate occurrences.

- **initial_average_abundance**:

A positive integer value indicating the average number of occurrences to be simulated within the extend of `polygon` at time point 1. This value will be used as mean of a Poisson distribution ($\lambda$ parameter).

- **spatial_autocorr**:

`"random"`, `"clustered"`, `"regular"` or a numeric value between -1 and 1 representing Moran's I. `"random"` corresponds to 0, `"clustered"` to 0.9 and `"regular"` to -0.9.

- **n_time_points**:

A positive integer value indicating the number of time points to simulate.

- **temporal_autocorr**:

`NA`, `"random_walk"` or a function which generates a trend in abundance over time. Only used if `time_points > 1`. When there are multiple time points and `"random_walk"` is selected, an internal function can be used to create a random walk over time. The user is also free to specify its own function that depends on `initial_average_abundance` and `n_time_points`, e.g. a linearly decreasing trend over time.

- **spatiotemporal_autocorr**:

A numeric value between indicating the strength of spatiotemporal autocorrelation.

- **seed**:

A positive numeric value. The seed for random number generation to make results reproducible. If `NA` (the default), no seed is used.

``` {#Code_2 .r .Code}
sample_observations(
  occurrences,
  detection_probability = 1,
  sampling_bias = c("no_bias", "polygon", "manual"),
  bias_area = NA,
  bias_strength = NA,
  bias_weights = NA,
  coordinate_uncertainty_meters = 25,
  seed = NA
)
```

- **occurrences**:

An sf object with POINT geometry.

- **detection_probability**:

A numeric value between 0 and 1, corresponding to the probability of detection of the species.

- **sampling_bias**:

`"no_bias"`, `"polygon"` or `"manual"`. The method used to generate a sampling bias (cf. the **virtualspecies** package @leroy2016virtualspecies).

  - `"polygon"`: bias the sampling in a polygon. Provide your polygon to `bias_area`. Provide bias strength to `bias_strength`.
  - `"manual"`: bias the sampling manually via a raster. Provide your raster layer in which each cell contains the probability to be sampled to `bias_weights`.

- **bias_area**:

`NA` or an sf object with POLYGON geometry. Only used if `sampling_bias = "polygon"`. The area in which the sampling will be biased.

- **bias_strength**:

`NA` or a positive numeric value. Only used if `sampling_bias = "polygon"`. The strength of the bias to be applied in the biased area (as a multiplier). Above 1, area will be oversampled. Below 1, area will be undersampled. For example, a value of 50 will result in 50 times more samples within the `bias_area` than outside. Conversely, a value of 0.5 will result in half less samples within the `bias_area` than outside.

- **bias_weights**:

`NA` or a raster layer (sf object with POLYGON geometry, or SpatRaster object). Only used if `sampling_bias = "manual"`. The raster of bias weights to be applied to the sampling of occurrences. Higher weights mean a higher probability of sampling. Weights can be numeric values between 0 and 1 or positive integers that will be rescaled to values between 0 and 1.

- **coordinate_uncertainty_meters**:

A positive numeric value or vector with length `nrow(occurrences)` describing the uncertainty in meters around each observation.

- **seed**:

A positive numeric value. The seed for random number generation to make results reproducible. If `NA` (the default), no seed is used.

Finally, we also have the function `add_coordinate_uncertainty()`.

``` {#Code_3 .r .Code}   
add_coordinate_uncertainty(
  occurrences,
  coordinate_uncertainty_meters = 25
)
```

This function is a supporting function for `sample_observations()` to add a `coordinateUncertaintyInMeters` column that should also be openly available in case users simulate observations based on virtual species distributions. This can for example be accomplished using the **virtualspecies** package [@leroy2016virtualspecies]:

1.  Species-environment relationship
    -   `generateSpFromFun()`
    -   `generateSpFromPCA()`
2.  Conversion to presence-absence
    -   `convertToPA()`
    -   introduce distribution bias: `limitDispersal()`
3.  Sample occurrences
    -   `sampleOccurrences()`
4.  Convert to sf object with POINT geometry
    -   `sf::st_as_sf()`
    -   create helper function `virtualspecies_to_sf()`?



### Collaboration and division of tasks
Following the information provided in the previous subsections, four types of tasks were distinguished ([Fig. 2](#Figure_2)).

1. Lowlevel tasks: 

2. Highlevel tasks: 

3. Technical tasks: 

4. Creative tasks: 

![Visualisation of the different types of tasks. See text for explanation.](./figures/task_types.png){#Figure_2 .Figure}

Using a Google Form we got an overview of participants' interest in the different tasks, and an idea where potential problems might arise. Tasks were chosen ... *bespreek icebox silicon valley*

Finally, common guidelines for software development (e.g. related to coding style, function naming and unit testing) were mentioned to ensure efficient collaboration as well as future maintenance and development.

deze citatie:
Huybrechts P, Trekels M, Abraham L, Desmet P (2024). B-Cubed software development guide. https://docs.b-cubed.eu/dev-guide/

## Results
Wat allemaal gedaan tegen einde. Pkgdown website met readme, functies met documentation and examples; repo met code coverage enal

### Using virtual species to cope with real problems
- incorporation of project 8 and framework for virtualspecies



## Discussion


## Conclusions and future work


## Links to software
-gcube repo
-Commit meegeven van einde hackathon


## Acknowledgements
We would like to express our gratitude to the Horizon Europe funded B-Cubed (Biodiversity Building Blocks for policy) project for the organisation of this hackathon.
Special thanks go to Laura Abraham of Meise Botanic Garden for her outstanding efforts in coordinating the event.
Additionally, we acknowledge the Research Foundation - Flanders (FWO) and KU Leuven for the support they gave us in making this event possible.

## References