<div align="center">
<img src="https://github.com/skswar/Seismic_Signal_Analysis/blob/main/img/banner.png" alt="Seismic Data Analysis Intro Logo" height="250px" width="80%"/>
</div>
<h3 align="center">Analyzing NE68 Seismic Tremors using Unsupervised Machine learning and Unsupervised Deep Learning Techniques (DEC) and Identifying Different Signal Patterns</h3>

## Table of contents
* [Introduction](#introduction)
* [About Dataset](#about-dataset)
* [Link to Code](#link-to-code)
* [Methodology](#methodology)
* [Acknowledgements](#acknowledgements)

<hr>

## Introduction
Data science extends beyond working solely with social or financial tabular data to extract insights. Data exists in various forms, and each form holds meaningful information. Thus in my opinion, a person willing to learn data science should not restrcit him/her to any particular type of data, rather be prepared to tackle any form of data that comes in their way. This ultimately help towards a better learnig curve in their Data Science journey. Extending from that, applying data science methodologies can be beneficial in numerous fields, including Earth Science. Ground vibrations and earthquakes are natural hazards that researchers analyze to understand their occurrence patterns and gain insights into the Earth's structure beneath the surface.

To conduct more informed research, capturing a larger volume of data on ground vibrations is essential. The availability of extensive data enables better solutions and analysis. However, as data volume increases, the analysis becomes more challenging. This is where data science plays a crucial role. Ground vibrations or earthquake signals can be considered as time series data, as they propagate from one location to another. Understanding the properties of these signals is invaluable, as they can often resemble noise or exhibit seismic-like characteristics due to natural activities.

In this project, the I aim to analyze earthquake signals, extract their properties, and cluster them based on these properties. This approach aimed to present a more refined and well-informed dataset, contributing to further research in the Earth Science community.

## About Dataset
The dataset is of 100 *.csv files, each containing earthquake (i.e., ground vibration) data for one earthquake. They are time series, just like other time signals for e.g., sound. This data was recorded at NE68 station located in Songliao basin, Northeastern China. Earthquake data have usually three components which are radial, transverse, and vertical. Each *.csv file is a 16800 by 3 matrix, with the first, second, and third column representing data from radial, transverse, and vertical component, respectively. In the provided data, the sample rate is 40 Hz (i.e., 40 samples per second), and the earthquake is supposed to arrive at 120th second. This means the first 120 second of the data can be considered as pre-earthquake noise, and the rest of them is the earthquake signal. 

The link to the data can be found [here](https://github.com/skswar/Seismic_Signal_Analysis/tree/main/datasource).

## Link to Code
The methodology followed in this proejct has been discussed in the next section in detail. One can access the notebook through the following link.

**Link to Notebook**: [Seismic_Data_Analysis.ipynb](https://github.com/skswar/Seismic_Signal_Analysis/tree/main/Seismic_Data_Analysis.ipynb)






