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
- [Using QGIS](#using-qgis)
  - [Map the Spreadsheet Data with QGIS](#map-the-spreadsheet-data-with-qgis)
  - [Adding a Basemap](#adding-a-basemap)
  - [Changing Projections](#changing-projections)
  - [Adding a Georeferenced Historic Basemap](#adding-a-georeferenced-historic-basemap)
- [Leaflet JavaScript for Web Mapping](#leaflet-javascript-for-web-mapping)
  - [Export a GeoJSON File for Web Mapping](#export-a-geojson-file-for-web-mapping)
  - [Download Atom-Live-Server Package](#download-atom-live-server-package)
  - [Add the Sherlock GeoJSON to a Web Map Using Atom](#add-the-sherlock-geojson-to-a-web-map-using-atom)
  - [Crowdsourced Web Mapping with Google Sheets](#crowdsourced-web-mapping-with-google-sheets)
- [Text Analysis, Geolocation, and Network Mapping with Python, QGIS, and Gephi](#text-analysis-geolocation-and-network-mapping-with-python-qgis-and-gephi)
  - [Open the ipynb File in Jupyter Notebook](#open-the-ipynb-file-in-jupyter-notebook)

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
Before opening QGIS, you should download this repository and save it to your desktop so that you can work with the files included here. You can download a zip file of this repository from the [link included here](https://github.com/jebowe3/YBY-Tutorial/archive/refs/heads/main.zip). Unzip this folder and save it to your desktop.

## Download the London Basemap
Now, you will need to download the georeferenced historic basemap of London. This is a map of London poverty drafted by Charles Booth in 1889. It is contemporaneous to Doyle's Sherlock Holmes series and will provide good historical context to our map.

Download the map from the [link included here](https://drive.google.com/file/d/1udpezkj1y-DIg0kjHLqfcI1swIwLTrwe/view?usp=sharing) and save it inside your unzipped project folder in a new subdirectory called "booth-poverty-map" as shown below.

![Saving the Basemap](images/basemap-save.png)  
**Figure 01**. Saving the Basemap.

## Using QGIS

### Map the Spreadsheet Data with QGIS

Within the unzipped project folder, you will find a file called "SHERLOCK_HOLMES_LONDON.csv" inside the "spreadsheet" folder. If you open this file, you will see that it contains six columns (place, location, info, X, Y, and story). For mapping this spreadsheet, the important information is in the X and Y columns.

Every map is essentially a chart with X and Y axes (you may also see Z for elevation). Think of a map oriented with the top of the sheet at north. As the X axis moves from left to right, the X column stores longitude data (degrees east or west of Greenwich, England). As the Y axis moves from bottom to top, this column stores the latitude information (degrees north or south of the Equator). Close the csv file and open QGIS.

Upon opening QGIS, you should notice a dropdown option called "Layer" in the bar at the top of your screen. Click this and select "Add Layer." Then select "Add Delimited Text Layer" from the options provided.

![Adding Spreadsheet Data to QGIS](images/Upload-csv-1.png)  
**Figure 02**. Option to add a spreadsheet in QGIS.

This will open a form. In the box next to "File name," include the path to the csv file. You can navigate to it by pressing the button with three dots to the right of this box. After doing so, the rest of this form should complete automatically. If not, make sure to select "CSV" under "File Format," click "Point coordinates" under "Geometry Definition," select "X" for "X field" and "Y" for "Y field," and make sure that "Geometry CRS" is set to "EPSG:4326 - WGS 84." Then, click "Add." The form should appear as follows.

![Add Delimited Text Layer Form](images/Upload-csv-2.png)  
**Figure 03**. How to fill out the form to add a delimited text layer.

### Adding a Basemap
After clicking add, you should see a collection of points on a white background in your map edit window. Not being sure if these points are actually in London, we need a basemap for visual verification. You can add one by clicking "XYZ Tiles" in the browser window at the top left corner. Select "OpenStreetMap" and drag and drop this into your map window. Next, in the layers window, make sure to drag the basemap under the Sherlock points.

![Add Basemap](images/points-over-base.png)  
**Figure 04**. Add a basemap and place it beneath the points.

### Changing Projections
Things look good, but if you look at maps for a living, this map looks a little squished. This illustrates the importance of projections. Every map is an abstraction of the Earth's natural curvature to a flat surface, so some projections are better than others for particular locations. In this case, it would be good to use a projection developed specifically for London, such as EPSG:102400 (London Survey Grid). In the bottom right corner of your window, you should see a little button that looks like a globe wearing a hat, followed by an EPSG code. This is where you can change your projection. Click on this and, in the form that opens, type "102400" into the "Filter" box. You should now see "London_Survey_Grid" appear in the box beneath "Predefined Coordinate Reference Systems." Click it and then click "OK." After you change the projection, your map should be a little easier on the eyes.

![Change Projection](images/change-projection.png)  
**Figure 05**. How to change the projection.

GIS users are trained to think of mappable data in two main categories - vector and raster. Vector data consist of distinct points, lines, and polygons. The spreadsheet data that you have mapped is one example of vector data. In contrast, raster data consist of continuous pixels. A scanned map is an example of raster data. We are now going to add some new raster data to our map.

### Adding a Georeferenced Historic Basemap
Adding an historic basemap to your project is a nice way to give your map historical context. Using GIS software, you can take any scanned map and "rubber sheet" it to your project in a painstaking process known as georeferencing. Essentially, this is a process of placing a series of pins on your scanned map and linking them to a series of matching pins in your map edit window. After you have done this, you can run a tool in GIS to assign coordinates to each pixel on your scanned map. Fortunately, the map you downloaded and placed inside the "booth-poverty-map" folder is already georeferenced.

Similar to how you added the csv data, click "Layer" in the bar at the top of the screen. Then, click "Add Layer" and "Add Raster Layer." This will open a form.

![Adding a Raster Layer](images/Add-raster.png)  
**Figure 06**. How to add a raster layer.

In the form that opens, navigate to and select the file called "Booth_Descriptive_Map_of_London_Poverty_1889.tif" located in the repository you downloaded. Then, click "Add."

![Add Raster Layer Form](images/Raster-form.png)  
**Figure 07**. The form for adding a raster layer.

After adding the georefenced raster, you should see Booth's 1889 map of London poverty in your map edit window. Again, make sure to drag this map beneath the points in the layers window. The result should look something like this:

![Booth Map](images/Booth-map-in-QGIS.png)  
**Figure 08**. The Booth map in QGIS.

This gives you a good idea of how to use QGIS to plot spreadsheet data over a scanned historic map. If you are interested in learning how to export this as a static map in pdf format, please see [these in-depth instructions](https://jebowe3.github.io/DH-Mapping/#step-7-how-to-make-a-static-map). If you want to see how to export these points in JavaScript Object Notation format so that the data can be used in an interactive web map, read on.

## Leaflet JavaScript for Web Mapping
One of the great things about QGIS as opposed to ArcGIS (aside from it being free and working in both Windows and MacOS) is that it works will with file formats that are readily accessible in JavaScript web mapping. Without needing to convert, QGIS can read, edit, and save GeoJSON files. A GeoJSON is a type of JavaScript Object Notation file that carries geographic information and feature data, just like a shapefile package, but within one convenient file. In the following steps, we will see how to export our points to a GeoJSON and how to use this file in an interactive web map.

### Export a GeoJSON File for Web Mapping
Return to the map edit window, right click the points layer, and click "Export" and "Save Features As." Make sure you export in GeoJSON format. Click the three dots next to "File name," save as "sherlock_points," and make sure to save the file inside the "data" folder within the "leaflet-map" folder inside the repository that you downloaded to your desktop. Finally, set coordinate precision to 5 decimal points. You could go with the default 15, but that level of coordinate precision is generally unnecessary and simply makes for heavier files.

![Export Sherlock Points](images/export-sherlock-points.png)  
**Figure 09**. Export all of the Sherlock points.

### Download Atom-Live-Server Package
Now we are ready to open our "leaflet-map" folder and do some minor editing in Atom. Open the repository that you downloaded to your desktop. Locate the folder called "leaflet-map." Drag and drop this entire folder over the green Atom icon on your desktop. This should open all of the web map components within an Atom text edit session. In the bar at the left, open the file called "index.html" so that you can see all of the code behind the web map. Your screen should look like this:

![Editing in Atom](images/index-html-atom.png)  
**Figure 10**. Editing in Atom.

The first thing that you will want to do so that you can check your progress is to download an Atom package called "atom-live-server." From the option in the bar at the top, click "Atom" and "Preferences." From the options that appear on the left, choose "Install," type "atom-live-server" in the search bar, and click "Install" on the first result. On my screen in the example below, you will see "Uninstall" because I have already installed this package.

![Installing Atom-Live-Server](images/install-liveserver.png)  
**Figure 11**. Installing atom-live-server.

Now you can check the progress of edits to your web map with a locally hosted server. To test it out, click "Packages" from the options in the bar at the top. Select "atom-live-server" and "Start server." This will open the map in your web browser.

![Initial Live Server Map](images/live-server-init-map.png)  
**Figure 12**. The initial web map in atom-live-server.

The map should look like the image above. You will notice that one interactive feature is already on the map. In the top right corner, there is a slider control that changes the opacity value of the historic base map tiles so that you can see the contemporary map of London underneath.

### Add the Sherlock GeoJSON to a Web Map Using Atom
You'll notice that there are no points on the map. That is because we have not directed the JavaScript within the index.html file to the GeoJSON file holding the points. Remember that the local path to the Sherlock points is 'data/sherlock_points.geojson' and that we will need to add this path to the index.html file. Scroll through the index.html file until you see the following lines of JavaScript:

```js
// use jquery to load GeoJSON data
$.when(
  $.getJSON(/* 'ADD PATH TO GEOJSON DATA HERE' */)
  // when the files are done loading,
  // identify them with names and process them through a function
).done(function(sherlockPts) {
  // more JavaScript here
});
```

Replace /* 'ADD PATH TO GEOJSON DATA HERE' */ with 'data/sherlock_points.geojson' so that those lines of JavaScript now look like this:

```js
// use jquery to load GeoJSON data
$.when(
  $.getJSON('data/sherlock_points.geojson')
  // when the files are done loading,
  // identify them with names and process them through a function
).done(function(sherlockPts) {
  // more JavaScript here
});
```

Now, save your edits to the index.html file and refresh your web map in atom-live-server. You should notice a lot of blue markers now appear. Hover over them and you will see detailed descriptions of each points. Also notice that there is a filter button under the zoom control in the top left corner. If you click on this, you will see that you can filter the points by story name.

![Finished Live Server Map](images/web-map-finished.png)  
**Figure 13**. The finished web map in atom-live-server.

While this walkthrough is intended as a quick introduction to what is possible with interactive web mapping, you may be wondering what the all of the code in the index.html file is doing. For a more thorough explanation, please [click this link](https://jebowe3.github.io/DH-Mapping/#step-4-explanation-of-the-code-behind-the-web-map).

### Crowdsourced Web Mapping with Google Sheets
With a few slight changes to our index.html code and a JavaScript library called PapaParse, we can parse a Google Sheet directly and add this content to map markers. Within the repository you downloaded, there is another [html file](https://github.com/jebowe3/YBY-Tutorial/blob/main/leaflet-map/googlesheet-index.html) at 'leaflet-map/googlesheet-index.html' that generates markers and popup content from our shared [Google Sheets spreadsheet](https://docs.google.com/spreadsheets/d/1CT3wnuXk0dObZgLyOgnZZmh_av5Sm2nWlRByVxVkr9k/edit?usp=sharing).

In Atom, open the googlesheet-index.html file and take a quick look at the code. We are going to point our browser to this html file instead of the index.html file we viewed previously.

This time, run atom-live-server again, but add 'googlesheet-index.html' to the url in the browser address bar. You should see a similar map load in your browser, with one important distinction. Notice how the first entry in our Google Sheets document contains an image link in a column titled "images." If you go back to the map in atom-live-server, filter for The Five Orange Pips in the story filter and click on the marker in the city center for Lloyd's Register, you will notice that this popup contains the image from that web link.

![Popup with Image](images/popup-with-image.png)  
**Figure 14**. A popup with an image.

Now, let's experiment with crowdsourcing popup image content using [Wikimedia Commons](https://commons.wikimedia.org/wiki/Main_Page). Return to our shared [Google Sheets spreadsheet](https://docs.google.com/spreadsheets/d/1CT3wnuXk0dObZgLyOgnZZmh_av5Sm2nWlRByVxVkr9k/edit?usp=sharing) and find an entry missing an image url in the "images" column for which there is likely to be an image (a train station, cathedral, institution, etc.).

![Empty Entry](images/empty-entry.png)  
**Figure 15**. An empty entry in the images column.

Next, search for an image of that location at [Wikimedia Commons](https://commons.wikimedia.org/wiki/Main_Page) as shown below.

![Image Search](images/search-images.png)  
**Figure 16**. Search for an image at Wikimedia.

Now, right click on the image you want to use and select "Open Link in New Tab" as shown below.

![Open Link in New Tab](images/new-tab.png)  
**Figure 17**. Open link in new tab.

In the new tab, to the right of the image, you will see an option to "use this file on the web". Click this and copy the link from the box under "File URL" as shown below.

![Copy Image URL](images/image-url.png)  
**Figure 18**. Copy the image url.

Paste this link into the empty entry in the images column of the shared google spreadsheet. Return to your googlesheet-index.html in atom-live-server and make sure to refresh the page. Now, when you hover over the marker for the image you just entered, you should see your added image in the popup content (it may take a moment).

![Image Added](images/image-added.png)  
**Figure 19**. Image added to popup.

Now that you have seen some of the potential for JavaScript in interactive web mapping, let's take a look at how Python scripting can help us to analyze and map texts geographically and conceptually.

## Text Analysis, Geolocation, and Network Mapping with Python, QGIS, and Gephi
If you foresee doing a lot of Python scripting in the future, it will be helpful to download [Anaconda Navigator](https://www.anaconda.com/products/individual) for setting up environments where you can test and run Python code inside a Jupyter Notebook file. For in-depth instructions on how to do this, [click this link](https://jebowe3.github.io/DH-Mapping/#download-anaconda-navigator).

However, in this example, we will run a Jupyter Notebook file within a pre-established environment in a [GESIS Notebooks Binder](https://notebooks.gesis.org/binder/) in our web browser. You can open this by [clicking this link](https://notebooks.gesis.org/binder/v2/gh/jebowe3/Text-Analysis-Binder/HEAD).

### Open the ipynb File in Jupyter Notebook
After the binder finishes loading in your browser, click and open the "place-analysis.ipynb" file in the menu on the left side of the screen.

![Open ipynb File](images/open-ipynb.png)  
**Figure 20**. Open the ipynb file.

Follow the steps listed in the opened file, making sure to read through the explanations before running each block of Python code. The code included in the ipynb file will do the following:

1. Download and save a txt file containing The Adventures of Sherlock Holmes
2. Make and save a Word2Vec model for text analysis
3. Create and save a word cloud of the the top 50 important words in the text
4. Create and save a word cloud of the the top 50 locations mentioned in the text
5. Save a csv file of all mentioned locations along with frequency counts for each
6. Save a revised csv file of cleaned and corrected locations along with frequency counts and coordinates for each
7. Generate a gexf file for mapping networks between the 50 most common important words from the text and the twenty most similar words to each
