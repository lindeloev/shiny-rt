# Reaction Time Distributions - An Interactive Overview
This is the code underlying [this guide](http://lindeloev.net/shiny/rt/). You can run it in RStudio or on a shiny server. I set up a free one at Google Cloud, which host it right now. If you expect fewer visitors, using RStudios built-in upload to [http://shinyapps.io](http://shinyapps.io) is very convenient. 

The file `index.html` is hosted locally at lindeloev.net to make Twitter Cards etc. work.

## How to set up a Shiny Server
The hard part was getting this to run on the web, which required around 6 evenings and a lot of debugging. [http://shinyapps.io](http://shinyapps.io) is very convenient for RStudio users, but the server shuts down after a document has been in use for 25 hours in a month. I choose to set up a shiny server on Google Cloud because they offered a year's worth of free computing and pretty low charges after that. I used [this excellent guide](https://github.com/paeselhz/RStudio-Shiny-Server-on-GCP) although it needs a few updates:

 * My SSH username was different than expected. It took the username of the OS of my PC for some reason.

 * The projectid was also different than expected. It should be "shinyrt" but somehow changed to "shinyrt-251809".

 * Use newest shiny server and newest rstudio server instead of the links provided in the guide.
 The guide proposes to put the scripts in  the `etc/shiny-server/`. I changed the location to  `/home/user/shiny`. You can do this by editing the shiny configuration. Write `sudo nano /etc/shiny-server/shiny-server.conf`. To load this configuration, run ` sudo systemctl reload shiny-server`. I also ended up setting a lower number of concurrent users : ` simple_scheduler 70;`. [Read more about configuring the Shiny server here](https://docs.rstudio.com/shiny-server/).


# Issues setting up the server

 * I used Ubuntu 18.04 for server since I'm an old Ubuntu user. For some reason, `rstan` failed to install so I couldn't just install ` brms`.  `rstan`  is not available in the PPA for 18.04. Since I only needed  `rstan`  to install  `brms`, I ended up copying out the relevant  `brms`  scripts and source them from R.

 * Perhaps due to heavy interest, I initially had issues with the server overloading to the degree that it would reject all connections. I did not find a sustainable solution, but it took *longer* for it to crash if I set a lower number of concurrent users (see above) restarting the server using `sudo systemctl stop shiny-server` followed by `sudo systemctl start shiny-server`. I guess you could make a cron job which monitors CPU usage and runs this automatically, but since all connections are interrupted upon restart, it's a very ugly hack.

 * When I run the .Rmd on my cloud shiny server, the Rmarkdown links fail to work. [I explained this problem here](https://community.rstudio.com/t/anchor-links-fail-on-default-shiny-server/39518), but I haven't found a solution yet.

 * Shiny does not expose files via URL so I could not just link to "images/file.png". I linked to the GitHub repo instead.
 
 * The Google Cloud server is just an IP address which is not memorable. After learning that I could not make a true web alias, I tried making an iframe in a GitHub page. However, because the Google Cloud server had no SSL certificate (no https://), GitHub Pages would not load content from it. As you can see, I hosted the iframe on my personal website instead. I had to add a .htaccess file to redirect https (SSL) traffic to http:


    RewriteEngine on
    RewriteCond %{HTTP:X-Forwarded-Proto} https
    RewriteRule ^(.*)$ http://lindeloev.net/shiny/rt [R=301,L]