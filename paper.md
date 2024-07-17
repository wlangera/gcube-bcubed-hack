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
date: 17 July 2024
bibliography: paper.bib
authors_short: Langeraert et al.
group: Project 2+8
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

During the B-Cubed Hackathon, we aimed to create a practical simulation framework for biodiversity data cubes. This framework is composed of three steps ([Fig. 1](#Figure_1)):

1. The occurrence process: Simulating occurrences of multiple species distributed in a landscape over a temporal scope. This will depend on the **rarity**, which can differ between species and over time, and their **spatial clustering**, which can differ between species. A challenge for this part is to implement a consistent **spatial and temporal autocorrelation** for simulated species trends.
2. The detection process: Simulation of a variety of observation processes can generate actual occurrence datasets. Each species has a different **detection probability**. The detection process will also depend on the **sampling effort** which can be different among spatial and temporal dimensions. We can also assign a spatial uncertainty to each observation.
3. The grid designation process: Based on their spatial uncertainty, occurrences can be designated to grid cells of a larger grid to form a data cube.

The simulation framework can be used to assess multiple research questions under different parameter settings, such as the effect of clustering on occurrence-to-grid designation and the effect of different patterns of missingness on data quality and indicator robustness. Simulation studies can incorporate scenarios with missing data, enabling researchers to assess the impact of data gaps on analyses. Understanding how missing data influences results is crucial for improving data collection strategies and addressing potential biases. With this, the secondary objective of the simulation study is to develop a visualisation tool for the simulated cubes. This tool aims to enhance the understanding of data clustering and missingness within the simulated environment. By creating a visual representation, researchers can effectively analyse and interpret patterns of clustered data as well as identify areas where data is missing. This visualization capability contributes to a more comprehensive exploration of the simulated scenarios, allowing for deeper insights into the behaviour of data within the context of the study.

![Simulation framework for biodiversity data cubes.](./figures/visual_proposal.png){#Figure_1
.Figure}

## Materials and Methods


## Results


## Discussion


## Conclusion


## Acknowledgements
We would like to express our gratitude to the Horizon Europe funded B-Cubed (Biodiversity Building Blocks for policy) project for the organisation of this hackathon.
Special thanks go to Laura Abraham of Meise Botanic Garden for her outstanding efforts in coordinating the event.
Additionally, we acknowledge the Research Foundation - Flanders (FWO) and KU Leuven for the support they gave us in making this event possible.

## References