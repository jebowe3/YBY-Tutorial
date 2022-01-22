# Digital Mapping for the Humanities
Jay Bowen, Digital Scholarship and Publishing Studio, University of Iowa Libraries

## Credits
- [The London of Sherlock Holmes](https://www.google.com/maps/d/viewer?ll=51.510345653313024%2C-0.12769532132744787&z=14&mid=11hi6OwDoifyUI4kFsg7suBQm1t8), by Thomas Bruce Wheeler
- [Descriptive Map of London Poverty 1889](https://davidrumsey.georeferencer.com/maps/b0af04e4-993d-52da-b642-1051e9877e7f/), from the David Rumsey Map Collection
- [Place context analysis using Natural Language Processing](https://github.com/jakobzhao/geog595/tree/master/06_ai), Bo Zhao
- [Word2Vec](https://github.com/sankyfox/word2vec), Sankalp Kolhe
- [Google News and Leo Tolstoy: Visualizing Word2Vec Word Embeddings using t-SNE](https://towardsdatascience.com/google-news-and-leo-tolstoy-visualizing-word2vec-word-embeddings-with-t-sne-11558d8bd4d), Sergey Smetanin

## Contents
- [Introduction](#introduction)
- [Required Technology](#required-technology)
- [Download This Repository](#download-this-repository)
- [Download the London Basemap](#download-the-london-basemap)

## Introduction
This tutorial is an overview of digital mapping in the humanities. Through the steps provided here, you will gain a cursory introduction in how to:

- Use desktop GIS software to map a pre-collected spreadsheet of points from the Sherlock Holmes series onto a georeferenced historic map of London
- Save a geojson file of these points for later use in web mapping
- Use a text editor to reference this geojson file in pre-written JavaScript to produce an interactive web map
- Use a text editor to reference a shared Google spreadsheet of these points in pre-written JavaScript
- Add images to the Google spreadsheet to demonstrate the potential for crowdsourcing in an interactive web map
- Use Python code in Jupyter Notebook to analyze The Adventures of Sherlock Holmes
- Use Python to identify, measure the frequency, and geocode mentioned locations in the text
- Use Python to identify important words from the text and identify their most similar relatives from other words in the text
- Use Gephi to map these word connections as a network to visualize broad themes in the text

## Required Technology
This tutorial focuses on open-source approaches to digital mapping in the humanities. All of the required technology is free to download and use. For all steps using GIS, we will use [QGIS](https://www.qgis.org/en/site/). For interactive web mapping, we will use [Leaflet](https://leafletjs.com/), a JavaScript library created specifically for web mapping. For editing the code that creates our online map, we will use a text editor called [Atom](https://atom.io/). For text analysis, we will execute [Python](https://www.python.org/) code in [Jupyter Notebook](https://jupyter.org/) using a [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/) server created with [GESIS Notebooks' Binder](https://notebooks.gesis.org/binder/) service. Finally, for network mapping of analyzed text, we will use [Gephi](https://gephi.org/). Before you begin, you must download these from the following sites:

- [QGIS](https://qgis.org/en/site/forusers/download.html)
- [Atom](https://atom.io/)
- [Gephi](https://gephi.org/users/download/)
- [Our GESIS Notebooks Binder](https://notebooks.gesis.org/binder/v2/gh/jebowe3/Text-Analysis-Binder/HEAD)

## Download This Repository
Before opening QGIS, you should download this repository and save it to your desktop so that you can work with the files included here. Towards the top of this page, you should see a green button that says, "Code." Click this and select "Download ZIP" from the options as shown in the image below.

![Downloading Repo](images/Repo-download.png)  
**Figure 01**. How to download a GitHub repository.

Unzip this folder and save it to your desktop.

## Download the London Basemap


Within the project folder, you will find a file called "SHERLOCK_HOLMES_LONDON.csv" inside the "spreadsheet" folder. If you open this file, you will see that it contains six columns (place, location, info, X, Y, and story). For mapping this spreadsheet, the important information is in the X and Y columns.

Every map is essentially a chart with X and Y axes (you may also see Z for elevation). Think of a map oriented with the top of the sheet at north. As the X axis moves from left to right, the X column stores longitude data (degrees east or west of Greenwich, England). As the Y axis moves from bottom to top, this column stores the latitude information (degrees north or south of the Equator). Close the csv file and open QGIS.
