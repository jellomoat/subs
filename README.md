# Redd All About It
What the top subreddits say about us

link to story: [on subreddits!](https://jellomoat.github.io/subs/)

## Description

A data story about the most popular subreddits and what they say about us
(More description to come)

## Overall Most Interesting Findings

- There are so many subreddits!  There's at least one subreddit created every minute!
- People often seek advice from complete strangers online.  Out of 1,000 subreddits, over <> sought advice in an "ask"-type community.
- People also are very open to offering advice and opinions freely online.
- There's much love for non-people porn.  Looking for such content?  Try <a href="https://www.reddit.com/r/MapPorn">r/MapPorn</a>, <a href="https://www.reddit.com/r/fightporn">r/fightporn</a>, <a href="https://www.reddit.com/r/shittyfoodporn">r/shittyfoodporn</a>, <a href="https://www.reddit.com/r/DesignPorn">r/DesignPorn</a>, and <a href="https://www.reddit.com/r/mycology">r/mycology</a> (which has "mycoporn").
- Many types of people on Reddit, though geeks and nerds seem the most engaged judging by how many science, learning, tech, anime, and games subreddits are among the most popular.
- Many redditors enjoy freedom of speech.  One example of this is the rise of <a href="https://reddit.com/r/AITAH">r/AITAH</a>, which at times eclipses its much elder sibling <a href="https://www.reddit.com/r/AmItheAsshole/">r/AmItheAsshole</a> (2013) in popularity.  The description for r/AITAH:
> this is a community like r/AmITheAsshole except unlike that subreddit here you can post interpersonal conflicts, anything that's AITA but is not allowed there even posting about Scar from the lion king and trying to convince redditors that he was not the AH. rules: don't berate others and no pornography we have children here

<!-- - Many  dislike Reddit's new pricing policies.  Reddit recently limited access to their API (by charging indie developers a lot of money); many admins and mods are protesting. -->

## Data Collection Process: Scraping, Many Times Over
Scraping, many times over

I used Beautiful Soup to scrape all of [Reddit's popular subreddits pages](https://www.reddit.com/subreddits/popular).  This amounted to 41 pages of roughly 100 records each, nearly 4100 records in total.

I actually initially wanted to scrape all subreddits ever by starting from the newest and working my way back.  I read [a story](https://wegotthiscovered.com/social-media/how-many-subreddits-are-on-reddit) that led me to believe that there were only around 140K subreddits as of last month.  (The article actually stated that there were ~140K _active_ subreddits, something I only realized after scraping over 200K records across 1750 pages.  New subreddits are created every minute; there were over 200K+ subreddits created in just the past few months.)

Both sets of data took a very long time to retrieve, so I implemented cacheing to save each page fetched to disk.  I reviewed Jeremy Singer-Vine's scraping materials and adapted the cacheing parts to my use case.

This all took way, way longer than I anticipated for several reasons:
1 - There were so many pages, and I put `time.sleep(2)` after each request.  I probably spent well over a few hours having the scraping script execute on my local machine.
2 - Unexpected issue related (I think?) to global load on Reddit servers.  I'd pass in a limit of 100 records to retrieve per request (the max allowable).  Sometimes I'd get exactly 100, other times 99, 86, 52 even.  It was unpredictable, so I adapted my scraping/crawling code to account for that.

## Data Analysis Process
Data analysis entailed parsing scraped data using pandas, using parsed data to scrape more data, writing parsed dataframes to new files, and designing charts and tables using those files.  Parsing included general ETL along with getting word frequencies and extracting topics, detailed further below.

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
