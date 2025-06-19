Title: Scraps and Scrapes - Web Scraping UFC Fight Data
Date: 2025-06-18
Tags: scraping, python, UFC, data, BeautifulSoup
Category: MMA Analytics
Slug: data-scraping
Authors: Oscar Kelly
Summary: A technical overview of how I used Python and BeautifulSoup to build a UFC dataset.
Status: published

### Why Data Quality is Important
There's a well-known saying in the data industry that describes how your model's predictive capabilities will never be significantly better than the quality of the training data.

*Sh\*t in = sh\*t out*

So, before we can do any thought-provoking analysis, we need some good data.

### Straight to the Source
Luckily, the UFC are kind enough to provide data on all of their events down to the round-level, via the [UFCstats](http://www.ufcstats.com) website. Under the *Events and Fights* section, you can select individual fights from any event and see striking and grappling stats for each fighter in each of the rounds fought - it also includes other data such as the final scorecards (if it was a decision), the referee, and the weightclass at which the fighters fought.

This section of UFCstats doesn't have everything unfortunately - some missing data includes:

- Round-by-round scorecards (though in hindsight, I don't know if the UFC actually publish these anyway...)
- If a fighter missed weight
- A fighter's stance
- How Bruce Buffer introduces them (where he calls them "a striker", or a "brawler" - I've always wondered how they decide who's what kind of fighter... We'll be exploring this in a later article!)

Despite some of the missing data, I believe I can collect this at a later date, and include it as fighter metadata in analysis going forward. But for the start of this project, I wanted to collect the stats from each fight. This would enable me to do a couple of things: first, I can see how fighters have performed over time, from the start of their career to the present day. Secondly, I can calculate some other interesting stats that often come up when talking about UFC fighters - e.g. SLpM (Strikes Landed per Minute) can be calculated from a fighter's total strikes landed and the length of each fight.

### Accessing the Data
The problem is, accessing this potential goldmine of data is very difficult - there's no download button, and no API that I could find that was freely available. But the website did have a consistent structure for every fight in every event for the last 15 or so years.

Enter `BeautifulSoup`.

For the unacquainted, `BeautifulSoup` is a *web scraping* python package, letting you pull data from websites, provided they have a consistent HTML structure.

Let's go through the steps I used to create my starting dataset.

### Step 1: Scrape All Event URLs
We have already identified the data source, but now we need to access each of the events in turn, so we can scrape the data from their respective fights. I used a simple function that scraped the [events page](http://ufcstats.com/statistics/events/completed?page=all), searched the HTML code for each event's URL, and pulled it into a list. This can now be iterated through to access each event in turn.

### Step 2: Extract All Fights From Each Event
I iterated through our event URL list, pulling all of the fight URLs from the HTML code of each event webpage. These fight URLs were then stored in a new list, creating a list of all UFC fights that have taken place since around 2009 (I didn't want to collect data that was too old, but decided that UFC100 was a good starting point, since it would include active UFC veterans and had the same HTML structure as more recent events).

### Step 3: Scrape Fight-Level Stats
Using another function, I iterated through the fight URLs to access the data associated with each fight. I pulled as much as I could from the page, starting with the fight-level data, then moving onto each of the individual rounds. The scraper had to be dynamic, as some fights ended early in round 1, while some went the full distance (either 3 rounds for normal fights, or 5 rounds for fights with a belt on the line/headline fights). So, I assumed I was collecting 5 rounds of data, and if the fight ended in round 1, the data in rounds 2-5 are filled with `NaN` values, to simplify things.

In addition to fight statistics, I collected data related to the fight itself: who the referee was, the fight length in seconds, the judges' names and scorecards if the fight ended in a decision, and the method of victory, amongst others. These statistics will allow me to add extra information to my models, and look into predicting things like how fights might end, rather than just if they will finish inside the distance.

I now faced a problem: how should I be storing this data? I couldn't set up a dictionary with all of the UFC fighters names - ~~that would take too long and I'm too lazy~~ it would be inefficient. If a new fighter came along, I would have to add their name to the dictionary before I could pull data for them.

Thankfully, Python already had a solution: the `defaultdict` in the `collections` module won't throw a KeyError if you pass a new key into it like a normal dictionary would. Instead, it seamlessly creates a new key for you!

### Step 4: Time Crisis
I pulled all of the fight data I could from every fight since UFC100 - thousands of fights, with hundreds of data points in each. My script ran for over an hour (if anyone has any tips to make this process more efficient, feel free to let me know in the comments!), and I immediately saved the JSON output locally to ensure I wouldn't lose it. I then tried to plot some data for a fighter over a period of time, to see how their stats had changed over time.

One rather crucial piece of data was missing from the fight pages... The date the fight took place.

So, back at the drawing board, I created a mapping dictionary - this mapped the fight URLs to the event date contained in the event page. Armed with this, I could modify the data scraping function to add this date in as metadata alongside the fight data, ensuring that I could create time series from the `defaultdict` at the end.

The final data object looked something like this:

```python
{
    ...,
    'Max Holloway': {
        'Ilia Topuria': [{'metadata': {'Fighter_1': 'Ilia Topuria',
        'Fighter_2': 'Max Holloway',
        'Weight_Class': 'UFC Featherweight Title Bout',
        ...,
        'Date': '2024-10-26'},
       'stats': {'FIGHT_KD_1': 1,
        'FIGHT_KD_2': 0,
        ...,
        'url': 'http://ufcstats.com/fight-details/ebf7cea27b83c432'}],
        'Justin Gaethje': [...],
        ...,
        },
    ...
}
```

The nested dictionary above stores each fighter's fights as keys, mapping to lists of dictionaries with their fight metadata and statistics. This structure lets us:

- Quickly access a fighter's historical stats
- Perform time-based filtering using the "Date" field
- Track changes in performance against different opponents

### Final Thoughts

That's it! Now we have a rather complex but rich dataset that can be used in all sorts of analysis projects. We have a time component that will allow for time series analysis, plenty of numerical and categorical data to allow basic analysis such as comparing different stats between fighters, or more complex analysis such as predicting who is likely to win a bout in a future event.

They say that data acquisition and cleaning is 80% of a data scientist's job, and only around 20% is spent actually doing the fun stuff like modelling, predicting, and drawing conclusions from the data. We will now be moving onto that 20% in the next article, where we'll use this dataset to create visual timelines of fighter stats, starting with some familiar names.

As always, feel free to let me know if you enjoyed this article, if there's anything you think I've missed, and what you would like to see next!