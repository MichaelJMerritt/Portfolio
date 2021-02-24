# Mike Merritt - Projects Created from Public Data

These simple projects show methodology and tool usage without exposing any private data.

## 1. Dashboard Methodology using Python and Power BI

Large amounts of data needs to be collected before many analyses can be made.  This can be public data downloaded or scraped from websites or it can be queried from private databases.  Often this data is not immediately in a useable form and must be processed in order to make sure that any missing data is accounted for and the data types are consistent.  In this case we've pulled nearly 600,000 lines of daily stock price and volume data of many different stocks from Yahoo! Finance.

![Image of DataFrame](https://michaeljmerritt.github.io/Portfolio/Images/bigdfa.jpg)

Once the data is in a useable form and well understood it can be used to find indicators that are shown to signal changes.  This can be accomplished with simple algorithms for data that is well understood or with machine learning techniques if there are many seemingly unrelated features that affect the decision.

In this case the indicator we want is a simple but effective indicator called on-balance volume that is a function of the stock's price and its trade volume.  It is calculated first instantaneously and then as a one week moving average and a two week moving average.  A crossing of the two averages is flagged as an important event, and we'll capture the volume data as an indicator of relative signal strength.  

![Image of DataFrame](https://michaeljmerritt.github.io/Portfolio/Images/tempdfb.jpg)

Once the calculations are complete it is a good idea to test the algorithm to make sure it is able to find the desired indicators.  Since the crossings are of importance and not the actual value the OBV data is scaled down to fit on the same chart as the stock price line in black for easier viewing.  In this case not every event that is flagged by the algorithm is important, however any general trajectory change in the stock price seems to be close to an indicator.  After a number of iterations I am happy with this set of curves and how they can indicate potential changes in the stock price.  

![Image of Chart](https://michaeljmerritt.github.io/Portfolio/Images/test.jpg)

Finally it is time to apply the code to inspect all of the data and identify indicators for all of the stock tickers.  The resulting data can be sorted in any number of ways, for instance below we find the stocks whose last signal was positive but was a long time ago.  However in this case I will upload this data to a new Microsoft PowerBI project along with another table that has summary information about each stock in the dataset.  

![Image of Tables](https://michaeljmerritt.github.io/Portfolio/Images/PBIDesign.jpg)

I will link these tables by the TICKER column and create a dashboard that allows me to quickly review any of the business sector or industry high level trends, and then drill down into the individual stocks that make up that sector to review their performance.

![Image of Dashboard](https://michaeljmerritt.github.io/Portfolio/Images/PBIReport.jpg)

This is helpful for looking at information that is already well understood, however when the data is not well understood a very simple way to isolate meaningful data points is to plot 2 measurements in a scatter plot.  In this case, for each stock I calculate how close the stock price is to its recent high values and chart it against the ratio of its two week moving average vs its four week moving average.  

So a point high on the Y axis is nearing a recent maximum and a point high along the X axis shows a price rising faster in the past two weeks than the past four.  So in this case points in the upper right quadrant of the chart will be of most interest to find new stocks that are currently showing strong momentum.

The dashboard below allows me to slice the data by sector, then choose individual data points from the scatter plot to show their recent price history on the line chart.

![Image of Scatter Dashboard](https://michaeljmerritt.github.io/Portfolio/Images/PBIReport2.jpg)

## 2. Cyclic Data

When presenting cyclic data it can help to overlay each cycle's data on top of each other and watch for changes.  It is easy to visualize slow drift in signals in this manner, and this type of inspection will also make seeing outliers or otherwise odd behavior in data.  

![Image of Cyclic Data](https://michaeljmerritt.github.io/Portfolio/Images/CyclicSignsls.gif)

## 3. Getting Detailed

Digging deep into data often uncovers details that aren't noticeable when looking at summaries, take the 2020 Presidential Election summary for instance.  Showing a map with the states colored according to who won that state is an effective image for showing how each candidate received their electoral votes, but does it provide any insight as to how the populace voted?

Parsing the voting results data by county and then shading each county along a continuous color scale allows us to inspect the voting results in detail without cluttering the chart.  Many states show large areas of muted colors that indicate close races with darker regions indicating strongholds for each candidate.  The chart is still simple and easy to read but shows much more information.

![Image of Map](https://michaeljmerritt.github.io/Portfolio/Images/election.gif)

## 4. Staying Grounded

It is not always best to stay confined to the details, it is often necessary to take a step back and take a macro view of the data.  For this example I examine the mortality due to Covid-19 in the United States in 2020.  Different organizations and publications present different tallies with different conditions that make them hard to compare.  A simple way to get a high level look might be to compare the 2020 mortality data against prior years.

When we do this we can see that the number of deaths in the US in 2020 was considerably higher than those in prior years and that the excess follows a pattern not unlike the different waves of Covid-19 that were reported throughout the year.  It is also interesting to note that the number of excess deaths as of mid-December is considerably higher than any of the reported Covid-19 tallies from that timeframe. 

![Image of Chart](https://michaeljmerritt.github.io/Portfolio/Images/mortalityhistorye.jpg)

The convergence indicators that are shown on the chart are calculated by collecting the value for each individual date for each week that the report is released.  This way we can see how that value changes from week to week and calculate how long it takes for the that day's tally to stabilize.  From the chart below we can see that for most dates the mortality counts approach their final value between weeks seven and eight.

An interesting artifact that this chart shows is that during the holidays at the end of December and early January there was a week in which it would appear reporting was put on hold.  The week of very few death reports followed by a significant spike in reported deaths can be seen rippling back throught the data for most of January.

![Image of Convegence](https://michaeljmerritt.github.io/Portfolio/Images/convergee.jpg)

## 5. Animation

Often showing patterns in data that changes with time can be made more effective with animation.  There are other times when showing a concept is easier with animation.

GitHub doesn't support in-web viewing of video at the moment and some animation files are too large to upload in GIF form.  I'd be happy to show you more when we speak!

![Image of Animation Screenshots](https://michaeljmerritt.github.io/Portfolio/Images/animationscreenshot.jpg)

![Another Image of Animation Screenshots](https://michaeljmerritt.github.io/Portfolio/Images/animationscreenshot2.jpg)
