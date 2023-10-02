# Mike Merritt - Projects Created from (mostly) Public Data

These simple projects show methodology and tool usage without exposing any private data.

## 1. Combining and Summarizing Data from Many Sources






## 2. Dashboard Methodology using Python and Power BI

For this analysis I've pulled overall mortality data in the USA from 3 different sources in the Center for Disease Control (CDC) database. First, a large set of historical data from 2014 - 2018 that is stable. Second, a dataset from the end of 2020 that had provisional, semi-stable mortality data for 2019. Finally the most recent dataset from 2023 that has provisional mortality data for 2020, 2021, 2022 and 2023 year to date.

These datasets overlap, so I used Python and Pandas to concatenate them into a single data table and then remove all duplicate data before bringing the cleaned data set into PowerBI.  From this point I can plot the mortality for each year on the same chart. The report will allow the data to be sliced by year and US state and I also include the breakout bar chart of causes of death for any slice.  Since any death can be from multiple causes these values do not sum to 100%.  

When I do this I can see that the number of deaths in the US in 2020, 2021 and 2022 were considerably higher than those in prior years and that the excess follows a pattern not unlike the different waves of Covid-19 that were reported during those times.  

![Image of Mortality](https://michaeljmerritt.github.io/Portfolio/Images/Mort0a.jpg)

Individually choosing the year 2019 provides baseline mortality for an average year in the time before the Covid pandemic:

![Image of Mortality 2019](https://michaeljmerritt.github.io/Portfolio/Images/Mort1a.jpg)

Choosing 2020 shows a significant increase in overall mortality in the first year of the Covid pandemic:

![Image of Mortality 2020](https://michaeljmerritt.github.io/Portfolio/Images/Mort2a.jpg)

Choosing 2021 shows that overall mortality in the US in the second year of the pandemic had exceeded that of the first year:

![Image of Mortality 2021](https://michaeljmerritt.github.io/Portfolio/Images/Mort3a.jpg)

Its clear from the charts that the data from 2023 has only stabilized for the first half of the year, so we will use the MONTHS slicer in the upper right corner of the visual to only display the 2023 data from January through August:

![Image of Mortality Early 2022](https://michaeljmerritt.github.io/Portfolio/Images/Mort4a.jpg)

From this we can see that the data first half of 2023 shows mortality rates approaching pre-pandemic levels.  There is an inflection point at day 113 of 2023 where the mortality rate begins to drop significantly, which tells me that its very likely that the data past that date has not yet stabilized and there is still alot of data that hasn't been verified and added to the database yet.

It is also interesting to note from the cause of death section that the percentage of deaths of natural causes remains more or less constant despite the increase in mortality due to Covid.  In 2020 and 2021 when the Covid related causes of death are introduced the heart and neoplasm/cancer related causes of death are reduced.  This suggests that Covid is proving more deadly to those with heart and cancer realted issues than healthy people.

For the next analysis I use only a single dataset from the CDC that has detailed information on Covid cases in the US categorized by age, race and sex.  Each case also has information regarding the severity of the case including hospitalization and death. 

In the charts I've charted the reported cases of Covid in the left panel, the Covid-related deaths in the top-center panel and the death rate by age group in the bottom-center panel.  I added a number of slicers to the right to further study different sections of the population.

Its interesting to note that while looking at the total population the death rate increases non-linearly with age.  In fact the death rate for people under 40 years old is extremely small.

![Image of Cases](https://michaeljmerritt.github.io/Portfolio/Images/Cases0a.jpg)

Clicking the 80+ age group highlights that while the total number of Covid cases is relatively small the death rate from these cases in very large.

![Image of Cases 80](https://michaeljmerritt.github.io/Portfolio/Images/Cases1a.jpg)

Clicking the 30-39 age group shows that while folks in this age group contracted more than four times as many Covid cases as 80+ year old people there were fewer than one twentieth as many deaths.

![Image of Cases 30](https://michaeljmerritt.github.io/Portfolio/Images/Cases2a.jpg)

Often animation can provide additional perspective to a visualization.  [CLICK HERE](https://michaeljmerritt.github.io/Portfolio/Images/CovidMarch2022.mp4) to view an animation that shows the rise and fall of recorded Covid19 infections by state over the past year and a half.  From this short clip you can follow how the hot spots shift over time and when the various waves of Covid rise and recede.

## 3. Computer Vision using Python 

Computer vision can be harnessed to analyze images and videos, especially under controlled conditions.   

[CLICK HERE](https://michaeljmerritt.github.io/Portfolio/Images/Foam2.mp4) to see an example of how testing with visual performance metrics can be automated.  In this case it was necessary to measure the amount of foam growth after a pour of nitrogenated coffee.  The test recorded dozens of videos per hour and each needed to be analyzed and the foam heights measured as well as the time it took for the growth to stop.  I created a script to open a specific network folder, collect the videos within it, analyze each video and output a data file with the measurements tabulated.  In this case the engineer can review the data file and review individual videos if something doesn't look right.

## 4. Animating Cyclic Data

When presenting cyclic data it can help to overlay each cycle's graph on top of each other and watch for changes.  It is easy to visualize slow drift in signals in this manner, and this type of inspection will also make seeing outliers or otherwise odd behavior in data.  

![Image of Cyclic Data](https://michaeljmerritt.github.io/Portfolio/Images/CyclicSignsls.gif)

## 5. Getting Detailed

Digging deep into data often uncovers details that aren't noticeable when looking at summaries, take the 2020 Presidential Election summary for instance.  Showing a map with the states colored according to who won that state is an effective image for showing how each candidate received their electoral votes, but does it provide any insight as to how the populace voted?

Parsing the voting results data by county and then shading each county along a continuous color scale allows us to inspect the voting results in detail without cluttering the chart.  Many states show large areas of muted colors that indicate close races with darker regions indicating strongholds for each candidate.  The chart is still simple and easy to read but shows much more information.

![Image of Map](https://michaeljmerritt.github.io/Portfolio/Images/2020ElectionSmall.gif)

## 6. Animation

[CLICK HERE](https://michaeljmerritt.github.io/Portfolio/Images/infectionstudy.mp4) to view an animation that attempts to demonstrate how an infection spreads though a population under different conditions.  The left pane is the baseline with a 20% infection rate and a contagious period of 150 steps.  The infection rate is the probability a contagious (red) sample will infect a passing healthy (blue) sample.  The next pane shows how the same population’s situation changes when the infection rate drops to 10% while keeping the contagious period the same.  The third pane brings the infection rate back up to 20% but reduces the contagious period by half down to 75 steps.  Finally the last pane reduces the infection rate to 10% and keeping the contagious period at 75 steps.

This model shows that for this particular set of circumstances the best way to substantially affect the spread of red dots is to both reduce the infection rate and the contagious period.  More what-if types of analyses could be run if one of these proves difficult.  For instance if the contagious period is something that cannot be affected then another analysis could be run with an even lower infection rate.  The results of these analyses could inform decisions on what style mask is required to reduce transmission or even if quarantine is necessary to stop the spread of red dots.
