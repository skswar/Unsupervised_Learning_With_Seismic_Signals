<div align="center">
<img src="https://github.com/skswar/Seismic_Signal_Analysis/blob/main/img/banner.png" alt="Seismic Data Analysis Intro Logo" height="250px" width="80%"/>
</div>
<h3 align="center">Analyzing NE68 Seismic Tremors using Unsupervised Machine learning and Unsupervised Deep Learning Techniques (DEC) and Identifying Different Signal Patterns</h3>

## Table of contents
* [Introduction](#introduction)
* [About Dataset](#about-dataset)
* [Methodology](#methodology)
  * [Deriving Signal Properties with FFT](#deriving-signal-properties-with-fft)
  * [Deriving Signal Properties with PSD](#deriving-signal-properties-with-psd)
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

### Deriving Signal Properties with FFT
As per Signal processing techniques, to analyze any given signal or wave, it is important to convert the singal into its frequency domain and find out the signal strength in different frequency. This is acheived through Fast Fourier Transform (FFT) helps us understand the dominant frequencies present in the signal and their amplitude range. It was given in the dataset description, the first 120 seconds of the data can be considered as pre earthquake noise and rest as legitimate signal. Therefore I divded the signal in two halves, performed Fast Fourier Transform (FFT) and analyzed the frequency level for both noise and signal. As per the below box plot we can clearly see that noise part of the signal has much higher frequency range than the other part of the signal.

<p align="center">
<img src="https://github.com/skswar/Seismic_Signal_Analysis/blob/main/img/eq1.png" width="45%"/>
</p>

Every signal and peaks and valleys, and peaks denotes the strenght of the signal. Thus to derive more properties of the signal, I calculated the top 5 peaks for both noise and earthquake component. This helped me find at what frequency range, and amplitude range this peaks are occuring.  The follwing left images shows, how the frequecy varies at different peaks for both noise and singal component. The right image shows how the amplitude varies for the same. These properties of the singal will later help us to define critical features to feed in the machine learning algorithm. 

<p align="center">
<img src="https://github.com/skswar/Seismic_Signal_Analysis/blob/main/img/eq2.png" width="45%"/>
<img src="https://github.com/skswar/Seismic_Signal_Analysis/blob/main/img/eq3.png" width="45%"/>
<p align="center">It is evident that noise has a higher frequency and lower amplitde distribution than the signal at different peaks</p>
</p>

### Deriving Signal Properties with PSD
Another important Singal analysis technique is Power Spectral Density (PSD). Unlike FFT, this method provides the strength of various frequecny values across signal. Just like above step, I calculated the PSD of noise and signal separately. The following images show the PSD range for noise and singal component. In the right image, I have kept peak one out from the graph as the value was too high to fit in.

<p align="center">
<img src="https://github.com/skswar/Seismic_Signal_Analysis/blob/main/img/eq4.png" width="35%" height="250px"/>
<img src="https://github.com/skswar/Seismic_Signal_Analysis/blob/main/img/eq5.png" width="60%" height="250px"/>
<p align="center">Clearly signal has a higher PSD than noise as shown in the left image. In right image we can see at peak 2 we have the highest range of PSD values and that is becuase the earthquake singal is likely to have the highest power during the first/second peak</p>
</p>

### Applying KMeans Clustering Algorithm
With all the features derived from the previous two steps, we can now look at these signals and try to figure out if there is any particular group of signals that belong together. This way it can be aimed to identify signals which are purely noise but look like earthquake data, ground vibration signals generating from human activity such as mining or actual earthquake data. 

Before applying any unsupervised machine learning, I calculated the following crrelation matrix. It was found that these features do not correlate much and thus can be used as a reliable predictor variables. In following image we can see that negative correlation is only upto -0.2 which is not strong, and there are very few cases where a strong correaltion (~0.8) occurs. As majority of the features were un correlated thus I decided to use all the features for the following step.

<p align="center">
<img src="https://github.com/skswar/Seismic_Signal_Analysis/blob/main/img/eq6.png" width="60%"/>
</p>

The box plots depicted above reveal the presence of outlier cases located at the extremities of the whiskers. Since we are working with signals, it is plausible that these outlier signals may contain valuable information. Consequently, instead of discarding these cases, I applied a standardization process to normalize the data thus reducing the algorithm's sensitivity to outliers.

Next, employing the Elbow method, the number of clusters is determined to be 4 for the implementation of the Kmeans algorithm. This selection allows for an optimal partitioning of the data into distinct groups based on their similarities, facilitating further analysis and interpretation.
<p align="center">
<img src="https://github.com/skswar/Seismic_Signal_Analysis/blob/main/img/eq7.png" width="40%"/>
</p>

The follwing image provided us the result of the clustering algorithm. With visual inspection we can infer that in Cluster 2 at last, singals are mostly looking like a sinusoidal wave throughout and possible indicates noisy signals. Whereas other clusters has signals which resembels a possible earthquake. The information related to frequency and PSD profile can now be plotted and further analyzed to understand signal chaectarestics of each clsuters.
<p align="center">
<img src="https://github.com/skswar/Seismic_Signal_Analysis/blob/main/img/eq8.png" width="80%"/>
</p>

### Applying Deep Embedded Clustering (DEC) Neural NetowrkAlgorithm
Another very common method of analyzing singlas are through spectogram. In simple terms, spectograms are heatmap like images that shows the signal power at different points of time. This images can be fed into a neural network algorithm which uses the auto encoder and decoder technique  to cluster the signals. The DEC algorithm was originally developed by Junyuan Xie, Ross Girshick & Ali Farhadi. In this project, I try to reproduce the algorithm and use it for this earthquake signal analysis. Individual steps for this method has been explained in the notebook. With number of experiements, I decided to choose 9 clusters. From the output of the DEC algorithm it was seen, signals were fairly distributed equally among each cluster. The following image produces three signals from each cluster. From visual inspection we can confirm that signals in different clusters are different and signals belonging to the same cluster has similar appearance charecteristics. As mentioned earlier, the frequency/psd profile of every cluster can be analyzed further to receive more numerically verifiable information.
<p align="center">
<img src="https://github.com/skswar/Seismic_Signal_Analysis/blob/main/img/eq9.png" width="80%"/>
</p>


## Link to Code
The methodology followed in this proejct has been discussed in the next section in detail. One can access the notebook through the following link.

**Link to Notebook**: [Seismic_Data_Analysis.ipynb](https://github.com/skswar/Seismic_Signal_Analysis/tree/main/Seismic_Data_Analysis.ipynb)

## References
1. [IRIS Earthquake Science, 3-component Seismograms—Capturing the motion of an earthquake](https://www.youtube.com/watch?v=Za_22xo7ZQQ&ab_channel=IRISEarthquakeScience)




