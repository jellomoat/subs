# Redd All About It
What the top subreddits say about us

link to story: [on subreddits!](https://jellomoat.github.io/subs/)

## Description


## Overall Findings


## Data Collection Process


### Scraping, many times over


## Data Analysis Process


### Getting Word Frequencies


### Extracting Topics and Classifying Subreddits
This is still a major work in progress.  I attempted to do this several ways:

I first tried extracting topics from subreddit names and descriptions using [sklearn](https://investigate.ai/text-analysis/introduction-to-topic-modeling/#Topic-modeling) and [TF-IDF](https://investigate.ai/text-analysis/a-simple-explanation-of-tf-idf/#Part-Two:-Inverse-document-frequency) but had dubious results.

So I scripted as much as I could using counting methods and determined categories based on most common words (using word frequencies described [here](#getting-word-frequencies)).  I then aggregated regex patterns for each category, wrote to csv any records that did not match any specified category, then integer-tagged each record in that csv with integers corresponding to categories.  This tagged csv was subsequently loaded and re-parsed to add to the accumulated category regex patterns.

Initially I was looking up subreddits that I could not tag based off of name or description alone.  But that was really time-consuming since there were hundreds of the original 1K dataset to sift through.  I did as much as I easily could and assigned value 12 (the "other" category) to the rest, with the intent to come back and re-tag/re-classify the remaining others either the semi-painful regex way or using some sort of more advanced method for text analysis.

### Creating Plots and Tables

Bubble Charts:
I used Flourish to create two bubble charts plotting the <a href="https://public.flourish.studio/visualisation/14399872/">1000</a> and <a href="https://public.flourish.studio/visualisation/14399773/">100</a> most popular subreddits as of July 2023.  These are explorables best viewed on desktop (hover over bubbles for more detail!)

Table:
I also used Datawrapper to create a table of this data.  I wanted to provide a means for easily reviewing the data itself.  I enjoyed putting in random search terms and discovering related up-and-coming communities.  This project led me to <a href="https://www.reddit.com/r/DiWHY/">r/DiWHY</a>, <a href="https://www.reddit.com/r/NatureIsFuckingLit/">r/NatureIsFuckingLit</a>, and <a href="https://www.reddit.com/r/technicallythetruth">r/technicallythetruth</a>.

Horizontal Bar Chart:
Mapping word frequencies!!!  In Flourish!?!

## Page Formatting
I adapted the style of the [Reddit subreddits main page](https://www.reddit.com/subreddits) for this story.  I first started with Reddit's HTML/CSS and pared that down to just preserve its color, orientation, and font particulars (background, shading, sizes, element positioning, etc.).  Most of the page's text content was replaced, and many of the elements there were removed.  I wanted my site to both appear distinctly different from Reddit while still evoking some sense of Reddit.

## Tools and Techniques Used
- Web scraping using [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)! 
- Lots of [pandas](https://pandas.pydata.org/)
- Progress monitoring using [tqdm](https://pypi.org/project/tqdm/#ipython-jupyter-integration)
- Text analysis, counting word frequencies, lemmatizing tokens, and grouping records using [nltk](https://www.nltk.org/), [sklearn](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html), [collections](https://docs.python.org/3/library/collections.html#collections.Counter), and [regex](https://regex101.com/)  Heavily referenced [investigate.ai](https://investigate.ai/#textanalysis)
- Styling adapted from [Reddit](https://www.reddit.com/subreddits)
- Plotting data using [Datawrapper](https://www.datawrapper.de/), [Flourish](https://flourish.studio/), and [Jupyter](https://jupyter.org/)

## Things I Considered or Planned On Doing But Did Not Get To Yet:
- Extracting topics and classifying records using non-regex methods
- Getting most recent post per subreddit
- Visualizing similarities/relationships between subreddits using word embeddings or network graphs
- Just making things look nicer?
