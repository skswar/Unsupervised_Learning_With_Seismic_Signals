<div align="center">
<img src="https://github.com/skswar/Seismic_Signal_Analysis/blob/main/img/banner.png" alt="Seismic Data Analysis Intro Logo" height="250px" width="80%"/>
</div>
<h3 align="center">Analyzing NE68 Seismic Tremors using Unsupervised Machine learning and Unsupervised Deep Learning Techniques (DEC) and Identifying Different Signal Patterns</h3>

## Table of contents
* [Introduction](#introduction)
* [About Dataset](#about-dataset)
* [Methodology](#methodology)
* [Link to Code](#link-to-code)
* [Acknowledgements](#acknowledgements)

<hr>

## Introduction
Data science extends beyond working solely with social or financial tabular data to extract insights. Data exists in various forms, and each form holds meaningful information. Thus in my opinion, a person willing to learn data science should not restrcit him/her to any particular type of data, rather be prepared to tackle any form of data that comes in their way. This ultimately help towards a better learnig curve in their Data Science journey. Extending from that, applying data science methodologies can be beneficial in numerous fields, including Earth Science. Ground vibrations and earthquakes are natural hazards that researchers analyze to understand their occurrence patterns and gain insights into the Earth's structure beneath the surface.

To conduct more informed research, capturing a larger volume of data on ground vibrations is essential. The availability of extensive data enables better solutions and analysis. However, as data volume increases, the analysis becomes more challenging. This is where data science plays a crucial role. Ground vibrations or earthquake signals can be considered as time series data, as they propagate from one location to another. Understanding the properties of these signals is invaluable, as they can often resemble noise or exhibit seismic-like characteristics due to natural activities.

In this project, the I aim to analyze earthquake signals, extract their properties, and cluster them based on these properties. This approach aimed to present a more refined and well-informed dataset, contributing to further research in the Earth Science community.

## About Dataset
The dataset is of 100 *.csv files, each containing earthquake (i.e., ground vibration) data for one earthquake. They are time series, just like other time signals for e.g., sound. This data was recorded at NE68 station located in Songliao basin, Northeastern China. Earthquake data have usually three components which are radial, transverse, and vertical. Each *.csv file is a 16800 by 3 matrix, with the first, second, and third column representing data from radial, transverse, and vertical component, respectively. In the provided data, the sample rate is 40 Hz (i.e., 40 samples per second), and the earthquake is supposed to arrive at 120th second. This means the first 120 second of the data can be considered as pre-earthquake noise, and the rest of them is the earthquake signal. 

The link to the data can be found [here](https://github.com/skswar/Seismic_Signal_Analysis/tree/main/datasource).

## Methodology
Ground virbation data although can be considered as a Time Seriese signal, but still doesn't follow a traditional time series analysis such as trend, seasonality. Earthquake data analysis mainly follows techniques of Digital Signal Processing. Earthquake data mainly contains three components which are Radial, Transverse and Vertical the combination of which provides seismologists a three dimensional view of the signals behaviour. In this project, I mainly decided to analyze the Vertical signal as the vertical channel captures more or less all type of earthquake waves (Primary, Secondary and Surface waves) [1], therefore I decided to select the vertical channel data and perform all analysis on this component. 

### Understanding Signal Properties
As per Signal processing techniques, to analyze any given signal or wave, it is important to convert the singal into its frequency domain and find out the signal strength in different frequency. This helps us understand the dominant frequencies present in the signal and their amplitude range. It was given in the dataset description, the first 120 seconds of the data can be considered as pre earthquake noise and rest as legitimate signal. Therefore I divded the signal in two halves, performed Fast Fourier Transform (FFT) and analyzed the frequency level for both noise and signal. As per the below box plot we can clearly see that noise part of the signal has much higher frequency range than the other part of the signal.

<p align="center">
<img src="https://raw.githubusercontent.com/skswar/Seismic_Signal_Analysis/master/img/eq1.png" width="45%"/>
</p>

Every signal and peaks and valleys, and peaks denotes the strenght of the signal. Thus to derive more properties of the signal, I calculated the top 5 peaks for both noise and earthquake component. This helped me find at what frequency range, and amplitude range this peaks are occuring.  The follwing left images shows, how the frequecy varies at different peaks for both noise and singal component. The right image shows how the amplitude varies for the same. These properties of the singal will later help us to define critical features to feed in the machine learning algorithm. 

<p align="center">
<img src="https://raw.githubusercontent.com/skswar/Seismic_Signal_Analysis/master/img/eq2.png" width="50%"/>
<img src="https://raw.githubusercontent.com/skswar/Seismic_Signal_Analysis/master/img/eq3.png" width="50%"/>
It is evident that noise has a higher frequency and lower amplitde distribution than the signal at different peaks
</p>

## Link to Code
The methodology followed in this proejct has been discussed in the next section in detail. One can access the notebook through the following link.

**Link to Notebook**: [Seismic_Data_Analysis.ipynb](https://github.com/skswar/Seismic_Signal_Analysis/tree/main/Seismic_Data_Analysis.ipynb)

## References
1. [IRIS Earthquake Science, 3-component Seismograms—Capturing the motion of an earthquake](https://www.youtube.com/watch?v=Za_22xo7ZQQ&ab_channel=IRISEarthquakeScience)




