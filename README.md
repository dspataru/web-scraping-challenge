# web-scraping-challenge


## Table of Contents
* [Background](https://github.com/dspataru/web-scraping-challenge/blob/main/README.md#background)
* [Section 1: Scrape Titles and Preview Text from Mars News](https://github.com/dspataru/web-scraping-challenge/blob/main/README.md#section-1-scrape-titles-and-preview-text-from-mars-news)
* [Section 2: Scrape and Analyze Mars Weather Data](https://github.com/dspataru/web-scraping-challenge/blob/main/README.md#section-2-scrape-and-analyze-mars-weather-data)

## Background

This repository contains a small project centered on web-scraping and data analysis. This project is broken into two sections: (1) Scraping titles and previewing text from Mars news articles, and (2) Scraping and analyzing Mars weather data from a table. The process involves identifying HTML elements on a page through their id and class attributes, and extracting this information via both automated browisng with Splinter and HTML parsing with BeautifulSoup.

#### Key Words: Jupyter Notebook, Python, JSON, Beautiful Soup, Splinter, Automated Browsing, Web Scraping, HTML, Chrome DevTools

## Section 1: Scrape Titles and Preview Text from Mars News

For this part of the project, we used Splinter, Beautiful Soup, and JSON libraries. First, automated browsing was used to visit the [Mars News Website](https://static.bc-edx.com/data/web/mars_news/index.html). To identify which elements to scrape, the page was inspected using DevTools. By inspecting the webpage, it was found that each news article preview contains an image, title, article preview, and date. The title elements are stored as 'div.content_title' and the preview elements are stored as 'div.article_teaser_body'. To access each of the text elements, we can use the find_all method. 

NOTE: There is a 'MORE' button on the webpage but it is not clickable. In this case, we do not need to scrape through multiple pages to click through older articles.

Below is a preview of what a text element looks like:

    <div class="list_text">
    <div class="list_date">November 9, 2022</div>
    <div class="content_title">NASA's MAVEN Observes Martian Light Show Caused by Major Solar Storm</div>
    <div class="article_teaser_body">For the first time in its eight years orbiting Mars, NASA’s MAVEN mission witnessed two different types of ultraviolet aurorae simultaneously, the result of solar storms that began on Aug. 27.</div>
    </div>

Next, the titles and preview text of the news articles that were scraped were stored into a Python data structures following these steps:
1. Store each title-and-preview pair in a Python dictionary. And, give each dictionary two keys: title and preview. An example is the following:

    {'title': "NASA's MAVEN Observes Martian Light Show Caused by Major Solar Storm", 'preview': "For the first time in its eight years orbiting Mars, NASA’s MAVEN mission witnessed two different types of ultraviolet aurorae simultaneously, the result of solar storms that began on Aug. 27."}
   
3. Store all the dictionaries in a Python list.

The results can be found in [Part 1: Mars News Jupyter Notebook](https://github.com/dspataru/web-scraping-challenge/blob/main/part_1_mars_news.ipynb).

## Section 2: Scrape and Analyze Mars Weather Data

The website that is used to scrape and analyze Mars weather data is called [Mars Temperature Data](https://static.bc-edx.com/data/web/mars_facts/temperature.html). The Mars Data website contains data representing the weather conditions on Mars from Sol 1 (August 7, 2012 on Earth) to Sol 1895 (February 27, 2018 on Earth). The table on the website contains the following columns:
1. id: the identification number of a single transmission from the Curiosity rover
2. terrestrial_date: the date on Earth
3. sol: the number of elapsed sols (Martian days) since Curiosity landed on Mars
4. ls: the solar longitude
5. month: the Martian month
6. min_temp: the minimum temperature, in Celsius, of a single Martian day (sol)
7. pressure: The atmospheric pressure at Curiosity's location

As mentioned on the webpage, the data was collected via the [Rover Environmental Monitoring Station (REMS)](https://mars.nasa.gov/msl/spacecraft/instruments/rems/). 

Automated browsing was used to visit the Mars Temperature Data Site, and the page was inspected to identify which elements to scrape. It was discovered that the div table has two classes: (1) class='container_fluid' and (2) class='py-5'. The title of the table is h1.display-5.fw-bold, the subtitle is p.col-md-8.fs-4, the table is of class='table', the table headings are th and the table enteries are td. A Beautiful Soup object was created and used to scrape the data in the HTML table. Note that this can also be achieved by using the Pandas read_html function, but for the purposes of this project, Beautiful Soup is used. Next is storing the data. The data was scraped into a Pandas DataFrame with the same columns as found on the webpage. Below is a preview of the first five rows of the DataFrame.

![mars_weather_df_first_5](https://github.com/dspataru/web-scraping-challenge/blob/main/images/mars_weather_df_first_5.png)















