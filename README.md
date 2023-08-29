# web-scraping-challenge

![mars](https://github.com/dspataru/web-scraping-challenge/blob/main/images/mars.jpg)


## Table of Contents
* [Background](https://github.com/dspataru/web-scraping-challenge/blob/main/README.md#background)
* [Section 1: Scrape Titles and Preview Text from Mars News](https://github.com/dspataru/web-scraping-challenge/blob/main/README.md#section-1-scrape-titles-and-preview-text-from-mars-news)
* [Section 2: Scrape and Analyze Mars Weather Data](https://github.com/dspataru/web-scraping-challenge/tree/main#section-2-scrape-and-analyze-mars-weather-data)

## Background

This repository contains a small project centered on web-scraping and data analysis. This project is broken into two sections: (1) Scraping titles and previewing text from Mars news articles, and (2) Scraping and analyzing Mars weather data from a table. The process involves identifying HTML elements on a page through their id and class attributes, and extracting this information via both automated browisng with Splinter and HTML parsing with BeautifulSoup.

#### Key Words: Jupyter Notebook, Pandas, Python, JSON, Beautiful Soup, Splinter, Automated Browsing, Web Scraping, HTML, Chrome DevTools

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

Automated browsing was used to visit the Mars Temperature Data Site, and the page was inspected to identify which elements to scrape. It was discovered that the div table has two classes: (1) class='container_fluid' and (2) class='py-5'. The title of the table is h1.display-5.fw-bold, the subtitle is p.col-md-8.fs-4, the table is of class='table', the table headings are th and the table enteries are td. 

A Beautiful Soup object was created and used to scrape the data in the HTML table. Note that this can also be achieved by using the Pandas read_html function, but for the purposes of this project, Beautiful Soup is used. Below is a snippet of a few records found by scraping the website:

    [['2', '2012-08-16', '10', '155', '6', '-75.0', '739.0'],
     ['13', '2012-08-17', '11', '156', '6', '-76.0', '740.0'],
     ['24', '2012-08-18', '12', '156', '6', '-76.0', '741.0'],
     ['35', '2012-08-19', '13', '157', '6', '-74.0', '732.0'],
     ['46', '2012-08-20', '14', '157', '6', '-74.0', '740.0'],
     ['57', '2012-08-21', '15', '158', '6', '-78.0', '740.0'],
     ['68', '2012-08-22', '16', '158', '6', '-77.0', '740.0'],
     ['79', '2012-08-23', '17', '159', '6', '-76.0', '742.0'],
     ['112', '2012-08-27', '21', '161', '6', '-74.0', '741.0'],
     ['114', '2012-08-28', '22', '162', '6', '-74.0', '742.0']]

Next is storing the data. The data was scraped into a Pandas DataFrame with the same columns as found on the webpage. Below is a preview of the first five rows of the DataFrame.

![mars_weather_df_first_5](https://github.com/dspataru/web-scraping-challenge/blob/main/images/mars_weather_df_first_5.png)

Once the data was saved as a pandas DataFrame, the data was prepared for analysis. First the data type of each column was examined and converted to the appropriate data type: `datetime`, `int`, or `float`, using Pandas `astype` and `to_datetime` methods. The original columns types are seen below:

    id                  object
    terrestrial_date    object
    sol                 object
    ls                  object
    month               object
    min_temp            object
    pressure            object
    dtype: object

and the adjusted data types are as follows:

    id                          object
    terrestrial_date    datetime64[ns]
    sol                          int64
    ls                           int64
    month                        int64
    min_temp                   float64
    pressure                   float64
    dtype: object

The dataset was then analyzed by using Pandas functions to answer the following questions:
1. How many months exist on Mars?
2. How many Martian (and not Earth) days worth of data exist in the scraped dataset?
3. What are the coldest and the warmest months on Mars (at the location of Curiosity)? To answer this question, we found the average the minimum daily temperature for all of the months, and plotted the results as a bar chart.
4. Which months have the lowest and the highest atmospheric pressure on Mars? To answer this question, we found the average the daily atmospheric pressure of all the months, and plotted the results as a bar chart.
5. About how many terrestrial (Earth) days exist in a Martian year? To answer this question, we considered how many days elapse on Earth in the time that Mars circles the Sun once, and visually estimate the result by plotting the daily minimum temperature.

The complete analysis can be found in [Part 2: Mars Weather Jupyter Notebook](https://github.com/dspataru/web-scraping-challenge/blob/main/part_2_mars_weather.ipynb)

To answer question #1, the pandas DataFrame was grouped by month using the `groupby()` method and the months were counted using the `count()` method on the grouped DataFrame. The result is:

    month
    1     174
    2     178
    3     192
    4     194
    5     149
    6     147
    7     142
    8     141
    9     134
    10    112
    11    138
    12    166
    Name: month, dtype: int64

To answer the second question, the `count()` method was used, and the number of Martian days' worth of data was: **1867**.

    num_martian_days = marsWeather_df['terrestrial_date'].count()
    num_martian_days

TO answer the third question, the average low temperature by month was found by grouping the DataFrame by month and using the `.agg()` function to find the average minimum temperture for each month, which rendered the following result:

    avg_low_temp_by_month = marsWeather_df.groupby('month').agg({'min_temp' : 'mean'})
    avg_low_temp_by_month

![avg low temp by month](https://github.com/dspataru/web-scraping-challenge/blob/main/images/avg_low_temp_by_month.png)

The average low temperatures by month were then plotted:

![avg min temp by month](https://github.com/dspataru/web-scraping-challenge/blob/main/images/avg_minTemp_by_month.png)

The coldest and hottest months were found to be month 3 and month 8 respectively. To make this easier to visualize, the data was sorted by minimum temperature and plotted again:

![avg min temp by month](https://github.com/dspataru/web-scraping-challenge/blob/main/images/avg_temp_by_month_sorted.png)

To answer question #4, the average pressure by Martian month was found using the `groupby()` method on the month, and calculating the average using the `mean()` function to achieve the following result, which was then plotted in a bar graph:

    month
    1     862.488506
    2     889.455056
    3     877.322917
    4     806.329897
    5     748.557047
    6     745.054422
    7     795.105634
    8     873.829787
    9     913.305970
    10    887.312500
    11    857.014493
    12    842.156627
    Name: pressure, dtype: float64

Atmospheric pressure is, on average, lowest in the sixth month and highest in the ninth.

![avg pressure by month](https://github.com/dspataru/web-scraping-challenge/blob/main/images/avg_pressure_by_month.png)

Lastly, to answer question #5 (How many terrestrial (earth) days are there in a Martian year?), the number of terrestrial days was plotted against the minimum temperature in degrees celcius.

![mars temp vs earth days](https://github.com/dspataru/web-scraping-challenge/blob/main/images/marsTemp_vs_EarthDays.png)

The distance from peak to peak is roughly 1425-750, or 675 days. A year on Mars appears to be about 675 days from the plot. Internet search confirms that a Mars year is equivalent to 687 earth days.

The DataFrame was then exported to a csv file using the following piece of code, and can be found by following this link: [mars_weather.csv](https://github.com/dspataru/web-scraping-challenge/blob/main/mars_weather.csv)

