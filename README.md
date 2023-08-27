# web-scraping-challenge


## Table of Contents
* [Background](https://github.com/dspataru/web-scraping-challenge/blob/main/README.md#background)
* [Section 1: Scrape Titles and Preview Text from Mars News](https://github.com/dspataru/web-scraping-challenge/blob/main/README.md#section-1-scrape-titles-and-preview-text-from-mars-news)
* [Section 2: Scrape and Analyze Mars Weather Data](https://github.com/dspataru/web-scraping-challenge/blob/main/README.md#section-2-scrape-and-analyze-mars-weather-data)

## Background

This repository contains a small project centered on web-scraping and data analysis. This project is broken into two sections: (1) Scraping titles and previewing text from Mars news articles, and (2) Scraping and analyzing Mars weather data from a table. The process involves identifying HTML elements on a page through their id and class attributes, and extracting this information via both automated browisng with Splinter and HTML parsing with BeautifulSoup.

## Section 1: Scrape Titles and Preview Text from Mars News

## Section 2: Scrape and Analyze Mars Weather Data

The website that is used to scrape and analyze Mars weather data is called (Mars Temperature Data)[https://static.bc-edx.com/data/web/mars_facts/temperature.html]. The Mars Data website contains data representing the weather conditions on Mars from Sol 1 (August 7, 2012 on Earth) to Sol 1895 (February 27, 2018 on Earth). The table on the website contains the following columns:
1. id: the identification number of a single transmission from the Curiosity rover
2. terrestrial_date: the date on Earth
3. sol: the number of elapsed sols (Martian days) since Curiosity landed on Mars
4. ls: the solar longitude
5. month: the Martian month
6. min_temp: the minimum temperature, in Celsius, of a single Martian day (sol)
7. pressure: The atmospheric pressure at Curiosity's location

As mentioned on the webpage, the data was collected via the (Rover Environmental Monitoring Station (REMS))[https://mars.nasa.gov/msl/spacecraft/instruments/rems/]. 

Automated browsing was used to visit the Mars Temperature Data Site, and the page was inspected to identify which elements to scrape. It was discovered that the div table has two classes: (1) class='container_fluid' and (2) class='py-5'. The title of the table is h1.display-5.fw-bold, the subtitle is p.col-md-8.fs-4, the table is of class='table', the table headings are th and the table enteries are td. A Beautiful Soup object was created and used to scrape the data in the HTML table. Note that this can also be achieved by using the Pandas read_html function, but for the purposes of this project, Beautiful Soup is used. Next is storing the data. The data was scraped into a Pandas DataFrame with the same columns as found on the webpage. Below is a preview of the first five rows of the DataFrame.

!(mars_weather_df_first_5)[]















