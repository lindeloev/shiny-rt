# Reaction Time Distributions - An Interactive Overview
This is the code underlying [this guide](http://lindeloev.shinyapps.io/shiny-rt). There is a [non-interactive version here](https://lindeloev.github.io/shiny-rt/) if the interactive version doesn't run. You can run the interactive verison it in RStudio (see below) or on a shiny server. If you expect fewer visitors, using RStudios built-in upload to [http://shinyapps.io](http://shinyapps.io) is very convenient.

The file `include/index.html` is hosted locally at lindeloev.net to make Twitter Cards etc. work.

## TL;DR
Most people default to using gaussian models to model reaction times. It has a poor fit to the actual data as even the simplest model assessment would tell you. I demonstrate that the **shifted log-normal** is superior in terms of fit, interpretability while being just as easy to use. The **Drift-Diffusion Model** is has greater theoretical value but is harder to fit.

Here is a review of various models that you can play with interactively if you run the app:

![](https://github.com/lindeloev/shiny-rt/raw/master/rt_cheat_sheet.png)

## Run on your own computer

 * Download the files to a folder
 
 * If you haven't already: Install and open RStudio. Then run this in the console to install the needed packages: `install.packages('shiny', 'rtdists')`
 
 * Open `index.Rmd`.
 
 * Press CTRL + SHIFT + K to launch it. Navigate the document in the Viewer pane or open it in the browser by clicking the small icon at the top of the Viewer pane. 


```
    RewriteEngine on
    RewriteCond %{HTTP:X-Forwarded-Proto} https
    RewriteRule ^(.*)$ http://lindeloev.net/shiny/rt [R=301,L]
```
