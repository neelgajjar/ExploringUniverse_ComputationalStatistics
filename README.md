# Universe DataAnalysis
## Calculate the Age of the Universe

### Image

![galaxies](https://user-images.githubusercontent.com/8587332/35609972-7bfc709a-0614-11e8-85fc-6799263db805.png)

*According to this data, the age of the universe is 13.773 billion years old. This is -0.187% off from the [accepted value](https://en.wikipedia.org/wiki/Age_of_the_universe) of 13.799 billion years old.*

## Step 1: Find and Filter the Data

Data was taken from [HyperLeda](http://leda.univ-lyon1.fr/leda/fullsql.html), using the command: `SELECT objname, mod0, vgsr WHERE mod0 IS NOT NULL`, basically taking all the distance vs. velocity data they had available (4240 galaxies). After doing a quick conversion from Distance Modulus to Megaparsecs (1 Megaparsec = 3.086x10^19 km), here's what the plot looks like:

![All Data](https://raw.githubusercontent.com/zonination/galaxies/master/other/Rplot01.png)

Hmm. This doesn't look too good. There's a huge cluster towards the origin, and a lot of sparse data and outliers on the extremes. This could really screw with our final value. Let's cut the extreme data out and just focus inside the red box I highlighted:

![Less Extreme Data](https://raw.githubusercontent.com/zonination/galaxies/master/other/Rplot02.png)

This looks much better. The cluster is a lot more even, and there are fewer (if any) outliers. Our total galaxy count is now 3908, still 92% of our data. The data range is `x<=250, y<=15000`. This is the set we'll use for our calculation on the age of the universe.

## Step 2: Brush up on your Kinematics

Find it odd that the further the galaxies are from you, the faster they're moving away from you? If you have objects moving away from you at a speed proportional to their distance from you, then there must have been some kind of explosion that took place before. Take, for instance, the following diagram, which is simulated using the program in the `other` folder:

![Small Particle Explosion](https://raw.githubusercontent.com/zonination/galaxies/master/other/Rplot03.png)

From this plot, you can intuitively figure two things:

1. The further the particle is away from the center, the faster it's moving away from the center.
2. If you were to go back in time, and tally up the speeds from each particle into the opposite direction of where they're currently moving, you'd see that they would all converge to a single point.

Here's what it looks like when these particles are plotted as speed vs. distance:

![Small Particle Explosion](https://raw.githubusercontent.com/zonination/galaxies/master/other/Rplot04.png)

Both these plots, by the way, would look similar if you chose any point on this plot as the center. 

## Step 3: Do some simple Calculations

As we know from physics, velocity times time equals distance (`d = v*t`). If we convert to a consistent set of units, divide distance (km) over velocity (km/s), we get time (s). A simple regression line works if you switch x and y (set the intercept to 0); the slope will be time in seconds. Convert into years, and, with this data, we get 13.77 billion years. That's pretty close.

## Information

* **Tools:** The data was compiled with R, and graphed in ggplot2.
* **Source:** [HyperLeda](http://leda.univ-lyon1.fr/leda/fullsql.html), using the command: `SELECT objname, mod0, vgsr WHERE mod0 IS NOT NULL`

# Star Classification
## Animated Hertzsprung-Russell Diagram with 119,614 datapoints

### About

Hertzsprung–Russell diagrams made and animated using 119,614 data points in a star catalog.

Stars twinkle for two reasons:

* Aesthetics
* Reduces overploting

## Graphic

![twinkle gif](https://user-images.githubusercontent.com/8587332/35610263-7bba74d2-0615-11e8-925a-0dc096f42c67.jpg)

## Notes:

If you're going to play with this:

* Make sure you have ImageMagick installed
* the last line is optimized to work with unix-like systems (Linux/Mac, basically). If you have Windows, replace it with `DEL star_anim*.png`
* make sure the second line has the correct working directory under `setwd()`.

## Sources:

* The [HYG database](http://www.astronexus.com/hyg)

[More info on H-R Diagrams from Wikipedia](https://en.wikipedia.org/wiki/Hertzsprung%E2%80%93Russell_diagram)

## Tools used:

* ggplot2
* Rstudio

# StartSpots

Inspired by [this thread](https://www.reddit.com/r/dataisbeautiful/comments/3ilzsi/daily_sunspot_number_1900_to_aug_2015_with_11/), I wanted to make the following changes:

* Expand to the full data set.
* Update the data set to most recent number provided.
* Create and provide an automated script in R to crunch new data as it comes in.
* Remove moving average, add aesthetic changes

## Image

![sunspots](https://user-images.githubusercontent.com/8587332/35610355-d1d51fd4-0615-11e8-8932-655ec997a5eb.png)

## Information

* Source: http://www.sidc.be/silso/INFO/sndtotcsv.php
* Tools: R/ggplot2


