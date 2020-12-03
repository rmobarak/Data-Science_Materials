---
title: 'Weekly Exercises #5'
author: "Rayyan Mobarak"
worked with: "Donia Kharaishi"
output: 
  html_document:
    keep_md: TRUE
    toc: TRUE
    toc_float: TRUE
    df_print: paged
    code_download: true
---





```r
library(tidyverse)     # for data cleaning and plotting
library(googlesheets4) # for reading googlesheet data
library(lubridate)     # for date manipulation
library(openintro)     # for the abbr2state() function
library(palmerpenguins)# for Palmer penguin data
library(maps)          # for map data
library(ggmap)         # for mapping points on maps
library(gplots)        # for col2hex() function
library(RColorBrewer)  # for color palettes
library(sf)            # for working with spatial data
library(leaflet)       # for highly customizable mapping
library(ggthemes)      # for more themes (including theme_map())
library(plotly)        # for the ggplotly() - basic interactivity
library(gganimate)     # for adding animation layers to ggplots
library(transformr)    # for "tweening" (gganimate)
library(shiny)         # for creating interactive apps
library(gifski)
library(ggridges)
library(gganimate)
library(ggimage)
gs4_deauth()           # To not have to authorize each time you knit.
theme_set(theme_minimal())
```


```r
# SNCF Train data
small_trains <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-02-26/small_trains.csv") 

# Lisa's garden data
garden_harvest <- read_sheet("https://docs.google.com/spreadsheets/d/1DekSazCzKqPS2jnGhKue7tLxRU3GVL1oxi-4bEM5IWw/edit?usp=sharing") %>% 
  mutate(date = ymd(date))

# Lisa's Mallorca cycling data
mallorca_bike_day7 <- read_csv("https://www.dropbox.com/s/zc6jan4ltmjtvy0/mallorca_bike_day7.csv?dl=1") %>% 
  select(1:4, speed)

# Heather Lendway's Ironman 70.3 Pan Am championships Panama data
panama_swim <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_swim_20160131.csv")

panama_bike <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_bike_20160131.csv")

panama_run <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_run_20160131.csv")

#COVID-19 data from the New York Times
covid19 <- read_csv("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv")
```

## Put your homework on GitHub!

Go [here](https://github.com/llendway/github_for_collaboration/blob/master/github_for_collaboration.md) or to previous homework to remind yourself how to get set up. 

Once your repository is created, you should always open your **project** rather than just opening an .Rmd file. You can do that by either clicking on the .Rproj file in your repository folder on your computer. Or, by going to the upper right hand corner in R Studio and clicking the arrow next to where it says Project: (None). You should see your project come up in that list if you've used it recently. You could also go to File --> Open Project and navigate to your .Rproj file. 

## Instructions

* Put your name at the top of the document. 

* **For ALL graphs, you should include appropriate labels.** 

* Feel free to change the default theme, which I currently have set to `theme_minimal()`. 

* Use good coding practice. Read the short sections on good code with [pipes](https://style.tidyverse.org/pipes.html) and [ggplot2](https://style.tidyverse.org/ggplot2.html). **This is part of your grade!**

* **NEW!!** With animated graphs, add `eval=FALSE` to the code chunk that creates the animation and saves it using `anim_save()`. Add another code chunk to reread the gif back into the file. See the [tutorial](https://animation-and-interactivity-in-r.netlify.app/) for help. 

* When you are finished with ALL the exercises, uncomment the options at the top so your document looks nicer. Don't do it before then, or else you might miss some important warnings and messages.

## Warm-up exercises from tutorial

  1. Choose 2 graphs you have created for ANY assignment in this class and add interactivity using the `ggplotly()` function.
  
 


```r
perfect_garden_graph <- garden_harvest %>%
  ggplot(aes(x = date, y = weight))+
  theme(plot.background = element_rect(fill = "#BFD5E3"),panel.grid.major.x = element_blank(),
    panel.grid.minor.x = element_blank(),axis.line = element_line(size = 1.5, colour = "dark blue"))+
  geom_point(color = "red") +
    labs(title = "Relationship of weight of vegetables in grams(g) with date", x = "", y = "")+
  geom_smooth(color = "purple", se = FALSE) 
ggplotly(perfect_garden_graph,
         tooltip = c("text", "x"))
```

<!--html_preserve--><div id="htmlwidget-9d926fcdcca5f6477614" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-9d926fcdcca5f6477614">{"x":{"data":[{"x":[18419,18419,18421,18422,18424,18424,18424,18424,18426,18426,18426,18426,18430,18430,18430,18430,18430,18431,18431,18431,18431,18432,18432,18432,18432,18433,18433,18433,18433,18433,18433,18433,18434,18434,18434,18434,18434,18434,18434,18434,18435,18435,18435,18435,18435,18435,18436,18436,18436,18436,18436,18437,18437,18438,18438,18439,18439,18440,18440,18440,18440,18441,18441,18441,18442,18442,18442,18442,18442,18442,18443,18443,18444,18445,18445,18445,18445,18446,18446,18446,18446,18447,18447,18447,18449,18449,18449,18449,18449,18449,18450,18450,18450,18450,18450,18450,18451,18451,18451,18451,18451,18451,18451,18451,18452,18452,18452,18452,18452,18453,18453,18454,18454,18454,18454,18454,18454,18454,18455,18455,18455,18455,18456,18456,18456,18456,18456,18456,18456,18456,18457,18457,18457,18457,18457,18458,18458,18458,18458,18459,18459,18459,18460,18460,18460,18460,18460,18461,18461,18461,18461,18461,18461,18462,18462,18462,18462,18462,18463,18463,18463,18463,18463,18463,18463,18463,18463,18463,18463,18463,18464,18464,18464,18464,18464,18464,18464,18465,18465,18465,18465,18466,18466,18466,18466,18466,18467,18467,18467,18467,18467,18467,18467,18467,18467,18467,18467,18467,18467,18467,18468,18468,18468,18468,18469,18469,18470,18470,18470,18470,18470,18470,18470,18470,18470,18470,18470,18470,18470,18471,18471,18471,18471,18471,18471,18471,18471,18472,18472,18472,18472,18472,18472,18472,18472,18472,18472,18473,18473,18473,18473,18473,18473,18473,18474,18474,18474,18474,18474,18474,18474,18474,18474,18474,18474,18475,18475,18475,18475,18475,18475,18475,18475,18475,18475,18475,18475,18476,18476,18476,18476,18476,18476,18476,18477,18477,18477,18477,18477,18477,18478,18478,18478,18478,18478,18478,18478,18478,18478,18478,18478,18478,18478,18478,18478,18478,18479,18479,18479,18479,18479,18479,18479,18479,18479,18480,18480,18480,18480,18480,18480,18480,18480,18480,18480,18481,18481,18481,18481,18481,18481,18481,18481,18481,18481,18481,18482,18482,18482,18482,18482,18482,18482,18482,18482,18482,18483,18483,18483,18483,18483,18483,18483,18483,18483,18484,18484,18484,18484,18484,18484,18484,18485,18485,18485,18485,18485,18485,18485,18485,18485,18485,18485,18485,18485,18485,18485,18485,18486,18487,18487,18487,18487,18487,18487,18487,18487,18487,18487,18487,18487,18487,18487,18487,18487,18488,18488,18488,18488,18488,18488,18488,18488,18488,18488,18489,18489,18489,18489,18489,18489,18489,18490,18490,18490,18490,18490,18490,18490,18490,18490,18490,18490,18491,18491,18491,18491,18491,18491,18491,18491,18491,18491,18491,18491,18492,18492,18492,18492,18492,18492,18492,18492,18492,18492,18492,18492,18492,18492,18492,18492,18493,18493,18493,18493,18493,18493,18493,18493,18493,18493,18493,18494,18494,18494,18494,18494,18494,18494,18494,18494,18494,18494,18494,18494,18494,18494,18494,18494,18495,18495,18495,18495,18495,18495,18495,18495,18495,18495,18495,18495,18495,18497,18497,18497,18497,18497,18497,18497,18497,18497,18497,18497,18498,18498,18498,18498,18499,18499,18499,18499,18499,18499,18499,18499,18499,18499,18499,18499,18499,18500,18500,18500,18500,18500,18500,18500,18500,18500,18500,18501,18502,18502,18502,18503,18503,18503,18503,18503,18503,18503,18503,18503,18503,18503,18503,18503,18503,18504,18504,18504,18504,18504,18504,18504,18504,18504,18504,18506,18506,18506,18506,18506,18506,18506,18506,18506,18506,18506,18506,18506,18506,18507,18507,18507,18507,18508,18508,18508,18508,18509,18509,18509,18509,18509,18509,18509,18509,18509,18509,18510,18510,18511,18511,18511,18511,18511,18512,18513,18514,18514,18514,18515,18515,18515,18515,18515,18515,18515,18517,18520,18520,18521,18521,18521,18522,18522,18522,18522,18523,18523,18523,18523,18523,18523,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18524,18525,18526,18526,18530,18530,18530,18530,18530,18530,18530,18530,18530,18530,18530,18530,18530,18531,18531,18532,18532,18532,18532,18532,18532,18532,18535,18535,18535,18535,18535,18535,18535,18536,18537,18537,18537,18538,18538,18538,18539,18542,18542,18542,18542,18542,18542,18542,18543,18543,18545,18545,18545,18545,18546,18546,18546,18546,18546,18546,18546,18546,18546,18546,18546,18546,18547,18547,18547,18547,18547,18547,18547,18547,18547,18547,18547,18547,18547,18547,18547,18549,18549,18549,18549,18549,18549,18549,18549,18549,18549,18549,18549,18549,18550,18550,18550,18550,18550,18550,18550,18551,18551,18552,18552,18552,18552,18552,18552,18552,18553,18553,18553,18553,18553,18553,18553,18553,18553,18553,18553,18553],"y":[20,36,15,10,67,12,9,8,53,19,14,10,48,58,8,121,8,40,47,59,25,58,39,11,38,22,25,18,16,71,148,20,37,19,71,95,51,13,57,60,37,52,40,19,19,18,40,165,41,2,5,34,122,22,30,17,425,52,89,60,333,793,99,111,58,23,625,561,30,82,32,80,60,144,16,798,743,217,216,88,9,285,457,147,17,175,235,189,433,48,67,62,10,43,11,13,75,252,178,39,181,83,96,75,61,131,140,69,78,61,150,60,77,19,79,105,701,24,130,89,492,83,47,145,50,85,53,137,40,443,128,152,207,526,152,393,743,1057,39,29,61,50,88,33,16,20,347,77,172,61,81,294,660,113,531,344,37,140,134,179,336,107,128,12,519,559,197,123,178,102,110,86,137,339,21,21,7,76,351,655,23,129,56,466,91,130,525,31,140,247,220,1321,100,32,93,16,3,68,178,80,463,106,121,901,81,148,1542,728,785,113,29,801,99,49,149,39,174,129,372,160,611,203,312,315,131,91,76,153,442,240,209,73,40,457,514,305,280,91,101,19,94,116,107,626,307,197,633,290,100,1215,592,23,31,107,174,435,320,619,97,436,168,164,1130,137,74,17,182,1175,509,857,336,156,211,102,308,252,1155,572,65,383,387,231,73,339,118,270,162,56,192,195,81,87,24,40,44,427,563,290,781,223,382,217,67,41,234,393,307,175,303,127,98,164,442,317,439,359,356,233,364,1045,562,292,1219,1327,255,19,162,81,564,184,108,122,1697,545,445,305,179,591,1102,308,54,64,443,118,302,13,272,168,216,241,309,221,731,302,307,160,755,1029,78,245,218,802,354,359,506,92,109,330,73,1774,468,122,421,332,727,642,413,65,599,12,198,308,517,2209,2476,1564,80,711,238,525,181,266,490,126,371,383,351,859,25,137,71,56,477,328,45,543,599,560,291,238,397,660,693,364,305,588,764,436,306,350,105,30,67,344,173,27,126,112,1151,225,2888,608,136,148,317,105,271,39,87,233,527,323,278,31,872,579,615,997,335,264,451,306,99,70,333,483,632,360,230,344,1010,328,287,322,493,252,70,834,113,1122,34,509,1601,842,1538,428,243,330,997,265,562,457,1542,801,436,747,1573,704,446,269,661,2436,111,134,115,75,117,578,871,115,629,186,320,488,506,920,179,1400,993,1026,1886,666,1042,593,216,309,497,261,819,1607,14,29,3244,85,24,289,380,737,1033,1097,483,627,352,262,716,888,566,169,861,460,2934,599,155,822,589,393,752,833,2831,1953,160,4758,2342,3227,5150,7350,805,178,201,1537,773,1202,798,370,43,60,1131,610,1265,102,2160,2899,442,1234,1178,255,430,33,256,58,214,1644,2377,710,1317,1649,615,3284,1300,843,102,228,692,674,1392,316,754,413,509,108,258,725,629,219,8,160,168,191,212,714,228,670,1052,1631,137,2934,304,1058,307,397,537,314,494,484,454,480,252,294,437,1834,1655,1927,1558,1183,1178,706,1686,1785,1923,2120,2325,1172,1311,6250,1154,1208,2882,2689,3441,7050,1109,1028,1131,1302,1570,1359,1608,2277,1743,2931,163,714,95,477,2738,236,1823,819,2006,659,1239,1978,28,24,75,84,156,95,94,81,139,134,883,449,232,88,92,1447,494,678,70,327,127,1596,101,145,252,213,346,39,254,363,715,272,64,17,169,372,436,1377,1977,258,23,2478,200,375,316,898,526,386,230,84,119,144,437,1031,2322,296,312,709,2143,1950,1291,1627,4372,5000,2990,1300,2710,137,859,791,1175,418,484,219,646,2838,1500,1023,328,175,89,3800,5700,3600,1527,272,1718,295,883,740,310,932,1096,1101,293,183,77,2001,673,144,366,1393,903,419,1026,1350,297,52,114],"text":["date: 2020-06-06","date: 2020-06-06","date: 2020-06-08","date: 2020-06-09","date: 2020-06-11","date: 2020-06-11","date: 2020-06-11","date: 2020-06-11","date: 2020-06-13","date: 2020-06-13","date: 2020-06-13","date: 2020-06-13","date: 2020-06-17","date: 2020-06-17","date: 2020-06-17","date: 2020-06-17","date: 2020-06-17","date: 2020-06-18","date: 2020-06-18","date: 2020-06-18","date: 2020-06-18","date: 2020-06-19","date: 2020-06-19","date: 2020-06-19","date: 2020-06-19","date: 2020-06-20","date: 2020-06-20","date: 2020-06-20","date: 2020-06-20","date: 2020-06-20","date: 2020-06-20","date: 2020-06-20","date: 2020-06-21","date: 2020-06-21","date: 2020-06-21","date: 2020-06-21","date: 2020-06-21","date: 2020-06-21","date: 2020-06-21","date: 2020-06-21","date: 2020-06-22","date: 2020-06-22","date: 2020-06-22","date: 2020-06-22","date: 2020-06-22","date: 2020-06-22","date: 2020-06-23","date: 2020-06-23","date: 2020-06-23","date: 2020-06-23","date: 2020-06-23","date: 2020-06-24","date: 2020-06-24","date: 2020-06-25","date: 2020-06-25","date: 2020-06-26","date: 2020-06-26","date: 2020-06-27","date: 2020-06-27","date: 2020-06-27","date: 2020-06-27","date: 2020-06-28","date: 2020-06-28","date: 2020-06-28","date: 2020-06-29","date: 2020-06-29","date: 2020-06-29","date: 2020-06-29","date: 2020-06-29","date: 2020-06-29","date: 2020-06-30","date: 2020-06-30","date: 2020-07-01","date: 2020-07-02","date: 2020-07-02","date: 2020-07-02","date: 2020-07-02","date: 2020-07-03","date: 2020-07-03","date: 2020-07-03","date: 2020-07-03","date: 2020-07-04","date: 2020-07-04","date: 2020-07-04","date: 2020-07-06","date: 2020-07-06","date: 2020-07-06","date: 2020-07-06","date: 2020-07-06","date: 2020-07-06","date: 2020-07-07","date: 2020-07-07","date: 2020-07-07","date: 2020-07-07","date: 2020-07-07","date: 2020-07-07","date: 2020-07-08","date: 2020-07-08","date: 2020-07-08","date: 2020-07-08","date: 2020-07-08","date: 2020-07-08","date: 2020-07-08","date: 2020-07-08","date: 2020-07-09","date: 2020-07-09","date: 2020-07-09","date: 2020-07-09","date: 2020-07-09","date: 2020-07-10","date: 2020-07-10","date: 2020-07-11","date: 2020-07-11","date: 2020-07-11","date: 2020-07-11","date: 2020-07-11","date: 2020-07-11","date: 2020-07-11","date: 2020-07-12","date: 2020-07-12","date: 2020-07-12","date: 2020-07-12","date: 2020-07-13","date: 2020-07-13","date: 2020-07-13","date: 2020-07-13","date: 2020-07-13","date: 2020-07-13","date: 2020-07-13","date: 2020-07-13","date: 2020-07-14","date: 2020-07-14","date: 2020-07-14","date: 2020-07-14","date: 2020-07-14","date: 2020-07-15","date: 2020-07-15","date: 2020-07-15","date: 2020-07-15","date: 2020-07-16","date: 2020-07-16","date: 2020-07-16","date: 2020-07-17","date: 2020-07-17","date: 2020-07-17","date: 2020-07-17","date: 2020-07-17","date: 2020-07-18","date: 2020-07-18","date: 2020-07-18","date: 2020-07-18","date: 2020-07-18","date: 2020-07-18","date: 2020-07-19","date: 2020-07-19","date: 2020-07-19","date: 2020-07-19","date: 2020-07-19","date: 2020-07-20","date: 2020-07-20","date: 2020-07-20","date: 2020-07-20","date: 2020-07-20","date: 2020-07-20","date: 2020-07-20","date: 2020-07-20","date: 2020-07-20","date: 2020-07-20","date: 2020-07-20","date: 2020-07-20","date: 2020-07-21","date: 2020-07-21","date: 2020-07-21","date: 2020-07-21","date: 2020-07-21","date: 2020-07-21","date: 2020-07-21","date: 2020-07-22","date: 2020-07-22","date: 2020-07-22","date: 2020-07-22","date: 2020-07-23","date: 2020-07-23","date: 2020-07-23","date: 2020-07-23","date: 2020-07-23","date: 2020-07-24","date: 2020-07-24","date: 2020-07-24","date: 2020-07-24","date: 2020-07-24","date: 2020-07-24","date: 2020-07-24","date: 2020-07-24","date: 2020-07-24","date: 2020-07-24","date: 2020-07-24","date: 2020-07-24","date: 2020-07-24","date: 2020-07-24","date: 2020-07-25","date: 2020-07-25","date: 2020-07-25","date: 2020-07-25","date: 2020-07-26","date: 2020-07-26","date: 2020-07-27","date: 2020-07-27","date: 2020-07-27","date: 2020-07-27","date: 2020-07-27","date: 2020-07-27","date: 2020-07-27","date: 2020-07-27","date: 2020-07-27","date: 2020-07-27","date: 2020-07-27","date: 2020-07-27","date: 2020-07-27","date: 2020-07-28","date: 2020-07-28","date: 2020-07-28","date: 2020-07-28","date: 2020-07-28","date: 2020-07-28","date: 2020-07-28","date: 2020-07-28","date: 2020-07-29","date: 2020-07-29","date: 2020-07-29","date: 2020-07-29","date: 2020-07-29","date: 2020-07-29","date: 2020-07-29","date: 2020-07-29","date: 2020-07-29","date: 2020-07-29","date: 2020-07-30","date: 2020-07-30","date: 2020-07-30","date: 2020-07-30","date: 2020-07-30","date: 2020-07-30","date: 2020-07-30","date: 2020-07-31","date: 2020-07-31","date: 2020-07-31","date: 2020-07-31","date: 2020-07-31","date: 2020-07-31","date: 2020-07-31","date: 2020-07-31","date: 2020-07-31","date: 2020-07-31","date: 2020-07-31","date: 2020-08-01","date: 2020-08-01","date: 2020-08-01","date: 2020-08-01","date: 2020-08-01","date: 2020-08-01","date: 2020-08-01","date: 2020-08-01","date: 2020-08-01","date: 2020-08-01","date: 2020-08-01","date: 2020-08-01","date: 2020-08-02","date: 2020-08-02","date: 2020-08-02","date: 2020-08-02","date: 2020-08-02","date: 2020-08-02","date: 2020-08-02","date: 2020-08-03","date: 2020-08-03","date: 2020-08-03","date: 2020-08-03","date: 2020-08-03","date: 2020-08-03","date: 2020-08-04","date: 2020-08-04","date: 2020-08-04","date: 2020-08-04","date: 2020-08-04","date: 2020-08-04","date: 2020-08-04","date: 2020-08-04","date: 2020-08-04","date: 2020-08-04","date: 2020-08-04","date: 2020-08-04","date: 2020-08-04","date: 2020-08-04","date: 2020-08-04","date: 2020-08-04","date: 2020-08-05","date: 2020-08-05","date: 2020-08-05","date: 2020-08-05","date: 2020-08-05","date: 2020-08-05","date: 2020-08-05","date: 2020-08-05","date: 2020-08-05","date: 2020-08-06","date: 2020-08-06","date: 2020-08-06","date: 2020-08-06","date: 2020-08-06","date: 2020-08-06","date: 2020-08-06","date: 2020-08-06","date: 2020-08-06","date: 2020-08-06","date: 2020-08-07","date: 2020-08-07","date: 2020-08-07","date: 2020-08-07","date: 2020-08-07","date: 2020-08-07","date: 2020-08-07","date: 2020-08-07","date: 2020-08-07","date: 2020-08-07","date: 2020-08-07","date: 2020-08-08","date: 2020-08-08","date: 2020-08-08","date: 2020-08-08","date: 2020-08-08","date: 2020-08-08","date: 2020-08-08","date: 2020-08-08","date: 2020-08-08","date: 2020-08-08","date: 2020-08-09","date: 2020-08-09","date: 2020-08-09","date: 2020-08-09","date: 2020-08-09","date: 2020-08-09","date: 2020-08-09","date: 2020-08-09","date: 2020-08-09","date: 2020-08-10","date: 2020-08-10","date: 2020-08-10","date: 2020-08-10","date: 2020-08-10","date: 2020-08-10","date: 2020-08-10","date: 2020-08-11","date: 2020-08-11","date: 2020-08-11","date: 2020-08-11","date: 2020-08-11","date: 2020-08-11","date: 2020-08-11","date: 2020-08-11","date: 2020-08-11","date: 2020-08-11","date: 2020-08-11","date: 2020-08-11","date: 2020-08-11","date: 2020-08-11","date: 2020-08-11","date: 2020-08-11","date: 2020-08-12","date: 2020-08-13","date: 2020-08-13","date: 2020-08-13","date: 2020-08-13","date: 2020-08-13","date: 2020-08-13","date: 2020-08-13","date: 2020-08-13","date: 2020-08-13","date: 2020-08-13","date: 2020-08-13","date: 2020-08-13","date: 2020-08-13","date: 2020-08-13","date: 2020-08-13","date: 2020-08-13","date: 2020-08-14","date: 2020-08-14","date: 2020-08-14","date: 2020-08-14","date: 2020-08-14","date: 2020-08-14","date: 2020-08-14","date: 2020-08-14","date: 2020-08-14","date: 2020-08-14","date: 2020-08-15","date: 2020-08-15","date: 2020-08-15","date: 2020-08-15","date: 2020-08-15","date: 2020-08-15","date: 2020-08-15","date: 2020-08-16","date: 2020-08-16","date: 2020-08-16","date: 2020-08-16","date: 2020-08-16","date: 2020-08-16","date: 2020-08-16","date: 2020-08-16","date: 2020-08-16","date: 2020-08-16","date: 2020-08-16","date: 2020-08-17","date: 2020-08-17","date: 2020-08-17","date: 2020-08-17","date: 2020-08-17","date: 2020-08-17","date: 2020-08-17","date: 2020-08-17","date: 2020-08-17","date: 2020-08-17","date: 2020-08-17","date: 2020-08-17","date: 2020-08-18","date: 2020-08-18","date: 2020-08-18","date: 2020-08-18","date: 2020-08-18","date: 2020-08-18","date: 2020-08-18","date: 2020-08-18","date: 2020-08-18","date: 2020-08-18","date: 2020-08-18","date: 2020-08-18","date: 2020-08-18","date: 2020-08-18","date: 2020-08-18","date: 2020-08-18","date: 2020-08-19","date: 2020-08-19","date: 2020-08-19","date: 2020-08-19","date: 2020-08-19","date: 2020-08-19","date: 2020-08-19","date: 2020-08-19","date: 2020-08-19","date: 2020-08-19","date: 2020-08-19","date: 2020-08-20","date: 2020-08-20","date: 2020-08-20","date: 2020-08-20","date: 2020-08-20","date: 2020-08-20","date: 2020-08-20","date: 2020-08-20","date: 2020-08-20","date: 2020-08-20","date: 2020-08-20","date: 2020-08-20","date: 2020-08-20","date: 2020-08-20","date: 2020-08-20","date: 2020-08-20","date: 2020-08-20","date: 2020-08-21","date: 2020-08-21","date: 2020-08-21","date: 2020-08-21","date: 2020-08-21","date: 2020-08-21","date: 2020-08-21","date: 2020-08-21","date: 2020-08-21","date: 2020-08-21","date: 2020-08-21","date: 2020-08-21","date: 2020-08-21","date: 2020-08-23","date: 2020-08-23","date: 2020-08-23","date: 2020-08-23","date: 2020-08-23","date: 2020-08-23","date: 2020-08-23","date: 2020-08-23","date: 2020-08-23","date: 2020-08-23","date: 2020-08-23","date: 2020-08-24","date: 2020-08-24","date: 2020-08-24","date: 2020-08-24","date: 2020-08-25","date: 2020-08-25","date: 2020-08-25","date: 2020-08-25","date: 2020-08-25","date: 2020-08-25","date: 2020-08-25","date: 2020-08-25","date: 2020-08-25","date: 2020-08-25","date: 2020-08-25","date: 2020-08-25","date: 2020-08-25","date: 2020-08-26","date: 2020-08-26","date: 2020-08-26","date: 2020-08-26","date: 2020-08-26","date: 2020-08-26","date: 2020-08-26","date: 2020-08-26","date: 2020-08-26","date: 2020-08-26","date: 2020-08-27","date: 2020-08-28","date: 2020-08-28","date: 2020-08-28","date: 2020-08-29","date: 2020-08-29","date: 2020-08-29","date: 2020-08-29","date: 2020-08-29","date: 2020-08-29","date: 2020-08-29","date: 2020-08-29","date: 2020-08-29","date: 2020-08-29","date: 2020-08-29","date: 2020-08-29","date: 2020-08-29","date: 2020-08-29","date: 2020-08-30","date: 2020-08-30","date: 2020-08-30","date: 2020-08-30","date: 2020-08-30","date: 2020-08-30","date: 2020-08-30","date: 2020-08-30","date: 2020-08-30","date: 2020-08-30","date: 2020-09-01","date: 2020-09-01","date: 2020-09-01","date: 2020-09-01","date: 2020-09-01","date: 2020-09-01","date: 2020-09-01","date: 2020-09-01","date: 2020-09-01","date: 2020-09-01","date: 2020-09-01","date: 2020-09-01","date: 2020-09-01","date: 2020-09-01","date: 2020-09-02","date: 2020-09-02","date: 2020-09-02","date: 2020-09-02","date: 2020-09-03","date: 2020-09-03","date: 2020-09-03","date: 2020-09-03","date: 2020-09-04","date: 2020-09-04","date: 2020-09-04","date: 2020-09-04","date: 2020-09-04","date: 2020-09-04","date: 2020-09-04","date: 2020-09-04","date: 2020-09-04","date: 2020-09-04","date: 2020-09-05","date: 2020-09-05","date: 2020-09-06","date: 2020-09-06","date: 2020-09-06","date: 2020-09-06","date: 2020-09-06","date: 2020-09-07","date: 2020-09-08","date: 2020-09-09","date: 2020-09-09","date: 2020-09-09","date: 2020-09-10","date: 2020-09-10","date: 2020-09-10","date: 2020-09-10","date: 2020-09-10","date: 2020-09-10","date: 2020-09-10","date: 2020-09-12","date: 2020-09-15","date: 2020-09-15","date: 2020-09-16","date: 2020-09-16","date: 2020-09-16","date: 2020-09-17","date: 2020-09-17","date: 2020-09-17","date: 2020-09-17","date: 2020-09-18","date: 2020-09-18","date: 2020-09-18","date: 2020-09-18","date: 2020-09-18","date: 2020-09-18","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-19","date: 2020-09-20","date: 2020-09-21","date: 2020-09-21","date: 2020-09-25","date: 2020-09-25","date: 2020-09-25","date: 2020-09-25","date: 2020-09-25","date: 2020-09-25","date: 2020-09-25","date: 2020-09-25","date: 2020-09-25","date: 2020-09-25","date: 2020-09-25","date: 2020-09-25","date: 2020-09-25","date: 2020-09-26","date: 2020-09-26","date: 2020-09-27","date: 2020-09-27","date: 2020-09-27","date: 2020-09-27","date: 2020-09-27","date: 2020-09-27","date: 2020-09-27","date: 2020-09-30","date: 2020-09-30","date: 2020-09-30","date: 2020-09-30","date: 2020-09-30","date: 2020-09-30","date: 2020-09-30","date: 2020-10-01","date: 2020-10-02","date: 2020-10-02","date: 2020-10-02","date: 2020-10-03","date: 2020-10-03","date: 2020-10-03","date: 2020-10-04","date: 2020-10-07","date: 2020-10-07","date: 2020-10-07","date: 2020-10-07","date: 2020-10-07","date: 2020-10-07","date: 2020-10-07","date: 2020-10-08","date: 2020-10-08","date: 2020-10-10","date: 2020-10-10","date: 2020-10-10","date: 2020-10-10","date: 2020-10-11","date: 2020-10-11","date: 2020-10-11","date: 2020-10-11","date: 2020-10-11","date: 2020-10-11","date: 2020-10-11","date: 2020-10-11","date: 2020-10-11","date: 2020-10-11","date: 2020-10-11","date: 2020-10-11","date: 2020-10-12","date: 2020-10-12","date: 2020-10-12","date: 2020-10-12","date: 2020-10-12","date: 2020-10-12","date: 2020-10-12","date: 2020-10-12","date: 2020-10-12","date: 2020-10-12","date: 2020-10-12","date: 2020-10-12","date: 2020-10-12","date: 2020-10-12","date: 2020-10-12","date: 2020-10-14","date: 2020-10-14","date: 2020-10-14","date: 2020-10-14","date: 2020-10-14","date: 2020-10-14","date: 2020-10-14","date: 2020-10-14","date: 2020-10-14","date: 2020-10-14","date: 2020-10-14","date: 2020-10-14","date: 2020-10-14","date: 2020-10-15","date: 2020-10-15","date: 2020-10-15","date: 2020-10-15","date: 2020-10-15","date: 2020-10-15","date: 2020-10-15","date: 2020-10-16","date: 2020-10-16","date: 2020-10-17","date: 2020-10-17","date: 2020-10-17","date: 2020-10-17","date: 2020-10-17","date: 2020-10-17","date: 2020-10-17","date: 2020-10-18","date: 2020-10-18","date: 2020-10-18","date: 2020-10-18","date: 2020-10-18","date: 2020-10-18","date: 2020-10-18","date: 2020-10-18","date: 2020-10-18","date: 2020-10-18","date: 2020-10-18","date: 2020-10-18"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(255,0,0,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(255,0,0,1)"}},"hoveron":"points","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[18419,18420.6962025316,18422.3924050633,18424.0886075949,18425.7848101266,18427.4810126582,18429.1772151899,18430.8734177215,18432.5696202532,18434.2658227848,18435.9620253165,18437.6582278481,18439.3544303797,18441.0506329114,18442.746835443,18444.4430379747,18446.1392405063,18447.835443038,18449.5316455696,18451.2278481013,18452.9240506329,18454.6202531646,18456.3164556962,18458.0126582278,18459.7088607595,18461.4050632911,18463.1012658228,18464.7974683544,18466.4936708861,18468.1898734177,18469.8860759494,18471.582278481,18473.2784810127,18474.9746835443,18476.6708860759,18478.3670886076,18480.0632911392,18481.7594936709,18483.4556962025,18485.1518987342,18486.8481012658,18488.5443037975,18490.2405063291,18491.9367088608,18493.6329113924,18495.3291139241,18497.0253164557,18498.7215189873,18500.417721519,18502.1139240506,18503.8101265823,18505.5063291139,18507.2025316456,18508.8987341772,18510.5949367089,18512.2911392405,18513.9873417722,18515.6835443038,18517.3797468354,18519.0759493671,18520.7721518987,18522.4683544304,18524.164556962,18525.8607594937,18527.5569620253,18529.253164557,18530.9493670886,18532.6455696203,18534.3417721519,18536.0379746835,18537.7341772152,18539.4303797468,18541.1265822785,18542.8227848101,18544.5189873418,18546.2151898734,18547.9113924051,18549.6075949367,18551.3037974684,18553],"y":[35.6789705739767,38.9118883519908,42.4402385682101,46.2651283557094,50.3876648475547,54.8089551768386,59.5301064766275,64.5522258799965,69.8764205200205,75.5037975297745,81.4354640423205,87.6725271907589,94.2160941081522,101.067271927576,108.227167782104,115.696888804812,123.477542128775,131.57023488705,139.976074212747,148.688861031265,157.251322972898,165.527207964168,173.707399749665,181.98278207398,190.544238681685,199.582653317407,209.28890972572,219.853891651214,231.468482838479,242.942256494023,251.301389066809,258.156539062811,265.393662846133,274.898716780898,288.55765723123,308.147199091695,331.852307808362,358.024600217602,386.20812723702,415.946939784052,446.785088776186,478.657239216906,515.831972461157,557.310439159342,600.153504061574,641.4220319177,678.178525767902,715.203020695609,757.418507423691,802.751600967417,849.128916341956,894.47706856278,936.722672645058,973.792343604061,1003.61269645506,1024.2339055958,1039.48444454279,1052.16319271985,1062.44873556446,1070.51965851416,1076.55454700645,1080.73198647886,1083.23056236892,1084.22886011413,1083.90546515203,1082.43896292014,1080.00793885597,1076.70244180939,1071.75314105222,1064.96113802754,1056.35226429837,1045.95235142769,1033.78723097854,1019.88273451393,1004.26469359686,986.958939790369,967.991304657497,947.38761976118,925.173716664472,901.375426930387],"text":["date: 18419.00","date: 18420.70","date: 18422.39","date: 18424.09","date: 18425.78","date: 18427.48","date: 18429.18","date: 18430.87","date: 18432.57","date: 18434.27","date: 18435.96","date: 18437.66","date: 18439.35","date: 18441.05","date: 18442.75","date: 18444.44","date: 18446.14","date: 18447.84","date: 18449.53","date: 18451.23","date: 18452.92","date: 18454.62","date: 18456.32","date: 18458.01","date: 18459.71","date: 18461.41","date: 18463.10","date: 18464.80","date: 18466.49","date: 18468.19","date: 18469.89","date: 18471.58","date: 18473.28","date: 18474.97","date: 18476.67","date: 18478.37","date: 18480.06","date: 18481.76","date: 18483.46","date: 18485.15","date: 18486.85","date: 18488.54","date: 18490.24","date: 18491.94","date: 18493.63","date: 18495.33","date: 18497.03","date: 18498.72","date: 18500.42","date: 18502.11","date: 18503.81","date: 18505.51","date: 18507.20","date: 18508.90","date: 18510.59","date: 18512.29","date: 18513.99","date: 18515.68","date: 18517.38","date: 18519.08","date: 18520.77","date: 18522.47","date: 18524.16","date: 18525.86","date: 18527.56","date: 18529.25","date: 18530.95","date: 18532.65","date: 18534.34","date: 18536.04","date: 18537.73","date: 18539.43","date: 18541.13","date: 18542.82","date: 18544.52","date: 18546.22","date: 18547.91","date: 18549.61","date: 18551.30","date: 18553.00"],"type":"scatter","mode":"lines","name":"fitted values","line":{"width":3.77952755905512,"color":"rgba(160,32,240,1)","dash":"solid"},"hoveron":"points","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":25.5707762557078,"l":34.337899543379},"paper_bgcolor":"rgba(191,213,227,1)","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Relationship of weight of vegetables in grams(g) with date","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[18412.3,18559.7],"tickmode":"array","ticktext":["Jun","Jul","Aug","Sep","Oct"],"tickvals":[18414,18444,18475,18506,18536],"categoryorder":"array","categoryarray":["Jun","Jul","Aug","Sep","Oct"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":true,"linecolor":"rgba(0,0,139,1)","linewidth":1.99252801992528,"showgrid":false,"gridcolor":null,"gridwidth":0,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-365.4,7717.4],"tickmode":"array","ticktext":["0","2000","4000","6000"],"tickvals":[0,2000,4000,6000],"categoryorder":"array","categoryarray":["0","2000","4000","6000"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":true,"linecolor":"rgba(0,0,139,1)","linewidth":1.99252801992528,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"61ca442ab26c7":{"x":{},"y":{},"type":"scatter"},"61ca44ace632c":{"x":{},"y":{}}},"cur_data":"61ca442ab26c7","visdat":{"61ca442ab26c7":["function (y) ","x"],"61ca44ace632c":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->


```r
lettuce_variety <- garden_harvest %>%
  filter(vegetable %in% c("lettuce")) %>%
  arrange(desc(variety)) %>%
  group_by(variety) %>%
  summarize(n = n()) %>%
  ggplot(aes(x = n, y = fct_reorder(variety, n))) +
  geom_col(fill = "blue", color = "red") +
  labs(title = "Harvesting Varieties of Lettuce",
       x = "Count",
        y = "Variety")
ggplotly(lettuce_variety,
         tooltip = c("text", "x"))
```

<!--html_preserve--><div id="htmlwidget-6407b199c9ece5bee48b" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-6407b199c9ece5bee48b">{"x":{"data":[{"orientation":"v","width":[27,29,1,3,9],"base":[3.55,4.55,0.55,1.55,2.55],"x":[13.5,14.5,0.5,1.5,4.5],"y":[0.9,0.9,0.9,0.9,0.9],"text":["n: 27","n: 29","n:  1","n:  3","n:  9"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(0,0,255,1)","line":{"width":1.88976377952756,"color":"rgba(255,0,0,1)"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":40.1826484018265,"l":148.310502283105},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Harvesting Varieties of Lettuce","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-1.45,30.45],"tickmode":"array","ticktext":["0","10","20","30"],"tickvals":[0,10,20,30],"categoryorder":"array","categoryarray":["0","10","20","30"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"Count","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,5.6],"tickmode":"array","ticktext":["mustard greens","reseed","Tatsoi","Farmer's Market Blend","Lettuce Mixture"],"tickvals":[1,2,3,4,5],"categoryorder":"array","categoryarray":["mustard greens","reseed","Tatsoi","Farmer's Market Blend","Lettuce Mixture"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"Variety","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"61ca46df471c9":{"x":{},"y":{},"type":"bar"}},"cur_data":"61ca46df471c9","visdat":{"61ca46df471c9":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

 2. Use animation to tell an interesting story with the `small_trains` dataset that contains data from the SNCF (National Society of French Railways). These are Tidy Tuesday data! Read more about it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2019/2019-02-26).
 

```r
train_delay <- small_trains %>%
  group_by(service) %>%
  filter(!is.na(service)) %>%
  filter(departure_station %in% c("ZURICH", "PARIS LYON"))
  delay1 <- train_delay %>% 
  ggplot(aes(x = avg_delay_all_departing, 
             y = service)) +
  geom_density_ridges() +
  transition_states(year) +
  labs(title = "Departing Delay by German and French Train Services",
       x = "Mean Delay in Minutes",
       y = "Train Service Type",
       subtitle = "Moving to {next_state}") 
  delay1
```


```r
anim_save("traindelay.gif", delay1)
```
 

```r
knitr::include_graphics("traindelay.gif")
```

 
## Garden data

  3. In this exercise, you will create a stacked area plot that reveals itself over time (see the `geom_area()` examples [here](https://ggplot2.tidyverse.org/reference/position_stack.html)). You will look at cumulative harvest of tomato varieties over time. You should do the following:
  * From the `garden_harvest` data, filter the data to the tomatoes and find the *daily* harvest in pounds for each variety.  
  * Then, for each variety, find the cumulative harvest in pounds.  
  * Use the data you just made to create a static cumulative harvest area plot, with the areas filled with different colors for each vegetable and arranged (HINT: `fct_reorder()`) from most to least harvested (most on the bottom).  
  * Add animation to reveal the plot over date. 

I have started the code for you below. The `complete()` function creates a row for all unique `date`/`variety` combinations. If a variety is not harvested on one of the harvest dates in the dataset, it is filled with a value of 0.


```r
garden_harvest %>%
  filter(vegetable == "tomatoes") %>%
  complete(variety, date = seq.Date(min(date), max(date), by="day")) %>%
  select(-c(vegetable, units)) %>%
  mutate(weight = replace_na(weight, 0)) %>%
  group_by(variety, date) %>%
  summarize(daily_harvest_lb = sum(weight)*0.00220462) %>%
  mutate(cumsum_daily_harvest_lb = cumsum(daily_harvest_lb)) %>%
  select(-daily_harvest_lb) %>%
  ggplot() +
    geom_area(aes(x = date, y = cumsum_daily_harvest_lb, fill = variety), position = position_stack()) +
    transition_reveal(date) +
    labs(title = "Cumulative Harvest of Varieties of Tomatoes through Time",
       x = "Date",
       y = "Cumulative Daily Harvest",
       subtitle = "Moving to {frame_along}") 
```

![](Rayyan_05_exercises_files/figure-html/unnamed-chunk-6-1.gif)<!-- -->


```r
anim_save("harvest_area.gif")
```


```r
knitr::include_graphics("harvest_area.gif")
```


## Maps, animation, and movement!

  4. Map my `mallorca_bike_day7` bike ride using animation! 
  Requirements:
  * Plot on a map using `ggmap`.  
  * Show "current" location with a red point. 
  * Show path up until the current point.  
  * Color the path according to elevation.  
  * Show the time in the subtitle.  
  * CHALLENGE: use the `ggimage` package and `geom_image` to add a bike image instead of a red point. You can use [this](https://raw.githubusercontent.com/llendway/animation_and_interactivity/master/bike.png) image. See [here](https://goodekat.github.io/presentations/2019-isugg-gganimate-spooky/slides.html#35) for an example. 
  * Add something of your own! And comment on if you prefer this to the static map and why or why not.
  
  

  

```r
mallorca_map <- get_stamenmap(
    bbox = c(left = 2.28, bottom = 39.41, right = 3.03, top = 39.8), 
    maptype = "terrain",
    zoom = 11
)
ggmap(mallorca_map) +
  geom_point(data = mallorca_bike_day7, 
             aes(x = lon, y = lat),
             color = "red", size = .5) +
  geom_path(data = mallorca_bike_day7, 
             aes(x = lon, y = lat, color = ele),
             size = .5) +
  labs(title = "Bike Trail of Mallorca",
       subtitle = "Time: {frame_along}") +
  transition_reveal(time) +
  scale_color_viridis_c(option = "magma") +
  theme_map() +
  theme(legend.background = element_blank())
```

![](Rayyan_05_exercises_files/figure-html/unnamed-chunk-9-1.gif)<!-- -->
  

```r
anim_save("bikpath.gif")
```


![](bikpath.gif)<!-- -->


The animated plot does a better job at establishing behavior over time. I think this is more efficient than a static plot due to the fact that we can use one plot to show the whole behavior. However, if we were writing a paper an animated plot would be difficult to include. 

5. In this exercise, you get to meet my sister, Heather! She is a proud Mac grad, currently works as a Data Scientist at 3M where she uses R everyday, and for a few years (while still holding a full-time job) she was a pro triathlete. You are going to map one of her races. The data from each discipline of the Ironman 70.3 Pan Am championships, Panama is in a separate file - `panama_swim`, `panama_bike`, and `panama_run`. Create a similar map to the one you created with my cycling data. You will need to make some small changes: 1. combine the files (HINT: `bind_rows()`, 2. make the leading dot a different color depending on the event (for an extra challenge, make it a different image using `geom_image()!), 3. CHALLENGE (optional): color by speed, which you will need to compute on your own from the data. You can read Heather's race report [here](https://heatherlendway.com/2016/02/10/ironman-70-3-pan-american-championships-panama-race-report/). She is also in the Macalester Athletics [Hall of Fame](https://athletics.macalester.edu/honors/hall-of-fame/heather-lendway/184) and still has records at the pool. 


```r
trail <- panama_swim %>%
  bind_rows(list(panama_run, panama_bike)) 
  
panama_map <- get_stamenmap(
  bbox = c(left = -79.56, bottom = 8.88, right = -79.41, top = 9.001),
  maptype = "terrain",
  zoom = 13
)
ggmap(panama_map) +
  geom_point(data = trail, 
             aes(x = lon, y = lat, color = event, shape = event),
             size = 2) +
  geom_path(data = trail,
            aes(x = lon, y = lat, color = event),
            alpha = 0.8, size = 0.5) +
  labs(title = "Map of Race",
       subtitle = "Time: {frame_along}") +
  scale_color_viridis_d(option = "magma") +
  theme_map() +
  theme(legend.background = element_blank()) +
  transition_reveal(time)
```
  

```r
anim_save("race.gif")
```

![](race.gif)<!-- -->

## COVID-19 data

  6. In this exercise, you are going to replicate many of the features in [this](https://aatishb.com/covidtrends/?region=US) visualization by Aitish Bhatia but include all US states. Requirements:
 * Create a new variable that computes the number of new cases in the past week (HINT: use the `lag()` function you've used in a previous set of exercises). Replace missing values with 0's using `replace_na()`.  
  * Filter the data to omit rows where the cumulative case counts are less than 20.  
  * Create a static plot with cumulative cases on the x-axis and new cases in the past 7 days on the x-axis. Connect the points for each state over time. HINTS: use `geom_path()` and add a `group` aesthetic.  Put the x and y axis on the log scale and make the tick labels look nice - `scales::comma` is one option. This plot will look pretty ugly as is.
  * Animate the plot to reveal the pattern by date. Display the date as the subtitle. Add a leading point to each state's line (`geom_point()`) and add the state name as a label (`geom_text()` - you should look at the `check_overlap` argument).  
  * Use the `animate()` function to have 200 frames in your animation and make it 30 seconds long. 
  * Comment on what you observe.
  

```r
covid19 %>%
  group_by(state) %>%
  mutate(lag7 = lag(cases, 7, order_by = date)) %>%
  replace_na(list(lag7 = 0)) %>%
  mutate(new_cases_past_week = cases - lag7) %>%
  filter(cases >= 20) %>%
  
  ggplot(aes(x = cases, y = new_cases_past_week, group = state)) +
  geom_point(color = "light blue") +
  geom_path(color = "red") +
  geom_text(aes(label = state), check_overlap = TRUE) +
  scale_x_log10(labels = scales::comma) +
  scale_y_log10(labels = scales::comma) +
  labs(
    title = "Corona Cases Trend in the US",
    x = "Total Cases",
    y = "New Cases",
    subtitle = "Date: {frame_along}"
  ) +
  theme(legend.position = "none") +
  transition_reveal(date) -> covid19trajectory_gganim
animate(covid19trajectory_gganim,
        nframes = 200,
        duration = 30)
```
  
  

```r
anim_save("covid.gif")
```

  
![](covid.gif)<!-- -->
  
  
We can see that almost all states have increased in confirmed cases through time, with certain fluctuations across the time span. The graph is a little unclear due to all states being included.

  7. In this exercise you will animate a map of the US, showing how cumulative COVID-19 cases per 10,000 residents has changed over time. This is similar to exercises 11 & 12 from the previous exercises, with the added animation! So, in the end, you should have something like the static map you made there, but animated over all the days. Put date in the subtitle. Comment on what you see. The code below gives the population estimates for each state. Because there are so many dates, you are going to only do the animation for all Fridays. So, use `wday()` to create a day of week variable and filter to all the Fridays. HINT: use `group = date` in `aes()`.


```r
census_pop_est_2018 <- read_csv("https://www.dropbox.com/s/6txwv3b4ng7pepe/us_census_2018_state_pop_est.csv?dl=1") %>% 
  separate(state, into = c("dot","state"), extra = "merge") %>% 
  select(-dot) %>% 
  mutate(state = str_to_lower(state))
```



```r
covid19_population <-
  covid19 %>% 
  mutate(state = str_to_lower(state)) %>%
  left_join(census_pop_est_2018,
            by = "state") %>% 
  group_by(state, est_pop_2018, date) %>%
  summarize(cumulative_cases = max(cases)) %>%
  mutate(cases_per_10000 = (cumulative_cases/est_pop_2018)*10000)
states_map <- map_data("state")
covid_map <- covid19_population %>% 
  mutate(state = str_to_lower(state), weekday = wday(date, label=TRUE)) %>%
  filter(weekday == "Fri") %>%
  ggplot() +
  geom_map(map = states_map,
           aes(map_id = state, fill = cases_per_10000, group = date)) +
  expand_limits(x = states_map$long, y = states_map$lat) + 
  labs(title = "Cumulative COVID-19 cases per 10,000 people in US") +
  theme(legend.background = element_blank()) + 
  theme_map() +
  scale_fill_viridis_c() +
  transition_states(date, transition_length = 0) +
  labs(subtitle = "Moving to {next_state}")
animate(covid_map, duration = 30)
```


```r
anim_save("covidmap.gif", covid_map)
```
  

![](covidmap.gif)<!-- -->
 
 
 This corresponds to the graph shown previously with cases cumulatively increasing across all states in the US. The change in colors then show that the cases per 100,000 people keep increasing across states through time which covers the entire map at the end.

## Your first `shiny` app (for next week!)

NOT DUE THIS WEEK! If any of you want to work ahead, this will be on next week's exercises.

  8. This app will also use the COVID data. Make sure you load that data and all the libraries you need in the `app.R` file you create. Below, you will post a link to the app that you publish on shinyapps.io. You will create an app to compare states' cumulative number of COVID cases over time. The x-axis will be number of days since 20+ cases and the y-axis will be cumulative cases on the log scale (`scale_y_log10()`). We use number of days since 20+ cases on the x-axis so we can make better comparisons of the curve trajectories. You will have an input box where the user can choose which states to compare (`selectInput()`) and have a submit button to click once the user has chosen all states they're interested in comparing. The graph should display a different line for each state, with labels either on the graph or in a legend. Color can be used if needed. 
  
## GitHub link

  9. Below, provide a link to your GitHub page with this set of Weekly Exercises. Specifically, if the name of the file is 05_exercises.Rmd, provide a link to the 05_exercises.md file, which is the one that will be most readable on GitHub. If that file isn't very readable, then provide a link to your main GitHub page.

[My github link](https://github.com/rmobarak/Data-Science_Materials)

**DID YOU REMEMBER TO UNCOMMENT THE OPTIONS AT THE TOP?**
