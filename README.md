# Mike Merritt - Projects Created from Public Data

These simple projects show methodology and tool usage without exposing any private data.

## 1. Dashboard Methodology

First, large amounts of data needs to be collected.  This can be public data downloaded or scraped from websites or it can be queried from private databases.  Often this data is not immediately in a useable form and must be processed in order to make sure that any missing data is accounted for and the data types are consistent.

![Image of DataFrame](https://michaeljmerritt.github.io/Portfolio/Images/bigdfa.jpg)

Once the data is in a useable form and well understood it can be used to find indicators that are shown to signal changes might be on the way.  This can be accomplished with simple algorythems on data that is well understood or with machine learnging techniques if there are many features that affect the decision.

In this case the indicator we want is a simple but effective indicator called on-balance volume that is a function of the stock's price and its trade volume.  It is calculated instantaneously, as a one week moving average and as a two week moving average.  A crossing of the two averages is flagged as an important event.  Since the crossings are of importance and not the actual value the OBV data is scaled down to fit on the ssame chart as the stock price line in black.

![Image of DataFrame](https://michaeljmerritt.github.io/Portfolio/Images/tempdfa.jpg)

Once the calculations are complete it is a good idea to test the algorithem to make sure it is finding what is necessary.  In this case not every event that is flagged by the algorithem is important, however any general trajectory change in the stock price seems to be close to an indicator.  After a number of iterations I am happy with this set of curves and how they can indicate potential changes in the stock price.  

![Image of DataFrame](https://michaeljmerritt.github.io/Portfolio/Images/test.jpg)

Finally its time to release the code to inspect all of the data find indicators for all of the stock tickers.  The resulting data can be sorted in any number of ways, for instance below we find the stocks who's last signal was positive but ws many months ago, expecting to find stcoks who'se prices have been on long upward trajectories.  Success, although a few of them appear to be nearing a downturn signal:

![Image of DataFrame](https://michaeljmerritt.github.io/Portfolio/Images/final.jpg)

## 2. Getting Detailed

Digging deep into data often uncovers details that aren't noticeable when looking at summaries, take the 2020 Presidential Election summary for instance.  Showing a map with the states colored according to who won that state is an effective image for showing how each candidate received their electoral votes, but does it provide any insight as to how the populace voted?

Parsing the voting results data by county and then shading each county along a continuous color scale allows us to inspect the voting results in detail without cluttering the chart.  Many states show large areas of muted colors showing close races while others show darker colors definite indicating strongholds for each candidate.  The chart is still simple and easy to read but shows much more information.

![Image of DataFrame](https://michaeljmerritt.github.io/Portfolio/Images/election.gif)

## 3. Staying Grounded

Its not always best to stay in the details, it is often necessary to take a step back and take a macro view of the data.  

![Image of DataFrame](https://michaeljmerritt.github.io/Portfolio/Images/mortalityhistorya.jpg)

The convergence indicators on the chart were simply calculated by looking at each individual date from the mortality data and watching for how long the value for that day took to stabilize.  From the chart below we can see that for most dates the mortality counts approach their final value between weeks five and six:

![Image of DataFrame](https://michaeljmerritt.github.io/Portfolio/Images/converge.jpg)

## 4. Animation

Often showing patterns in data that changes with time can be made more effective with animation.  There are other times when showing a concept is easier with animation.

Github doen't support in-web viewing of animation at the moment and many animation files are too large to upload in GIF form.  I'd be happy to show you more when we speak!

![Image of DataFrame](https://michaeljmerritt.github.io/Portfolio/Images/animationscreenshot.jpg)

![Image of DataFrame](https://michaeljmerritt.github.io/Portfolio/Images/animationscreenshot2.jpg)
