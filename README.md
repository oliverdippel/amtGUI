
<!-- README.md is generated from README.Rmd. Please edit that file -->
amtGUI
======

The goal of `amtGUI` is to provide a simple user interface to `amt` with Shiny for the analysis of animal telemetry data. This `README` shows how to use the app. For a detailed explanation of how the app and it's underlying calculations work consider reading the term paper.

Installation
------------

You can install `amtGUI` from github with:

``` r
# install.packages("devtools")
devtools::install_github("abuchmueller/amtGUI")
```

Getting started
---------------

To get started you will need two things: A dataset containing GPS data of at least one animal and a landuse raster (usually in form of a .tif image) for the underlying area of study.

However, `amtGUI` comes with examples for both so you can get started immediately.

Uploading data
--------------

We proceed to load the "Fisher NY" data set, a reduced version of fisher data from LaPoint et al. (2013a).

![Getting started](img/dataup-small.png)

After loading your data successfully, you can see it below. You can switch between your data and a column summary of it. **Note:** You need to assign a valid EPSG code in order to procceed here. The code for our showcase data set is 4326.

Uploading a map
---------------

After you've loaded your data set you may proceed to load your landuse raster (map).

![Map Upload](img/mapup-small.png)

`amtGUI` tries to automatically detect all known EPSG codes of the raster and will give suggestions, however you still need to assign one manually to proceed.

After this is done you can start configuring your analysis.

Configuring your analysis
-------------------------

This section of the App is split in two tabs. Inside the first tab you can create tracks. In the second tab you can add additional covariates to your analysis.

For now let's begin with track creation. To create a track, you need to specifiy which columns of your data set contain the x and y-coordinates as well as the timestamps. This is mandatory, as without a track, you can't perform meaningful analysis of telemetry data. Additionally, you can specify an ID column for your data to identify which observations belong to which animal, or if you have multiple animals in your data set and specify ID you can filter animals out, preform analysis on only one animal. To create the track now you only need to specify two more things: The resampling rate and the tolerance for your track then you're done, the app will immediately start working in the background to (re)calculate your track(s). You can also set a date range, the default setting is to set to the date range of your data entirely so you don't need to specify one to proceed.

![Track creation](img/track-small.png) The 'Add Covariates' tab let's you configure your analysis even further. On the left side of the tab the smallest number of bursts for a step to count (the minimum here is 3, as you need 3 relocations within one time interval to calculate the turning angle of a step) and will be accompanied by a small table giving you information on the number of bursts remaining for each animal ID with your current settings.

On the right side you can edit the names of environmental covariates and transform them into categorical variables with a simple checkbox. You can also set to include or exclude the time of day as a categorical covariate. This will be accompanied by a table where you can see existing levels for each animal ID.

![Add Covariates](img/addc-small.png)

Model Building
--------------

If you correctly set up your track before, you are now ready to fit statistical models with `amtGUI`.

On the Modeling tab you can choose between two model types: Integrated Step Selection Functions (iSSF) and Resource Selection Functions (RSF).

To fit an ISSF you need to select the input variables you want to use. Besides your covariates you can specify up to 5 interaction terms. By moving the slider you can increase/decrease the number of interaction terms. Addtionally you can specify the number of random steps for each taken step (ISSF only). Hitting the "Fit Model" button will immediately start the fitting process (as indicated by the loading bar). Below the buttons you can see your model output, i.e., your models estimates which you can download in a csv file. Clicking the "Clear" resets the tab so you can begin fresh. This is recommended before fitting a new model. ![Add Covariates](img/issf-small.png)

If you want to save your analysis to recreate it later you can download a report file by clicking the "Download report" button which will create a report containing all visible user inputs.

Interactive Map
---------------

Here you can take a look at your data (for one animal at a time). If supplied the app with ID's in the "Create Track" tab and only choose ***one*** active ID you can see an interactive map here.

![Add Covariates](img/intmap-small.png)
