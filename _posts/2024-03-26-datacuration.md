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

Because I used both webscrapping and an API, I needed to check two different pages to see if I could ethically collect the data. For webscrapping, I checked the [BGG Robots.txt](https://boardgamegeek.com/robots.txt). The pages I wanted to scrape from were not disallowed and general users are allowed access to the majority of the site. For the API, I checked the [BGG API Terms of Use](https://boardgamegeek.com/wiki/page/XML_API_Terms_of_Use). The API is free to use, but asks users to credit BGG as the source of the data.

After checking both of these pages, I was good to start my curation process.


### Collection Processes

#### Webscraping

The data collection process was completed in two parts. For the first part, I needed the internal game ids of the top games. To accomplish this, I webscraped BGG's ranking pages. This was quite simple, as game id's were under a unique class in the html code. Furthermore, the ids were found in order of their rank, so I could use their index to determine their rank.

The code I used to get the ids and ranks was similar to:

```
r = requests.get(url)

soup = BeautifulSoup(r.text)

gameids = soup.find_all('a', {'class': 'primary'})

```

I then put the ids I scraped into a dataframe with its ranking. I repeated this process for every page I wanted to scrape from. Each data frame had 100 entrys and I had 9 dataframes total. I then used a full outer join on all tables based on game id to create one large dataframe with every unique game an rankings for each category.

#### API

The second part required using BGG XML API to get information on plays and statistics for each game. Despite the majority of what I wanted being on one page, the api has the information under multiple paths.

|![Ark Nova Stats]({{site.url}}{{site.baseurl}}/assets/img/ArkNovaStats.png)|
|:--:| 
| The Stats Page for *Ark Nova* |

There were two different paths that I needed to use to collect all the data I wanted. The first path that I used was /xmlapi2/plays. This path, unsuprisingly, gives information on a games logged plays. I used this for the variable 'Plays Last Month'. I gave the API the game id and the minimum date to count plays from. It returns a large XML file that contained a single line with the information I wanted, followed by every play log since the minimum date. I used BeutifulSoup and Regex to extract the total plays in the last month for each game (When using BeutifulSoup on XML, make sure to specify the parameter `features = 'xml'`). Something to note, the window of my data collection is capped at when my code ran. The figure that I recorded was the number of plays between Feb 24, 2024 and Mar 25, 2024.
