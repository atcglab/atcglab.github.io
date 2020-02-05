---
layout: post
title: Efficient data synthesis and visualisation
subtitle: A Coding Club workshop for the Oxford Zoology & Plant Sciences departments
date: 2020-02-02 10:00:00
author: Gergana
meta: "Tutorials"
tags: data_manip data_vis intermediate advanced
---

### Tutorial Aims:

#### <a href="#maps"> 1. Make and beautify maps </a>
#### <a href="#distributions"> 2. Visualise distributions with raincloud plots </a>
#### <a href="#histograms"> 3. Make, customise and annotate histograms </a>

<p></p>

<div class="bs-callout-blue" markdown="1">

__The goal of this tutorial is to advance skills in data visualisation, efficiently handling datasets and customising figures to make them both beautiful and informative. Here, we will focus on ways using packages from the `tidyverse` collection and a few extras, which together can streamline data visualisation and make your research pop out more!__

</div>

## All the files you need to complete this tutorial can be downloaded from <a href="https://github.com/ourcodingclub/CC-dataviz-beautification" target="_blank">this repository</a>. __Click on `Clone/Download/Download ZIP` and unzip the folder, or clone the repository to your own GitHub account.__

`R` really shines when it comes to data visualisation and with some tweaks, you can make eye-catching plots that make it easier for people to understand your science. The `ggplot2` package, part of the `tidyverse` collection of packages, as well as its many extension packages are a great tool for data visualisation, and that is the world that we will jump into over the course of this tutorial. 

The `gg` in `ggplot2` stands for grammar of graphics. Writing the code for your graph is like constructing a sentence made up of different parts that logically follow from one another. In a more visual way, it means adding layers that take care of different elements of the plot. Your plotting workflow will therefore be something like creating an empty plot, adding a layer with your data points, then your measure of uncertainty, the axis labels, and so on.

<center><img src="{{ site.baseurl }}/img/DL_datavis1_layers.png" alt="Img" style="width: 900px;"/> </center>
<center> <b>Just like onions and fancy cakes, graphs in `ggplot2` have layers. </b> </center>

__Note: Pressing enter after each "layer" of your plot (i.e. indenting it) prevents the code from being one gigantic line and makes it much easier to read.__

<div class="bs-callout-blue" markdown="1">
#### Understanding `ggplot2`'s jargon

Perhaps the trickiest bit when starting out with `ggplot2` is understanding what type of elements are responsible for the contents (data) versus the container (general look) of your plot. Let's de-mystify some of the common words you will encounter.

__geom__: a geometric object which defines the type of graph you are making. It reads your data in the __aesthetics__ mapping to know which variables to use, and creates the graph accordingly. Some common types are `geom_point()`, `geom_boxplot()`, `geom_histogram()`, `geom_col()`, etc. 

__aes__: short for __aesthetics__. Usually placed within a `geom_`, this is where you specify your data source and variables, AND the properties of the graph _which depend on those variables_. For instance, if you want all data points to be the same colour, you would define the `colour = ` argument _outside_ the `aes()` function; if you want the data points to be coloured by a factor's levels (e.g. by site or species), you specify the `colour = ` argument _inside_ the `aes()`. 

__stat__: a stat layer applies some statistical transformation to the underlying data: for instance, `stat_smooth(method = "lm")` displays a linear regression line and confidence interval ribbon on top of a scatter plot (defined with `geom_point()`).

__theme__: a theme is made of a set of visual parameters that control the background, borders, grid lines, axes, text size, legend position, etc. You can use <a href="https://ggplot2.tidyverse.org/reference/ggtheme.html" target="_blank">pre-defined themes</a>, create <a href="https://ourcodingclub.github.io/2017/03/29/data-vis-2.html#theme" target="_blank">your own</a>, or use a theme and overwrite only the elements you don't like. Examples of elements within themes are `axis.text`, `panel.grid`, `legend.title`, and so on. You define their properties with `elements_...()` functions: `element_blank()` would return something empty (ideal for removing background colour), while `element_text(size = ..., face = ..., angle = ...)` lets you control all kinds of text properties. 


Also useful to remember is that layers are added on top of each other as you progress into the code, which means that elements written later may hide or overwrite previous elements. 

</div>

### Deciding on the right type of plot

A very key part of making any data visualisation is making sure that it is appropriate to your data type (e.g. discrete vs continuous), and fits your purpose, i.e. what you are trying to communicate! 

Here are some common graph types, but really there is loads more, and you can visit <a href="https://www.r-graph-gallery.com/" target="_blank">the R Graph Gallery</a>for more inspiration!

<center><img src="{{ site.baseurl }}/img/DL_datavis1_which_plot.png" alt="Img" style="width: 950px;"/> </center>

<b>Figures can change a lot the more you work on a project, and often they go on what we call a beautification journey - from a quick plot with boring or no colours to a clear and well-illustrated graph. So now that we have the data needed for the examples in this tutorial, we can start the journey.</b>

<a name="maps"></a>

<b>Open `RStudio`, select `File/New File/R script` and start writing your script with the help of this tutorial. You might find it easier to have the tutorial open on half of your screen and `RStudio` on the other half, so that you can go between the two quickly.</b>

<a id="Acode01" class="copy" name="copy_pre" href="#"> <i class="fa fa-clipboard"></i> Copy Contents </a><br>
<section id= "code01" markdown="1"> 

```r
# Purpose of the script
# Your name, date and email

# Your working directory, set to the folder you just downloaded from Github, e.g.:
setwd("~/Downloads/CC-dataviz-beautification")

# Libraries ----
# if you haven't installed them before, run the code install.packages("package_name")
library(tidyverse)
library(ggthemes)  # for a mapping theme
library(ggalt)  # for custom map projections
library(ggrepel)  # for annotations
library(viridis)  # for nice colours

# Data ----
# Load data - site coordinates and plant records from
# the Long Term Ecological Research Network
# https://lternet.edu and the Niwot Ridge site more specifically
lter <- read.csv("lter.csv")
niwot_plant_exp <- read.csv("niwot_plant_exp.csv")

```
</section>

<div class="bs-callout-blue" markdown="1">

__Managing long scripts:__ Lines of code pile up quickly! There is an outline feature in `RStudio` that makes long scripts more organised and easier to navigate. You can make a subsection by writing out a comment and adding four or more characters after the text, e.g. `# Section 1 ----`. If you've included all of the comments from the tutorial in your own script, you should already have some sections.

</div>

<center> <img src="{{ site.baseurl }}/img/outline_screenshot.png" alt="Img" style="width: 600px;"/> </center>

__An important note about graphs made using `ggplot2`: you'll notice that throughout this tutorial, the `ggplot2` code is always surrounded by brackets. That way, we both make the graph, assign it to an object, e.g. `duration1` and we "call" the graph, so we can see it in the plot tab. If you don't have the brackets around the code chunk, you'll make the graph, but you won't actually see it. Alternatively, you can "call" the graph to the plot tab by running just the line `duration1`. It's also best to assign your graphs to objects, especially if you want to save them later, otherwise they just disappear and you'll have to run the code again to see or save the graph.__

## Make and beautify maps
<b>Often we find ourselves needing to plot sites or species' occurrences on a map and with `ggplot2` and a combo of a few of its companion packages, we can make nice and clear maps, with the option to choose among different map projections. Here is the journey this particular map of the sites part of the <a href="https://lternet.edu" target="_blank">Long-Term Ecological Research Network</a> are embarking on - small tweaks among the different steps, but ultimately the final map stands out more.</b>

<center><img src="{{ site.baseurl }}/img/beautification1.png" alt="Img" style="width: 950px;"/> </center>

<a id="Acode01" class="copy" name="copy_pre" href="#"> <i class="fa fa-clipboard"></i> Copy Contents </a><br>
<section id= "code01" markdown="1"> 

```r
# MAPS ----
# Get the shape of North America
north_america <- map_data("world", region = c("USA", "Canada"))

# Exclude Hawaii if you want to
north_america <- north_america[!(north_america$subregion %in% "Hawaii"),]

# A very basic map
(lter_map1 <- ggplot() +
    geom_map(map = north_america, data = north_america,
             aes(long, lat, map_id = region), 
             color = "gray80", fill = "gray80", size = 0.3) +
    # Add points for the site locations
    geom_point(data = lter, 
               aes(x = long, y = lat)))

# You can ignore this warning message, it's cause we have forced
# specific lat and long columns onto geom_map()
# Warning: Ignoring unknown aesthetics: x, y

# if you wanted to save this (not amazing) map
# you can use ggsave()
ggsave(lter_map1, filename = "map1.png",
       height = 5, width = 8)  # the units by default are in inches
       
# the map will be saved in your working directory
# if you have forgotten where that is, use this code to find out
get_wd()
```
</section>

<center> <img src="{{ site.baseurl }}/img/map1.png" alt="Img" style="width: 600px;"/> </center>

Our first map does a not terrible job at visualising where the sites are, but it looks rather off and is not particularly great to look at. It's also not communicating much information other than where the sites are. For example, we can use colours to indicate the elevation of each site.

<a id="Acode01" class="copy" name="copy_pre" href="#"> <i class="fa fa-clipboard"></i> Copy Contents </a><br>
<section id= "code01" markdown="1"> 

```r
(lter_map2 <- ggplot() +
    geom_map(map = north_america, data = north_america,
             aes(long, lat, map_id = region), 
             color = "gray80", fill = "gray80", size = 0.3) +
    geom_point(data = lter, 
               aes(x = long, y = lat, fill = ele),
	       # when you set the fill or colour to vary depending on a variable
	       # you put that (e.g., fill = ele) inside the aes() call
	       # when you want to set a specific colour (e.g., colour = "grey30"),
	       # that goes outside of the aes() call
               alpha = 0.8, size = 4, colour = "grey30",
               shape = 21))

ggsave(lter_map2, filename = "map2.png",
       height = 5, width = 8)
```
</section>

<center> <img src="{{ site.baseurl }}/img/map2.png" alt="Img" style="width: 600px;"/> </center>

Next up we can work on improving the map projection - by default we get the Mercantor projection but that doesn't represent the world very realistically. With the `ggalt` package and the `coord_proj` function, we can easily swap the default projection.

<a id="Acode01" class="copy" name="copy_pre" href="#"> <i class="fa fa-clipboard"></i> Copy Contents </a><br>
<section id= "code01" markdown="1"> 

```r
(lter_map3 <- ggplot() +
    geom_map(map = north_america, data = north_america,
             aes(long, lat, map_id = region), 
             color = "gray80", fill = "gray80", size = 0.3) +
    # you can change the projection here
    # coord_proj("+proj=wintri") +
    # the wintri one above is good for the whole world, the one below for just North America
    coord_proj(paste0("+proj=aea +lat_1=29.5 +lat_2=45.5 +lat_0=37.5 +lon_0=-96",
                      " +x_0=0 +y_0=0 +ellps=GRS80 +datum=NAD83 +units=m +no_defs")) +
    geom_point(data = lter, 
               aes(x = long, y = lat, fill = ele),
               alpha = 0.8, size = 4, colour = "grey30",
               shape = 21))

# You don't need to worry about the warning messages
# that's just cause we've overwritten the default projection

ggsave(lter_map3, filename = "map3.png",
       height = 5, width = 8)
```
</section>

<center> <img src="{{ site.baseurl }}/img/map3.png" alt="Img" style="width: 600px;"/> </center>

The projection is better now, but because there are a few faraway sites, the map looks quite small. Since those sites are not going to be our focus, we can zoom in on the map.

<a id="Acode01" class="copy" name="copy_pre" href="#"> <i class="fa fa-clipboard"></i> Copy Contents </a><br>
<section id= "code01" markdown="1"> 

```r
(lter_map4 <- ggplot() +
    geom_map(map = north_america, data = north_america,
             aes(long, lat, map_id = region), 
             color = "gray80", fill = "gray80", size = 0.3) +
    coord_proj(paste0("+proj=aea +lat_1=29.5 +lat_2=45.5 +lat_0=37.5 +lon_0=-96",
                      " +x_0=0 +y_0=0 +ellps=GRS80 +datum=NAD83 +units=m +no_defs"),
	       # zooming in by setting specific coordinates
               ylim = c(25, 80), xlim = c(-175, -50)) +
    geom_point(data = lter, 
               aes(x = long, y = lat, fill = ele),
               alpha = 0.8, size = 4, colour = "grey30",
               shape = 21))

ggsave(lter_map4, filename = "map4.png",
       height = 5, width = 8)
```
</section>

<center> <img src="{{ site.baseurl }}/img/map4.png" alt="Img" style="width: 600px;"/> </center>

Next up we can declutter a bit - we don't really need that grey background and people know that on a map you have latitude and longitude as the axes.

<a id="Acode01" class="copy" name="copy_pre" href="#"> <i class="fa fa-clipboard"></i> Copy Contents </a><br>
<section id= "code01" markdown="1"> 

```r
(lter_map5 <- ggplot() +
    geom_map(map = north_america, data = north_america,
             aes(long, lat, map_id = region), 
             color = "gray80", fill = "gray80", size = 0.3) +
    coord_proj(paste0("+proj=aea +lat_1=29.5 +lat_2=45.5 +lat_0=37.5 +lon_0=-96",
                      " +x_0=0 +y_0=0 +ellps=GRS80 +datum=NAD83 +units=m +no_defs"),
               ylim = c(25, 80), xlim = c(-175, -50)) +
    geom_point(data = lter, 
               aes(x = long, y = lat, fill = ele),
               alpha = 0.8, size = 4, colour = "grey30",
               shape = 21) +
    # Adding a clean map theme
    theme_map() +
    # Putting the legend at the bottom
    theme(legend.position = "bottom"))

ggsave(lter_map5, filename = "map5.png",
       height = 5, width = 8)
```
</section>

<center> <img src="{{ site.baseurl }}/img/map5.png" alt="Img" style="width: 600px;"/> </center>

Sometimes we want to annotate points and communicate what's where - the `ggrepel` package is very useful in such cases.

<a id="Acode01" class="copy" name="copy_pre" href="#"> <i class="fa fa-clipboard"></i> Copy Contents </a><br>
<section id= "code01" markdown="1"> 

```r
(lter_map6 <- ggplot() +
    geom_map(map = north_america, data = north_america,
             aes(long, lat, map_id = region), 
             color = "gray80", fill = "gray80", size = 0.3) +
    coord_proj(paste0("+proj=aea +lat_1=29.5 +lat_2=45.5 +lat_0=37.5 +lon_0=-96",
                      " +x_0=0 +y_0=0 +ellps=GRS80 +datum=NAD83 +units=m +no_defs"),
               ylim = c(25, 80), xlim = c(-175, -50)) +
    geom_point(data = lter, 
               aes(x = long, y = lat, fill = ele),
               alpha = 0.8, size = 4, colour = "grey30",
               shape = 21) +
    theme_map() +
    theme(legend.position = "bottom") +
    # Adding point annotations with the site name
    geom_label_repel(data = lter,
                     aes(x = long, y = lat,
                         label = site),
		     # Setting the positions of the labels
                     box.padding = 1, size = 4, nudge_x = 1, nudge_y = 1))

ggsave(lter_map6, filename = "map6.png",
       height = 5, width = 8)
```
</section>

<center> <img src="{{ site.baseurl }}/img/map6.png" alt="Img" style="width: 600px;"/> </center>

Well, we _slightly_ overdid it with the labels, we have a lot of sites and it's definitely an eye sore to look at all of their names at once. But where annotations really shine is in drawing attention to a specific point or data record. So we can add a label just for one of the sites, Niwot Ridge, from where the plant data for the rest of the tutorial comes.

<a id="Acode01" class="copy" name="copy_pre" href="#"> <i class="fa fa-clipboard"></i> Copy Contents </a><br>
<section id= "code01" markdown="1"> 

```r
(lter_map7 <- ggplot() +
    geom_map(map = north_america, data = north_america,
             aes(long, lat, map_id = region), 
             color = "gray80", fill = "gray80", size = 0.3) +
    coord_proj(paste0("+proj=aea +lat_1=29.5 +lat_2=45.5 +lat_0=37.5 +lon_0=-96",
                      " +x_0=0 +y_0=0 +ellps=GRS80 +datum=NAD83 +units=m +no_defs"),
               ylim = c(25, 80), xlim = c(-175, -50)) +
    geom_point(data = lter, 
               aes(x = long, y = lat, fill = ele),
               alpha = 0.8, size = 4, colour = "grey30",
               shape = 21) +
    theme_map() +
    theme(legend.position = "bottom") +
    geom_label_repel(data = subset(lter, ele > 2000),
                     aes(x = long, y = lat,
                         label = site),
                     box.padding = 1, size = 4, nudge_x = 1, nudge_y = 12))

ggsave(lter_map7, filename = "map7.png",
       height = 5, width = 8)
```
</section>

<center> <img src="{{ site.baseurl }}/img/map7.png" alt="Img" style="width: 600px;"/> </center>

This is looking better, but the colours are not very exciting. Depending on the purpose of the map and where it's going (e.g., presentation, manuscript, a science communication piece), we can also add some text with an interesting fact about the site.

<a id="Acode01" class="copy" name="copy_pre" href="#"> <i class="fa fa-clipboard"></i> Copy Contents </a><br>
<section id= "code01" markdown="1"> 

```r
(lter_map8 <- ggplot() +
    geom_map(map = north_america, data = north_america,
             aes(long, lat, map_id = region), 
             color = "gray80", fill = "gray80", size = 0.3) +
    coord_proj(paste0("+proj=aea +lat_1=29.5 +lat_2=45.5 +lat_0=37.5 +lon_0=-96",
                      " +x_0=0 +y_0=0 +ellps=GRS80 +datum=NAD83 +units=m +no_defs"),
               ylim = c(25, 80), xlim = c(-175, -50)) +
    geom_point(data = lter, 
               aes(x = long, y = lat, fill = ele),
               alpha = 0.8, size = 4, colour = "grey30",
               shape = 21) +
    theme_map() +
    theme(legend.position = "bottom") +
    geom_label_repel(data = subset(lter, ele > 2000),
                     aes(x = long, y = lat,
                         label = site),
                     box.padding = 1, size = 4, nudge_x = 1, nudge_y = 12) +
    labs(fill = "Elevation (m)") +
    annotate("text", x = -150, y = 35, colour = "#553c7f",
             label = "At 3528 m above sea level,\nNiwot Ridge is\nthe highest LTER site.",
             size = 4.5, fontface = "bold") +
    scale_fill_viridis(option = "magma", direction = -1, begin = 0.2))

ggsave(lter_map8, filename = "map8.png",
       height = 5, width = 8)
```
</section>

<center> <img src="{{ site.baseurl }}/img/map8.png" alt="Img" style="width: 600px;"/> </center>

<b>There goes our map! Hard to say our "finished" map, because figures evolve a lot, but for now we'll leave the map here and move onto distributions - a great way to communicate the whole spectrum of variance in your dataset!</b>

<a name="distributions"></a>

## Visualise distributions (and make them rain data with raincloud plots)

<a id="Acode01" class="copy" name="copy_pre" href="#"> <i class="fa fa-clipboard"></i> Copy Contents </a><br>
<section id= "code01" markdown="1"> 

```r

```
</section>

<a id="Acode01" class="copy" name="copy_pre" href="#"> <i class="fa fa-clipboard"></i> Copy Contents </a><br>
<section id= "code01" markdown="1"> 

```r

```
</section>

<a id="Acode01" class="copy" name="copy_pre" href="#"> <i class="fa fa-clipboard"></i> Copy Contents </a><br>
<section id= "code01" markdown="1"> 

```r

```
</section>

# DISTRIBUTIONS ----

theme_niwot <- function(){
  theme_bw() +
    theme(text = element_text(family = "Helvetica Light"),
          axis.text = element_text(size = 16), 
          axis.title = element_text(size = 18),
          axis.line.x = element_line(color="black"), 
          axis.line.y = element_line(color="black"),
          panel.border = element_blank(),
          panel.grid.major.x = element_blank(),                                          
          panel.grid.minor.x = element_blank(),
          panel.grid.minor.y = element_blank(),
          panel.grid.major.y = element_blank(),  
          plot.margin = unit(c(1, 1, 1, 1), units = , "cm"),
          plot.title = element_text(size = 18, vjust = 1, hjust = 0),
          legend.text = element_text(size = 12),          
          legend.title = element_blank(),                              
          legend.position = c(0.95, 0.15), 
          legend.key = element_blank(),
          legend.background = element_rect(color = "black", 
                                           fill = "transparent", 
                                           size = 2, linetype = "blank"))
}

# Calculate species richness per plot per year
niwot_richness <- niwot_plant_exp %>% group_by(plot_num, year) %>%
  mutate(richness = length(unique(USDA_Scientific_Name))) %>% ungroup()

(distributions1 <- ggplot(niwot_richness, aes(x = fert, y = richness)) +
    geom_violin())

ggsave(distributions1, filename = "distributions1.png",
       height = 5, width = 5)

(distributions2 <- ggplot(niwot_richness, aes(x = fert, y = richness)) +
    geom_violin(aes(fill = fert, colour = fert), alpha = 0.5) +
    theme_niwot())

ggsave(distributions2, filename = "distributions2.png",
       height = 5, width = 5)

(distributions3 <- ggplot(niwot_richness, aes(x = fert, y = richness)) +
    geom_violin(aes(fill = fert, colour = fert), alpha = 0.5) +
    geom_boxplot(aes(colour = fert), width = 0.2) +
    theme_niwot())

ggsave(distributions3, filename = "distributions3.png",
       height = 5, width = 5)

(distributions4 <- ggplot(niwot_richness, aes(x = fert, y = richness)) +
    geom_violin(aes(fill = fert, colour = fert), alpha = 0.5) +
    geom_jitter(aes(colour = fert), position = position_jitter(0.1), 
                alpha = 0.3) +
    theme_niwot())

ggsave(distributions4, filename = "distributions4.png",
       height = 5, width = 5)

source("https://gist.githubusercontent.com/benmarwick/2a1bb0133ff568cbe28d/raw/fb53bd97121f7f9ce947837ef1a4c65a73bffb3f/geom_flat_violin.R")

raincloud_theme <- function(){
  theme(
  text = element_text(size = 10),
  axis.title.x = element_text(size = 16),
  axis.title.y = element_text(size = 16),
  axis.text = element_text(size = 14),
  axis.text.x = element_text(vjust = 0.5),
  legend.title = element_text(size = 16),
  legend.text = element_text(size = 16),
  legend.position = "right",
  plot.title = element_text(lineheight = .8, face = "bold", size = 16),
  panel.border = element_blank(),
  panel.grid.minor = element_blank(),
  panel.grid.major = element_blank(),
  axis.line.x = element_line(colour = "black", size = 0.5, linetype = "solid"),
  axis.line.y = element_line(colour = "black", size = 0.5, linetype = "solid"))
}

lb <- function(x) mean(x) - sd(x)
ub <- function(x) mean(x) + sd(x)

sumld <- niwot_richness %>% dplyr::select(fert, richness) %>%
  group_by(fert) %>% 
  summarise_all(funs(mean, median, lower = lb, upper = ub))

(distributions5 <- 
    ggplot(data = niwot_richness, 
           aes(x = reorder(fert, desc(richness)), y = richness, fill = fert)) +
    geom_flat_violin(position = position_nudge(x = 0.2, y = 0), alpha = 0.8) +
    geom_point(aes(y = richness, color = fert), 
               position = position_jitter(width = 0.15), size = 1, alpha = 0.1) +
    geom_boxplot(width = 0.2, outlier.shape = NA, alpha = 0.8) +
    labs(y = "Species richness\n", x = NULL) +
    guides(fill = FALSE) +
    guides(color = FALSE) +
    scale_y_continuous(limits = c(0, 30)) +
    scale_fill_manual(values = c("#5A4A6F", "#E47250",  "#EBB261", "#9D5A6C")) +
    scale_colour_manual(values = c("#5A4A6F", "#E47250",  "#EBB261", "#9D5A6C")) +
    raincloud_theme() +
    theme_niwot())

ggsave(distributions5, filename = "distributions5.png",
       height = 5, width = 5)

(distributions6 <- 
    ggplot(data = niwot_richness, 
           aes(x = reorder(fert, desc(richness)), y = richness, fill = fert)) +
    geom_flat_violin(position = position_nudge(x = 0.2, y = 0), alpha = 0.8) +
    geom_point(aes(y = richness, color = fert), 
               position = position_jitter(width = 0.15), size = 1, alpha = 0.1) +
    geom_boxplot(width = 0.2, outlier.shape = NA, alpha = 0.8) +
    labs(y = "\nSpecies richness", x = NULL) +
    guides(fill = FALSE) +
    guides(color = FALSE) +
    scale_y_continuous(limits = c(0, 30)) +
    scale_fill_manual(values = c("#5A4A6F", "#E47250",  "#EBB261", "#9D5A6C")) +
    scale_colour_manual(values = c("#5A4A6F", "#E47250",  "#EBB261", "#9D5A6C")) +
    coord_flip() +
    raincloud_theme() +
    theme_niwot())

ggsave(distributions6, filename = "distributions6.png",
       height = 5, width = 5)

# Create new columns based on a combo of conditions using case_when()
alpine_magic <- niwot_richness %>% mutate(fairy_dust = case_when(fert == "PP" & hits > 5 ~ "Blue fairy dust",
                                                                 fert == "CC" & hits > 15 ~ "The ultimate fairy dust"))

(distributions_magic <- 
    ggplot(data = alpine_magic, 
           aes(x = reorder(fairy_dust, desc(richness)), y = richness, fill = fairy_dust)) +
    geom_flat_violin(position = position_nudge(x = 0.2, y = 0), alpha = 0.8) +
    geom_point(aes(y = richness, color = fairy_dust), 
               position = position_jitter(width = 0.15), size = 1, alpha = 0.1) +
    geom_boxplot(width = 0.2, outlier.shape = NA, alpha = 0.8) +
    labs(y = "\nSpecies richness", x = NULL) +
    guides(fill = FALSE) +
    guides(color = FALSE) +
    scale_y_continuous(limits = c(0, 30)) +
    scale_fill_manual(values = c("turquoise4", "magenta4")) +
    scale_colour_manual(values = c("turquoise4", "magenta4")) +
    coord_flip() +
    raincloud_theme() +
    theme_niwot())

alpine_magic_only <- alpine_magic %>% drop_na(fairy_dust)

(distributions_magic2 <- 
    ggplot(data = alpine_magic_only, 
           aes(x = reorder(fairy_dust, desc(richness)), y = richness, fill = fairy_dust)) +
    geom_flat_violin(position = position_nudge(x = 0.2, y = 0), alpha = 0.8) +
    geom_point(aes(y = richness, color = fairy_dust), 
               position = position_jitter(width = 0.15), size = 1, alpha = 0.1) +
    geom_boxplot(width = 0.2, outlier.shape = NA, alpha = 0.8) +
    labs(y = "\nSpecies richness", x = NULL) +
    guides(fill = FALSE) +
    guides(color = FALSE) +
    scale_y_continuous(limits = c(0, 30)) +
    scale_fill_manual(values = c("turquoise4", "magenta4")) +
    scale_colour_manual(values = c("turquoise4", "magenta4")) +
    coord_flip() +
    raincloud_theme() +
    theme_niwot())

ggsave(distributions_magic2, filename = "distributions_magic2.png",
       height = 5, width = 5)





If you've ever tried to perfect your `ggplot2` graphs, you might have noticed that the lines starting with `theme()` quickly pile up: you adjust the font size of the axes and the labels, the position of the title, the background colour of the plot, you remove the grid lines in the background, etc. And then you have to do the same for the next plot, which really increases the amount of code you use. Here is a simple solution: create a customised theme that combines all the `theme()` elements you want and apply it to your graphs to make things easier and increase consistency. You can include as many elements in your theme as you want, as long as they don't contradict one another and then when you apply your theme to a graph, only the relevant elements will be considered - e.g. for our graphs we won't need to use `legend.position`, but it's fine to keep it in the theme in case any future graphs we apply it to do have the need for legends.

```r
# Setting a custom ggplot2 function ---
# This function makes a pretty ggplot theme
# This function takes no arguments 
# meaning that you always have just niwot_theme() and not niwot_theme(something else here)
theme_clean <- function(){
  theme_bw() +
    theme(axis.text.x = element_text(size = 14),
          axis.text.y = element_text(size = 14),
          axis.title.x = element_text(size = 14, face = "plain"),             
          axis.title.y = element_text(size = 14, face = "plain"),             
          panel.grid.major.x = element_blank(),                                          
          panel.grid.minor.x = element_blank(),
          panel.grid.minor.y = element_blank(),
          panel.grid.major.y = element_blank(),  
          plot.margin = unit(c(0.5, 0.5, 0.5, 0.5), units = , "cm"),
          plot.title = element_text(size = 15, vjust = 1, hjust = 0.5),
          legend.text = element_text(size = 12, face = "italic"),          
          legend.title = element_blank(),                              
          legend.position = c(0.5, 0.8))
}
```



```r
# Check the distribution of duration across the time-series
# A quick and not particularly pretty graph
(duration_hist <- ggplot(aus_pops, aes(x = duration)) +
    geom_histogram())
```

<center> <img src="{{ site.baseurl }}/img/hist1a.png" alt="Img" style="width: 500px;"/> </center>

This graph just uses all the `ggplot2` default settings. It's fine if you just want to see the distribution and move on, but if you plan to save the graph and share it with other people, we can make it way better. The figure beautification journey!

<b> When using `ggplot2`, you usually start your code with `ggplot(your_data, aes(x = independent_variable, y = dependent_variable))`, then you add the type of plot you want to make using `+ geom_boxplot()`, `+ geom_histogram()`, etc. `aes` stands for aesthetics, hinting to the fact that using `ggplot2` you can make aesthetically pleasing graphs - there are many `ggplot2` functions to help you clearly communicate your results, and we will now go through some of them.</b>

<b>When we want to change the colour, shape or fill of a variable based on another variable, e.g. colour-code by species, we include `colour = species` inside the `aes()` function. When we want to set a specific colour, shape or fill, e.g. `colour = "black"`, we put that outside of the `aes()` function.</b>

```r
(duration_hist <- ggplot() +
    geom_histogram(data = aus_pops, aes(x = duration), alpha = 0.6, 
                   breaks = seq(5, 40, by = 1), fill = "turquoise4"))

(duration_hist <- ggplot(aus_pops, aes(x = duration)) +
    geom_histogram(alpha = 0.6, 
                   breaks = seq(5, 40, by = 1), 
		   fill = "turquoise4") +
    # setting new colours, changing the opacity and defining custom bins
    scale_y_continuous(limits = c(0, 600), expand = expand_scale(mult = c(0, 0.1))))
    # the final line of code removes the empty blank space below the bars
```

<center> <img src="{{ site.baseurl }}/img/hist1b.png" alt="Img" style="width: 500px;"/>  <img src="{{ site.baseurl }}/img/hist5.png" alt="Img" style="width: 500px;"/></center>

Now imagine you want to have a darker blue outline around the whole histogram - not around each individual bin, but the whole shape. It's the little things that add up to make nice graphs! We can use `geom_step()` to create the histogram outline, but we have to put the steps in a data frame first. The three lines of code below are a bit of a cheat to create the histogram outline effect. Check out the object `d1` to see what we've made.

```r
# Adding an outline around the whole histogram
h <- hist(aus_pops$duration, breaks = seq(5, 40, by = 1), plot = FALSE)
d1 <- data.frame(x = h$breaks, y = c(h$counts, NA))  
d1 <- rbind(c(5,0), d1)
```

__When we want to plot data from different data frames in the same graph, we have to move the data frame from the main `ggplot()` call to the specific part of the graph where we want to use each dataset. Compare the code below with the code for the previous versions of the histograms to spot the difference.__

```r
(duration_hist <- ggplot() +
    geom_histogram(data = aus_pops, aes(x = duration), alpha = 0.6, 
                   breaks = seq(5, 40, by = 1), fill = "turquoise4") +
    scale_y_continuous(limits = c(0, 600), expand = expand_scale(mult = c(0, 0.1))) +
    geom_step(data = d1, aes(x = x, y = y),
              stat = "identity", colour = "deepskyblue4"))

summary(d1) # it's fine, you can ignore the warning message
# it's because some values don't have bars
# thus there are missing "steps" along the geom_step path
```

<center> <img src="{{ site.baseurl }}/img/hist4.png" alt="Img" style="width: 500px;"/> </center>

We can also add a line for the mean duration across studies and add an annotation on the graph so that people can quickly see what the line means.

```r
(duration_hist <- ggplot() +
    geom_histogram(data = aus_pops, aes(x = duration), alpha = 0.6, 
                   breaks = seq(5, 40, by = 1), fill = "turquoise4") +
    scale_y_continuous(limits = c(0, 600), expand = expand_scale(mult = c(0, 0.1))) +
    geom_step(data = d1, aes(x = x, y = y),
              stat = "identity", colour = "deepskyblue4") +
    geom_vline(xintercept = mean(aus_pops$duration), linetype = "dotted",
               colour = "deepskyblue4", size = 1))

(duration_hist <- ggplot() +
    geom_histogram(data = aus_pops, aes(x = duration), alpha = 0.6, 
                   breaks = seq(5, 40, by = 1), fill = "turquoise4") +
    scale_y_continuous(limits = c(0, 600), expand = expand_scale(mult = c(0, 0.1))) +
    geom_step(data = d1, aes(x = x, y = y),
              stat = "identity", colour = "deepskyblue4") +
    geom_vline(xintercept = mean(aus_pops$duration), linetype = "dotted",
               colour = "deepskyblue4", size = 1) +
    # Adding in a text allocation - the coordinates are based on the x and y axes
    annotate("text", x = 15, y = 500, label = "The mean duration\n was 23 years.") +
    # "\n" creates a line break
    geom_curve(aes(x = 15, y = 550, xend = mean(aus_pops$duration) - 1, yend = 550),
               arrow = arrow(length = unit(0.07, "inch")), size = 0.7,
               color = "grey20", curvature = -0.3))
    # Similarly to the annotation, the curved line follows the plot's coordinates
    # Have a go at changing the curve parameters to see what happens
```

<center> <img src="{{ site.baseurl }}/img/hist3.png" alt="Img" style="width: 500px;"/>  <img src="{{ site.baseurl }}/img/hist2.png" alt="Img" style="width: 500px;"/></center>

We are super close to a nice histogram - all we are missing is letting it "shine". The default `ggplot2` theme is a bit cluttered and the grey background and lines distract from the main message of the graph. At the start of the tutorial we made our own clean theme, time to put it in action!

```r
(duration_hist <- ggplot() +
  geom_histogram(data = aus_pops, aes(x = duration), alpha = 0.6, 
                 breaks = seq(5, 40, by = 1), fill = "turquoise4") +
  scale_y_continuous(limits = c(0, 600), expand = expand_scale(mult = c(0, 0.1))) +
  geom_step(data = d1, aes(x = x, y = y),
            stat = "identity", colour = "deepskyblue4") +
  geom_vline(xintercept = mean(aus_pops$duration), linetype = "dotted",
             colour = "deepskyblue4", size = 1) +
  annotate("text", x = 15, y = 500, label = "The mean duration\n was 23 years.") +
  geom_curve(aes(x = 15, y = 550, xend = mean(aus_pops$duration) - 1, yend = 550),
             arrow = arrow(length = unit(0.07, "inch")), size = 0.7,
             color = "grey20", curvature = -0.3) +
  labs(x = "\nDuration", y = "Number of time-series\n") +
  theme_clean())
```

<center> <img src="{{ site.baseurl }}/img/hist1.png" alt="Img" style="width: 500px;"/> </center>

There's our histogram! We can save it using `ggsave`. The units for the height and width are in inches. Unless you specify a different file path, the graph will go in your working directory. If you've forgotten where that is, you can easily find out by running `getwd()` in the console.

```r
ggsave(duration_hist, filename = "hist1.png",
       height = 5, width = 6)
```

## Extra resources

## Check out our new free online course <a href="https://ourcodingclub.github.io/course_home/" target="_blank">"Data Science for Ecologists and Environmental Scientists"</a>!

To learn more about the power of pipes check out:
<a href = "http://dplyr.tidyverse.org/" target ="_blank"> the tidyverse website</a> and <a href="http://r4ds.had.co.nz/pipes.html" target="_blank"> the R for Data Science book</a>.

To learn more about the `tidyverse` in general, check out Charlotte Wickham's slides <a href="https://github.com/cwickham/data-science-in-tidyverse/tree/master/slides" target="_blank">here</a>.



<hr>
<hr>



<h3><a href="https://www.surveymonkey.com/r/XD85MW5" target="_blank">&nbsp; We would love to hear your feedback, please fill out our survey!</a></h3>

<br>
<h3>&nbsp; You can contact us with any questions on <a href="mailto:ourcodingclub@gmail.com?Subject=Tutorial%20question" target = "_top">ourcodingclub@gmail.com</a></h3>
<br>
<h3>&nbsp; Related tutorials:</h3>
{% for post in site.posts %}
	{% if post.url != page.url %}
  		{% for tag in post.tags %}
    			{% if page.tags contains tag %}
<h4><a style="margin:0 padding:0" href="{{ post.url }}">&nbsp; - {{ post.title }}</a></h4>
  			{% endif %}
		{% endfor %}
	{% endif %}
{% endfor %}
<br>
<h3>&nbsp; Subscribe to our mailing list:</h3>
<div class="container">
	<div class="block">
        <!-- subscribe form start -->
		<div class="form-group">
			<form action="https://getsimpleform.com/messages?form_api_token=de1ba2f2f947822946fb6e835437ec78" method="post">
			<div class="form-group">
				<input type='text' class="form-control" name='Email' placeholder="Email" required/>
			</div>
			<div>
                        	<button class="btn btn-default" type='submit'>Subscribe</button>
                    	</div>
                	</form>
		</div>
	</div>
</div>

<ul class="social-icons">
	<li>
		<h3>
			<a href="https://twitter.com/our_codingclub" target="_blank">&nbsp;Follow our coding adventures on Twitter! <i class="fa fa-twitter"></i></a>
		</h3>
	</li>
</ul>