# Mike Merritt - Projects Created from (mostly) Public Data

These simple projects show methodology and tool usage without exposing any private data.

## 1. Computer Vision using Python 

Computer vision can be harnessed to analyze images and videos, especially under controlled conditions.   

[CLICK HERE](https://michaeljmerritt.github.io/Portfolio/Images/Foam2.mp4) to see an example of how testing with visual performance metrics can be automated.  In this case it was necessary to measure the amount of foam growth after a pour of nitrogenated coffee.  The test recorded dozens of videos per hour and each needed to be analyzed and the foam heights measured as well as the time it took for the growth to stop.  I created a script to open a specific network folder, collect the videos within it, analyze each video and output a data file with the measurements tabulated.  In this case the engineer can review the data file and review individual videos if something doesn't look right.

## 2. Animating Cyclic Data

When presenting cyclic data it can help to overlay each cycle's graph on top of each other and watch for changes.  It is easy to visualize slow drift in signals in this manner, and this type of inspection will also make seeing outliers or otherwise odd behavior in data.  

![Image of Cyclic Data](https://michaeljmerritt.github.io/Portfolio/Images/CyclicSignsls.gif)


## 3. Dashboard Methodology using Python and Power BI

For this analysis I've pulled overall mortality data in the USA from 3 different sources in the Center for Disease Control (CDC) database. First, a large set of historical data from 2014 - 2018 that is stable. Second, a dataset from the end of 2020 that had provisional, semi-stable mortality data for 2019. Finally the most recent dataset from 2022 that has provisional mortality data for 2020, 2021 and 2022 year to date.

These datasets overlap, so I used Python and Pandas to concatenate them into a single data table and then remove all duplicate data before bringing the cleaned data set into PowerBI.  From this point I can plot the mortality for each year on the same chart. The report will allow the data to be sliced by year and US state, and I also include the breakout bar chart of causes of death for any slice.  Since any death can be from multiple causes these values do not sum to 100%.  

When I do this I can see that the number of deaths in the US in 2020, 2021 and 2022 were considerably higher than those in prior years and that the excess follows a pattern not unlike the different waves of Covid-19 that were reported during those times.  

![Image of Mortality](https://michaeljmerritt.github.io/Portfolio/Images/Mort0a.jpg)

Individually choosing the year 2019 provides baseline mortality for an average year in the time before the Covid pandemic:

![Image of Mortality 2019](https://michaeljmerritt.github.io/Portfolio/Images/Mort1a.jpg)

Choosing 2020 shows a significant increase in overall mortality in the first year of the Covid pandemic:

![Image of Mortality 2020](https://michaeljmerritt.github.io/Portfolio/Images/Mort2a.jpg)

Choosing 2021 shows that overall mortality in the US in the second year of the pandemic has exceeded that of the first year.  It's likely that the data for 2021 is for the most part stable now, but it appears that deaths in January of 2022 are rising faster than in prior years.  I can also see from the sharp change in direction of the 2022 curve that the January 2022 numbers have not yet stabilized, so we need to wait for more data to see if this trend will continue into February.    

![Image of Mortality 2021](https://michaeljmerritt.github.io/Portfolio/Images/Mort3a.jpg)

It is also interesting to note from the cause of death section that the percentage of deaths of natural causes remains more or less constant despite the increase in mortality due to Covid.  In 2020 and 2021 when the Covid related causes of death are introduced the heart and neoplasm/cancer related causes of death are reduced.  This suggests that Covid is proving more deadly to those with heart and cancer realted issues than healthy people.

For the next analysis I use only a single dataset from the CDC that has detailed information on Covid cases in the US categorized by age, race and sex.  Each case also has information regarding the severity of the case including hospitalization and death. 

In the charts I've charted the reported cases of Covid in the left panel, the Covid-related deaths in the top-center panel and the death rate by age group in the bottom-center panel.  I added a number of slicers to the right to further study different sections of the population.

Its interesting to note that while looking at the total population the death rate increases non-linearly with age.  In fact the death rate for people under 40 years old is extremely small.

![Image of Cases](https://michaeljmerritt.github.io/Portfolio/Images/Cases0a.jpg)

Clicking the 80+ age group highlights that while the total number of Covid cases is relatively small the death rate from these cases in very large.

![Image of Cases 80](https://michaeljmerritt.github.io/Portfolio/Images/Cases1a.jpg)

Clicking the 30-39 age group shows that while folks in this age group contracted six times as many Covid cases as 80+ year old people there were only one twentieth as many deaths.

![Image of Cases 30](https://michaeljmerritt.github.io/Portfolio/Images/Cases2a.jpg)

Often animation can provide additional perspective to a visualization.  [CLICK HERE](https://michaeljmerritt.github.io/Portfolio/Images/CovidMarch2022.mp4) to view an animation that shows the rise and fall of recorded Covid19 infections by state over the past year and a half.  From this short clip you can follow how the hot spots shift over time and when the various waves of Covid rise and recede.

## 4. Collecting, Combining and Cleaning Fragmented Data

Large amounts of data needs to be collected before many analyses can be made.  This can be public data downloaded or scraped from websites or it can be queried from private databases.  Often this data is not immediately in a useable form and must be processed in order to make sure that any missing data is accounted for and the data types are consistent.  In this case I've pulled nearly 600,000 lines of daily stock price and volume data of nearly 7,000 different stocks from Yahoo! Finance.  Each stock was pulled from a separate web page and then needed to be combined into a single data file.

![Image of DataFrame](https://michaeljmerritt.github.io/Portfolio/Images/bigdfa.jpg)

Once the data is in a useable form and well understood it can be used to find indicators that are shown to signal changes.  This can be accomplished with simple algorithms for data that is well understood or with machine learning techniques if there are many seemingly unrelated features that affect the decision.

In this case the indicator we want is a simple but effective indicator called on-balance volume that is a function of the stock's price and its trade volume.  It is calculated first instantaneously and then as a one week moving average and a two week moving average.  A crossing of the two averages is flagged as an important event, and we'll capture the volume data as an indicator of relative signal strength.  The data necessary for these indicators will be added as new columns to the data file that was just created.

![Image of DataFrame](https://michaeljmerritt.github.io/Portfolio/Images/tempdfb.jpg)

Once the calculations are complete it is a good idea to test the algorithm to make sure it is able to find the desired indicators.  Since the crossings are of importance and not the actual value the OBV data is scaled down to fit on the same chart as the stock price line in black for easier viewing.  In this case not every event that is flagged by the algorithm is important, however any general trajectory change in the stock price seems to be close to an indicator.  After a number of iterations I am happy with this set of curves and how they can indicate potential changes in the stock price.  

![Image of Chart](https://michaeljmerritt.github.io/Portfolio/Images/test.jpg)

Finally it is time to inspect all of the data and identify indicators for all of the stock tickers.  For this analysis I will upload the entire data set as a table into a new Microsoft PowerBI project.  I have also added a table that has summary information about each stock that will be used to subdivide the various stocks into categories of similar industries and sectors.  I created a third table within Power BI that duplicated the summary table and used it to create a new column that calculates how close each stock's latest closing price is to its recent high values, and another column that calculates the ratio of the price's two week moving average vs its four week moving average. 

![Image of Tables](https://michaeljmerritt.github.io/Portfolio/Images/PBIDesigna.jpg)

I have linked these tables by the TICKER columns and created a dashboard that allows me to quickly review business category performance and then drill down through the individual stocks.  In this case I can select any sector or industry and get a chart of the sector's performance as well as a table of all stocks that make up that slice of data.  I can then sort that table by any of the columns of data and finally select individual stocks to see the performance chart for that stock.

![Image of Dashboard](https://michaeljmerritt.github.io/Portfolio/Images/PBIReport.jpg)

This is helpful for looking at information that is already well understood, however when the data is not well understood a very simple way to separate meaningful data points from the pack is to plot two measurements in a scatter plot.  In the dashboard below I have done just that, by plotting the two calculated fields I created against each other:  how close the stock's last closing price is to its most recent high price and the stock's momentum as determined by its moving average ratio.  

![Image of Scatter Dashboard](https://michaeljmerritt.github.io/Portfolio/Images/PBIReport2a.jpg)

So a point high on the Y axis is stock with its price near a recent maximum and a point high along the X axis shows a price rising faster in the past two weeks than the past four.  So in this case points in the upper right quadrant of the chart will be of most interest to find new stocks that are showing strong momentum.

## 5. Getting Detailed

Digging deep into data often uncovers details that aren't noticeable when looking at summaries, take the 2020 Presidential Election summary for instance.  Showing a map with the states colored according to who won that state is an effective image for showing how each candidate received their electoral votes, but does it provide any insight as to how the populace voted?

Parsing the voting results data by county and then shading each county along a continuous color scale allows us to inspect the voting results in detail without cluttering the chart.  Many states show large areas of muted colors that indicate close races with darker regions indicating strongholds for each candidate.  The chart is still simple and easy to read but shows much more information.

![Image of Map](https://michaeljmerritt.github.io/Portfolio/Images/2020ElectionSmall.gif)

## 6. Animation

[CLICK HERE](https://michaeljmerritt.github.io/Portfolio/Images/infectionstudy.mp4) to view an animation that attempts to demonstrate how an infection spreads though a population under different conditions.  The left pane is the baseline with a 20% infection rate and a contagious period of 150 steps.  The infection rate is the probability a contagious (red) sample will infect a passing healthy (blue) sample.  The next pane shows how the same population’s situation changes when the infection rate drops to 10% while keeping the contagious period the same.  The third pane brings the infection rate back up to 20% but reduces the contagious period by half down to 75 steps.  Finally the last pane reduces the infection rate to 10% and keeping the contagious period at 75 steps.

This model shows that for this particular set of circumstances the best way to substantially affect the spread of red dots is to both reduce the infection rate and the contagious period.  More what-if types of analyses could be run if one of these proves difficult.  For instance if the contagious period is something that cannot be affected then another analysis could be run with an even lower infection rate.  The results of these analyses could inform decisions on what style mask is required to reduce transmission or even if quarantine is necessary to stop the spread of red dots.
