# Plotting spatial data in R

In this workshop you will learn how to plot spatial data in R by using the **tmap** package. This package is an implementation of the grammar of graphics for thematic maps, and resembles the syntax of **ggplot2**. This package is useful for both *exploration* and *publication* of spatial data, and offers both *static* and *interactive* plotting.

For those of you who are unfamiliar with spatial data in R, we will briefly introduce the fundamental packages for spatial data, which are **sf**, **sp**, and **raster**. With demonstrations and exercises, you will learn how to process spatial objects from various types (polygons, points, lines, rasters, and simple features), and how to plot them. Feel free to bring your own spatial data.

Besides plotting spatial data, we will also discuss the possibilities of *publication*. Maps created with **tmap** can be exported as static images, html files, but they can also be embedded in **rmarkdown** documents and **shiny** apps.

R packages: tmap, sf, sp, raster, rmarkdown, shiny

Tennekes, M. (2018) tmap: Thematic Maps in R. Forthcoming in the Journal of Statistical Software (JSS).


### Overview of CRAN pacakges on spatial data

177 CRAN packages are listed in the [CRAN Task View: Analysis of Spatial Data](https://cran.r-project.org/web/views/Spatial.html)
I can imagine, you can't see the wood for the trees anymore. An excellent online book to get started with spatial data is: https://geocompr.robinlovelace.net/, which was also the topic of the Workshop this morning (https://github.com/jannes-m/erum18_geocompr). There are two package which are fundamental:

* `sf` classes and methods for vector data (it is replacing `sp`, currently the most frequenctly used R package on spatial R)
* `raster` classes and methods for raster data (will eventually be replaced by `stars`)

These two packages will allow you to do all basic analysis and visualization of spatial data.


The `tmap` package is build on top of the shoulders of giants. As a consequence, once you install tmap, the most important other packages that are useful for spatial data will be installed as well. Note that installation may require some effort. 


### Installation of tmap

You can install either from CRAN (version 1.11-2) of from github (version 2.0). 

The tmap package will have a major update (version 2.0) soon. The github version is 2.0, while the CRAN version is 1.11-2. If you would like to use version 2.0, but still want to be able to fall back to (the more stable) 1.11-2, you can use the following approach:

```{r}
install.packages(c("devtools", "tmap"))

library(devtools)
dev_mode()
install_github("mtennekes/tmaptools")
install_github("mtennekes/tmap")
```

See https://github.com/mtennekes/tmap/#installation for installation instructions, which is especially useful for Linux users.

For those of you who use Docker, see https://hub.docker.com/r/robinlovelace/geocompr which contains all packages needed for spatial data visualization (including tmap version 2.0).

Loading the required packages:

```{r}
library(sf)
library(raster)
library(tmap)
library(tmaptools)
```


## Getting spetial data

It's your choice what spatial data you want to use in this workshop. Some suggestions:

There are a couple of data sets contained in tmap. The most interesting are `World`, which contains World country data, `metro`, which contains population time series for large metropolitan areas, and `land`, which is rasterized data of land use and tree coverage.

```{r}
library(tmap)
data(World, metro)
```

Thep packages `spData` and `spDataLarge` contain many spatial datasets. See `https://github.com/Nowosad/spData` for an overview of available datasets. 

```{r}
library(spData)
library(spDataLarge) #  install.packages('spDataLarge', repos='https://nowosad.github.io/drat/', type='source'))
```

The pacakge `osmdata` is an interface to OpenStreetMap.

```{r}
library(osmdata)

q <- opq("Budapest")
q_smkt <- add_osm_feature(q, key = "shop", value = "supermarket", value_exact = FALSE)
x_smkt <- osmdata_sf(q_smkt)
```

The package `rnaturalearth` is an interface to `www.naturalearthdata.com`, a great source of shapes.

```{r}
library(rnaturalearth)
airports <- ne_download( scale = 10, type = 'ports' )
```

## Assignment

Your first task is to explore the spatial data sets you are using.

