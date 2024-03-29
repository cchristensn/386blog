---
layout: post
title:  "Top Board Game Data" 
date: 2024-03-27
description: Data Curation Results   
image: "/assets/img/PoweredByBGG.png"
display_image: true  # change this to true to display the image below the banner 
---

### So, What's All This Then?

As you probably know, this blog covers the data that I collected for Stat 386. My data set includes information on the top board games as rated on BoardGameGeek (BGG). Data collected using BoardGameGeek's XML API (BGG XML API or BGG API) and web scraping.

If you don't know me, I am 'The Board Game Guy'. I absolutely adore the intrigue and strategy that these games bring. This project is backed by my genuine interest in the subject, and I had a blast working on it.

#### Dataset variables

My data has information on the top 100 games for each category, as well as overall. Because a game can have multiple categories (e.g., Strategy and War), the dataset contains 751 games.

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

Because I used both web scrapping and an API, I needed to check two different pages to see if I could ethically collect the data. For web scrapping, I checked the [BGG Robots.txt](https://boardgamegeek.com/robots.txt). The pages I wanted to scrape from were not disallowed and general users are allowed access to the majority of the site. For the API, I checked the [BGG API Terms of Use](https://boardgamegeek.com/wiki/page/XML_API_Terms_of_Use). The API is free to use but asks users to credit BGG as the source of the data.

After checking both of these pages, I was good to start my curation process.

### Collection Processes

#### Web scraping

The data collection process was completed in two parts. For the first part, I needed the internal game ids of the top games. To accomplish this, I web scraped BGG's ranking pages. This was quite simple, as game ids were under a unique class in the html code. Furthermore, the ids were found in order of their rank, so I could use their index to determine their rank.

The code I used to get the ids and ranks was similar to:

```
r = requests.get(url)

soup = BeautifulSoup(r.text)

gameids = soup.find_all('a', {'class': 'primary'})

```

I then put the ids I scraped into a data frame with its ranking. I repeated this process for every page I wanted to scrape from. Each data frame had 100 entries and I had 9 data frames total. I then used a full outer join on all tables based on game id to create one large data frame with every unique game and rankings for each category.

#### API

The second part required using BGG XML API to get information on plays and statistics for each game. Despite the majority of what I wanted being on one page, the API has the information under multiple paths.

|![Ark Nova Stats]({{site.url}}{{site.baseurl}}/assets/img/ArkNovaStats.png)|
|:--:| 
| The Stats Page for *Ark Nova* |

There were two different paths that I needed to use to collect all the data I wanted. The first path that I used was /xmlapi2/plays. This path, unsurprisingly, gives information on a game’s logged plays. I used this for the variable 'Plays Last Month'. I gave the API the game id and the minimum date to count plays from. It returns a large XML file that contained a single line with the information I wanted, followed by every play log since the minimum date.

 I used BeutifulSoup and Regex to extract the total plays in the last month for each game (When using BeutifulSoup on XML, make sure to specify the parameter `features = 'xml'`). Something to note, the window of my data collection is capped at when my code ran. The figure that I recorded was the number of plays between Feb 25, 2024 and Mar 25, 2024.

 The following sudo code is what I used to get the number of plays for each game:

```
playparameters = {"id": <comma separated list of game ids>, 
                      'type': 'thing',
                      'mindate':'2024-02-25'}

r=requests.get(<api 'plays' path>, params=playparameters)

soup = BeautifulSoup(r.text, features='xml')
gamePlays = re.findall('total="(\d+)"', str(soup.find('plays')))
```

I then used the 'thing' API path to get the rest of the information that I needed. For my purposes, I also needed to specify the parameter `stats=1`. The process was similar to what I did for getting the number of plays, and allowed me to collect the rest of my variables.

After all of this, I put everything into the data frame that I originally created. In the end, I had a pandas data frame with 751 rows and 18 columns. The only columns with missing values are the `{Category} Rank` columns, which only have 100 non-missing values each. This is mostly because each game belongs to one or two different categories, and thus can't be ranked in other areas.

### Conclusions

I have used the BGG API before when we first used APIs in python, so it was nice using something that I already was familiar with and improve on what I already knew. It was also fun working with board game data. As I said above, board games are my passion, and I am super excited to be exploring this data and parsing any patterns that I can find. If you love board games as well, stay tuned! My next post will be using this data set to make graphs and exploring different EDA questions.
