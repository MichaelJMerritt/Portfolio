# Mike Merritt - Projects Created from (mostly) Public Data

These simple projects show methodology and tool usage without exposing any private data.

## 1. Collecting and Combining Data from Many Sources

There are many tools publicly available to analyze an individual stock's performance but I wanted to be able to compare many stock histories and rank them by either (1) how likely they are to continue their current course or (2) how likely they are to change their course in the near future.  I wanted a PowerBI report that I can use to select only companies that meet certain conditions and then drill down into those companies to decide if they are good investments for me.  These conditions include whether a stock price is trending up or down, whether that price trend is accelerating or decelerating and whether there are recent large spikes in trading volume.

<p align="center">  
    <img src="https://michaeljmerritt.github.io/Portfolio/Images/Stocks_Top.jpg">
</p>

In order to do that I need to collect historical price and trading volume data for many stocks and develop measures to be able to compare their recent performance.

I found some summary information listing basic information about all of the publicly traded companies in US markets.  So I wrote script to organize the company data into market sectors and then periodically refresh the high level data into a local spreadsheet.  From that data I chose the largest 100 companies from each market sector to keep a database of price and trading volume history, over 2,000 companies.  I wrote another script to update a local database with recent price and trading volume data.  The scrip will look to see if that stock is new to the database and if it is new then it will collect the past 8 years of data, otherwise it will simply update the local database with new data.



Process :
1. Collect summary data on all publicly traded companies from public websites, nearly 7,000 companies.
2. Write script to periodically refresh the data into a local spreadsheet.
3. Organize the company data into market sectors and industries.
4. Choose the largest 100 companies from each market sector to keep a database of price and trading volume history, over 2,000 companies.
5. Write script to periodically refresh each individual stock's historical data locally.
   - Ensure that if a new stock enters the top 100 that the code will collect the last 4 years of data, otherwise simply add any missing data that has become available since the last refresh.
6. Decide on various analyses to perform in order to gain insight on how the stock is performing:
   - A 25 day moving average and a 50 day moving average on stock price to get insight on how the price is trending ( up or down ) and how the trend is moving ( accelerating or decelerating ).
   - Identify all points at which the 2 moving averages cross to understand when the price change enters a meaningful direction change.
   - Use the trading volume and the price histories to calculate a measure of public sentiment called On Balance Volume (OBV) which simply adds the trading volume during price increases and subtracts the trading volume during times of price decreases.
   - Calculate the slopes of each of the price and volume regression lines over the past 25 days to create a measure of the magnitude of how a price is changing.
7. Combine all individual stock history data into a single data file.  Current data file approaching 3 million lines.
8. For each stock symbol in the data file:
   - Add columns for the various moving averages and the OBV. Perform the regression analyses to get the slope of the trends.
   - Based on these slopes identify if each line is Rising Fast, Rising, Neutral, Falling or Falling Fast.
   - Add these measures to the original spreadsheet containing all of the stock summaries.
  
At this point I verify that each measure is working as intended while still using Python, image below.  In the stock price pane ( top ) I plot each moving average crossing with either a red or green dot, depending on if the crossing is the short term rising above the long term or falling below.  Then I plot the price trend line in grey over its signal in black.  In the trading volume pane ( bottom ) I plot the OBV measurement in black and the trend line in red.  

<p align="center">  
    <img src="https://michaeljmerritt.github.io/Portfolio/Images/Stocks_Definition.jpg">
</p>

Now I was ready to create a PowerBI report that links to the summary spreadhseet and the stock history data file, relating the data files to each other by the stock symbol.  reate visuals on a single page that allow me to only show stocks that are performing in a particular manner, and then



<p align="center">  
    <img src="https://michaeljmerritt.github.io/Portfolio/Images/Stocks_Individual.jpg">
</p>

## 2. Simple Data Drill Down in Python

I wanted to make it easier to set my fantasy football lineups each week, so I created a simple tool to compare any NFL team's offensive output vs any other team's defensive performance.

<p align="center">  
    <img src="https://michaeljmerritt.github.io/Portfolio/Images/FBOverview.jpg">
</p>

This tool draws from a database of all NFL stats that I collect from the internet each week.  I can select any 2 teams andcompare any position.  For instance in the screnshot above I compare the Chiefs running back rushing offense against the 49ers running back rushing defense.  The upper stacked bar chart shows me the Chief's total rushing output for all positions every week in grey, and then stacks each individual running back's output in each week.  Finally each week's opponent's average rushing defensive performance is plotted with a heavy dot.  This one chart can give me a high level view of how the selected team has performed against each opponent's average and then each individual player's contribution.

The bottom bar chart show's the opponent's performance against each running back they've played.  The colored line is that running back's performace against the selected team, and the heavy dot is that running back's average performance.  From this chart it looks like the 49ers have had success holding running backs that average more than 60 yeards fper game below their average, however they hadn't faced a strong running back in the final 3 weeks of the regular season.

Changing what statistics to look at is as simple as choosing new values from the drop-down boxes and clicking EXECUTE.  Selecting tight end recieving data reveals the charts below.  The 49ers had good success early in the season holding tight ends below their average but seemed to struggle later.  Meanwhile the Chiefs rely heavily on their tight ends in the assing game and routinely collect more yards than the opponents average.  Its interesting to note that trend has fallen off as the season ended.

<p align="center">  
    <img src="https://michaeljmerritt.github.io/Portfolio/Images/FBOverview2.jpg">
</p>

## 3. Dashboard Methodology using Python and Power BI

For this analysis I've pulled overall mortality data in the USA from 3 different sources in the Center for Disease Control (CDC) database. First, a large set of historical data from 2014 - 2018 that is stable. Second, a dataset from the end of 2020 that had provisional, semi-stable mortality data for 2019. Finally the most recent dataset from 2023 that has provisional mortality data for 2020, 2021, 2022 and 2023 year to date.

These datasets overlap, so I used Python and Pandas to concatenate them into a single data table and then remove all duplicate data before bringing the cleaned data set into PowerBI.  From this point I can plot the mortality for each year on the same chart. The report will allow the data to be sliced by year and US state and I also include the breakout bar chart of causes of death for any slice.  Since any death can be from multiple causes these values do not sum to 100%.  

When I do this I can see that the number of deaths in the US in 2020, 2021 and 2022 were considerably higher than those in prior years and that the excess follows a pattern not unlike the different waves of Covid-19 that were reported during those times.  

<p align="center">  
    <img src="https://michaeljmerritt.github.io/Portfolio/Images/Mort0a.jpg">
</p>

Individually choosing the year 2019 provides baseline mortality for an average year in the time before the Covid pandemic:

<p align="center">  
    <img src="https://michaeljmerritt.github.io/Portfolio/Images/Mort1a.jpg">
</p>

Choosing 2020 shows a significant increase in overall mortality in the first year of the Covid pandemic:

<p align="center">  
    <img src="https://michaeljmerritt.github.io/Portfolio/Images/Mort2a.jpg">
</p>

Choosing 2021 shows that overall mortality in the US in the second year of the pandemic had exceeded that of the first year:

<p align="center">  
    <img src="https://michaeljmerritt.github.io/Portfolio/Images/Mort3a.jpg">
</p>

Its clear from the charts that the data from 2023 has only stabilized for the first half of the year, so we will use the MONTHS slicer in the upper right corner of the visual to only display the 2023 data from January through August:

<p align="center">  
    <img src="https://michaeljmerritt.github.io/Portfolio/Images/Mort4a.jpg">
</p>

From this we can see that the data first half of 2023 shows mortality rates approaching pre-pandemic levels.  There is an inflection point at day 224 of 2023 where the mortality rate begins to drop significantly, which tells me that its very likely that the data past that date has not yet stabilized and there is still alot of data that hasn't been verified and added to the database yet.

It is also interesting to note from the cause of death section that the percentage of deaths of natural causes remains more or less constant despite the increase in mortality due to Covid.  In 2020 and 2021 when the Covid related causes of death are introduced the heart and neoplasm/cancer related causes of death are reduced.  This suggests that Covid is proving more deadly to those with heart and cancer related issues than otherwise healthy people.

For the next analysis I use only a single dataset from the CDC that has detailed information on Covid cases in the US categorized by age, race and sex.  Each case also has information regarding the severity of the case including hospitalization and death. 

In the charts I've charted the reported cases of Covid in the left panel, the Covid-related deaths in the top-center panel and the death rate by age group in the bottom-center panel.  I added a number of slicers to the right to further study different sections of the population.

Its interesting to note that while looking at the total population the death rate increases non-linearly with age.  In fact the death rate for people under 40 years old is extremely small.

<p align="center">  
    <img src="https://michaeljmerritt.github.io/Portfolio/Images/Cases0a.jpg">
</p>

Clicking the 80+ age group highlights that while the total number of Covid cases is relatively small the death rate from these cases in very large.

<p align="center">  
    <img src="https://michaeljmerritt.github.io/Portfolio/Images/Cases1a.jpg">
</p>

Clicking the 30-39 age group shows that while folks in this age group contracted more than four times as many Covid cases as 80+ year old people there were fewer than one twentieth as many deaths.

<p align="center">  
    <img src="https://michaeljmerritt.github.io/Portfolio/Images/Cases2a.jpg">
</p>

## 3. Computer Vision using Python 

Computer vision can be harnessed to analyze images and videos and collect data without human intervention, especially under controlled conditions.   

[CLICK HERE](https://michaeljmerritt.github.io/Portfolio/Images/Foam2.mp4) to see an example of how testing with visual performance metrics can be automated.  In this case it was necessary to measure the amount of foam growth after a pour of nitrogenated coffee.  The test recorded dozens of videos per hour and each needed to be analyzed and the foam heights measured as well as the time it took for the growth to stop.  I created a script to open a specific network folder, collect the videos within it, analyze each video and output a data file with the measurements tabulated.  In this case the engineer can review the data file and review individual videos if something doesn't look right.

## 4. Animating Cyclic Data

When presenting cyclic data it can help to overlay each cycle's graph on top of each other and watch for changes.  It is easy to visualize slow drift in signals in this manner, and this type of inspection will also make seeing outliers or otherwise odd behavior in data.  

<p align="center">  
    <img src="https://michaeljmerritt.github.io/Portfolio/Images/CyclicSignsls.gif">
</p>

## 5. Getting Detailed

Digging deep into data often uncovers details that aren't noticeable when looking at summaries, take the 2020 Presidential Election summary for instance.  Showing a map with the states colored according to who won that state is an effective image for showing how each candidate received their electoral votes, but does it provide any insight as to how the populace voted?

Parsing the voting results data by county and then shading each county along a continuous color scale allows us to inspect the voting results in detail without cluttering the chart.  Many states show large areas of muted colors that indicate close races with darker regions indicating strongholds for each candidate.  The chart is still simple and easy to read but shows much more information.

<p align="center">  
    <img src="https://michaeljmerritt.github.io/Portfolio/Images/2020ElectionSmall.gif">
</p>

## 6. Animation

[CLICK HERE](https://michaeljmerritt.github.io/Portfolio/Images/infectionstudy.mp4) to view an animation that attempts to demonstrate how an infection spreads though a population under different conditions.  The left pane is the baseline with a 20% infection rate and a contagious period of 150 steps.  The infection rate is the probability a contagious (red) sample will infect a passing healthy (blue) sample.  The next pane shows how the same population’s situation changes when the infection rate drops to 10% while keeping the contagious period the same.  The third pane brings the infection rate back up to 20% but reduces the contagious period by half down to 75 steps.  Finally the last pane reduces the infection rate to 10% and keeping the contagious period at 75 steps.

This model shows that for this particular set of circumstances the best way to substantially affect the spread of red dots is to both reduce the infection rate and the contagious period.  More what-if types of analyses could be run if one of these proves difficult.  For instance if the contagious period is something that cannot be affected then another analysis could be run with an even lower infection rate.  The results of these analyses could inform decisions on what style mask is required to reduce transmission or even if quarantine is necessary to stop the spread of red dots.
