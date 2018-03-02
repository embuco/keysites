# keysites
R code and related materials for sea duck key sites analysis

This repository contains R code used to estimate key site polygons from Atlantic Winter Sea Duck Survey data 2008-2011.  Also included are data from regionally restricted survey work in 2012 and the 2014 Atlantic Marine Assessment Program for Protected Species (AMAPPS) winter survey. AMAPPS uses the same survey design as the early winter sea duck survey, but the lines are extended farther to the east to cover habitat for pelagic seabirds.

Steps in the analysis:

1. Bird observations summed and partitioned to equal length segments along survey transect lines, survey effort by side and segment is also calculated (for code, see *Segmentation* folder).

**Note**: The *planned* survey transects were used to calculate flight length and segment centroid, not the actual flight paths, due to difficulties reconciling left and right seat observer tracks (clock times are not perfectly syncronized). This also makes it easier to determine weights reflecting survey effort (see #2), but an improved analysis would/will use the actual flight tracks.

2. Survey effort is determined for each segment surveyed. This information is used as a weight in the kernel density estimation, since the kernel estimate needs to account for the fact that some segments were surveyed more often than others (in particular, the winter sea duck survey design changed from 2008 to 2009 and does not cover the offshore area in 2008 v. 2009-11 ... see FWS summary report in *Documentation* folder for more details on the winter sea duck surveys).

3. A border corrected, effort weighted kernel density is estimated using all segments with sea ducks present (code allows subsetting to species or species groups). This kernel represents a density function for probability of presence.

4. The kernel is cut to the 99% isopleth to define the overall sea duck winter at-sea range.  Segments outside this kernel are dropped and the accumulation curve for the remaining segments (total individuals plotted against number of segments) is used to calculate the inflection point of "diminishing returns," i.e., the proportion of the area sampled at which sampled area begins to increase more quickly that individuals counted.  This defines the percentage to use to define the "core" sea duck areas.

5. The kernel isolpleth is calculated for the core percentage and the associated polygons identified.

6. Each distinct core area is assessed to determine if it meet "key site" status: (i) Cumulative sea duck density > 10/km^2 and (ii) apparent total birds (no adjustment for detection or mis-counting bias) = cumulative density * polygon area > 20,000.


