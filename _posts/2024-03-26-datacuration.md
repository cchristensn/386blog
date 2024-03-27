---
layout: post
title:  "Top Board Game Data" 
date: 2024-03-27
description: Data Curation Results   
image: "/assets/img/PoweredByBGG.png"
display_image: true  # change this to true to display the image below the banner 
---

### So, What's All This Then?

As you probably know, this blog covers the data that I collected for Stat 386. My data set includes information on the top board games as rated on BoardGameGeek (BGG). Data collected using BoardGameGeek's XML API (BGG XML API or BGG API) and webscraping.

#### Dataset variables

My data has information on the top 100 games for each category, as well as overall. Because a game can have multiple categories (e.g. Strategy and War), the dataset contains 751 games.

My dataset has the variables:

- Name

- Year

- ID

- Rating

- Complexity

- Overall Rank

- Plays Last Month

- Owns

- Wants

- Wishlists

- {Category} Rank (Category being any major game category on BGG)

To view the data and/or documentation, check out my [GitHub Repo](https://github.com/cchristensn/datacuration)

### Was My Collection Ethical?

Yea, trust me bro. [BGG API Terms of Use](https://boardgamegeek.com/wiki/page/XML_API_Terms_of_Use)
[BGG Robots.txt](https://boardgamegeek.com/robots.txt)

### Collection Processes

The data collection process was completed in two parts. For the first part, I needed the internal game ids of the top games. To accomplish this, I webscraped BGG's ranking pages. This was quite simple, as game id's were under a unique class in the html code. Furthermore, the ids were found in order of their rank, so I could use their index to determine their rank.

The code I used to get the ids and ranks was similar to:

```
r = requests.get(url)

soup = BeautifulSoup(r.text)

gameids = soup.findall('a', {'class': 'primary'})

```

The second part required using BGG XML API to get information on plays and statistics for each game.