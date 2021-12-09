# Currently under development.  BETA will be released soon.
########### ########### ########### ########### ########### 

# Primary Use Case
<p align="justify"> 
Textual analysis is a broad term for various research methodologies used to qualitatively describe, interpret and understand text data. These methodologies are mainly used in academic research to analyze content related to media and communication studies, popular culture, sociology, and philosophy. Textual analysis allows researchers to quickly obtain relevant insights from unstructured data. All types of information can be gleaned from textual data, especially from social media posts or news articles. Some of this information includes the overall concept of the subtext, symbolism within the text, assumptions being made and potential relative value to a subject (e.g. data science). In some cases it is possible to deduce the relative historical and cultural context of a body of text using analysis techniques coupled with knowledge from different disciplines, like linguistics and semiotics.

<i>NewsHound</i> was designed to assist researchers in these tasks by performing high quality news and article extraction for sources in multiple languages. For instance <i>NewsHound</i> allows you to scrape article content from <a href="https://www.bbc.com">the BBC</a> in English, the <a href="www.bhaskar.com">Dainik Bhaskar</a> in Hindi, the <a href="www.people.com.cn">People's Daily</a> in Chinese and the <a href=" www.khaosod.co.th">Khaosod</a> in Thai.
  
<i>NewsHound</i> is designed to scrape news sites for these common data elements:
  
- Title/Headline
- Description/Summary
- Keywords 
- Author(s)
- Text/Content
- Language Type 
- Published Date
- Modified Date
- Top Image
</p>


# Installation

<p align="justify"> 
   Install the distribution via pip:
</p>

```python
pip3 install newshound
```


# General Package Utilization

<i>NewsHound</i> usage is slightly different that other Python Packages, such as <a href="https://github.com/codelucas/newspaper">Newspaper3k</a>.  The latter package requires an end-user to call the functions <i>download()</i> and <i>parse()</i> prior to calling a function like <i>title</i>.  <i>Newspaper3k</i> also required an end-user to called the Class Config() to pass variables (e.g., User-Agent) to <i>Python Requests</i>. <i>NewsHound</i> takes care of this basic housekeeping without user intervention.

For example this is how an end-user would request data extraction for a single article using <i>NewsHound</i>.

```python 
from newshound import Article

article = Article(source_url='https://www.cnn.com/2021/12/08/europe/germany-covid-europe-intl/index.html')
```

Here is how an end-user would obtain the Publish date and last modified date of an article. Please note that some articles do not have a modified date, so <i>NewsHound</i> will provide this text: "article modified date not found." 

```python 
from newshound import Article

article = Article(source_url='https://www.cnn.com/2021/12/08/europe/germany-covid-europe-intl/index.html')

print(article.published_date)
2021-12-08T13:05:07Z

print(article.modified_date)
2021-12-08T15:12:44Z
```

Here is how to obtain the article's title.

```python 
from newshound import Article

article = Article(source_url='https://www.cnn.com/2021/12/08/europe/germany-covid-europe-intl/index.html')

print(article.title)
germany records highest number of covid-19 deaths since february - cnn
```

Here is how to obtain an article's description.

```python 
from newshound import Article

article = Article(source_url='https://www.cnn.com/2021/12/08/europe/germany-covid-europe-intl/index.html')

print(article.description)
Germany recorded its highest number of daily deaths from Covid-19 since February on Wednesday, as it struggles to bring a fourth wave of the pandemic under control.
```

Here is how to obtain the names of the individuals that wrote the article.

```python 
from newshound import Article

article = Article(source_url='https://www.cnn.com/2021/12/08/europe/germany-covid-europe-intl/index.html')

print(article.authors)
['Laura Smith-Spark', 'Stephanie Halasz']
```

Here is how to obtain the language that the article was written in.

```python 
from newshound import Article

article = Article(source_url='https://www.cnn.com/2021/12/08/europe/germany-covid-europe-intl/index.html')

print(article.language)
english(united states)
```

Here is how to find the published keywords associated with an article.

```python 
from newshound import Article

article = Article(source_url='https://www.cnn.com/2021/12/08/europe/germany-covid-europe-intl/index.html')

print(article.keywords)
['europe', 'germany records highest number of covid-19 deaths since february - cnn']
```

Here is how to obtain the article's URL and the URL of the top image used in the article.

```python 
from newshound import Article

article = Article(source_url='https://www.cnn.com/2021/12/08/europe/germany-covid-europe-intl/index.html')

print(article.url)
https://www.cnn.com/2021/12/08/europe/germany-covid-europe-intl/index.html

print(article.top_image_url)
https://cdn.cnn.com/cnnnext/dam/assets/211208054441-germany-hospital-coronavirus-patient-11-30-2021-super-tease.jpg
```

Here is how to obtain the textual content of the article. 

```python 
from newshound import Article

article = Article(source_url='https://www.cnn.com/2021/12/08/europe/germany-covid-europe-intl/index.html')

print(article.text)

A total of 69,601 new infections were reported and an additional 527 people died in the past 24 hours, according to the Robert Koch Institute (RKI), the national disease and control center. That marked the highest Covid-19 daily death toll since February 18, when there were 534 fatalities.Germany's seven-day incidence rate dropped slightly, but remains high at 427 per 100,000 inhabitants. The country has recorded 104,047 deaths from Covid-19 in total since the outbreak of the pandemic.The grim news came on the day that Olaf Scholz was sworn in as Germany's Chancellor, replacing Angela Merkel at the helm of Europe's largest economy. The country's new health minister is Karl Lauterbach, an MP and prominent epidemiologist.Germany last week announced a nationwide lockdown for the unvaccinated, barring them from accessing all but the most essential businesses, such as supermarkets and pharmacies, as it battles to curb infections. The ban doesn't apply to those who have recently recovered from Covid-19.Its leaders also backed plans for mandatory vaccinations in the coming months, which, if voted through the German parliament, could take effect from February at the earliest.Many hospitals are struggling to cope with the increasing number of intensive care patients and German medics have warned that intensive care occupancy could soon exceed that seen during last winter's peak.The emergence of the fast-spreading Omicron coronavirus variant has heightened concerns in Germany as elsewhere.Researchers working in South Africa reported Tuesday that the Omicron variant partly escapes the protection offered by the Pfizer vaccine, although people who have been previously infected and then vaccinated are likely to be well protected. The research team cautioned that it was a small, preliminary study.If approved, Germany's vaccine mandate would follow in the footsteps of neighboring Austria, which also plans to make inoculations for eligible adults compulsory from February.Greece announced last week that vaccines would be mandatory for people aged over 60 from mid-January. Those refusing to do so would face 100 euro (US $113) fines for each passing month, the government said.The United Kingdom marked a year Wednesday since it became the world's first nation to begin vaccinating its citizens with a fully vetted and authorized Covid-19 shot.The UK government is under pressure from leading scientists to introduce tougher restrictions to try to limit infections amid rising case numbers. The seven-day rolling average on November 29 was over 45,000, the highest it's been since a peak around October 17.UK health officials are urging all those eligible to get vaccinated against Covid-19 and has accelerated its booster shot rollout, amid wide concern over the potential impact of the Omicron variant. Last week, the government reimposed the requirement to wear a face covering in shops and on public transport after a number of cases of the new variant were detected in the UK."We can conclude there is now community transmission across multiple regions of England," UK Health Secretary Sajid Javid said Monday of the Omicron variant.At the same time, the UK government is facing an uproar over reports of a staff Christmas party at Downing Street during last year's lockdown.

```

The extracted data elements can also be outputted in <i>JSON</i> or a <i>Pandas Dataframe</i>.  This is accomplished by using the variable <i>output_format</i>, which by default is set to <i>output_format='dictionary'</i>.  You have to call <i>article.all_elements</i> to obtain the requested output. 

<b>JSON Output</b>

```python 
from newshound import Article

article = Article(source_url='https://www.cnn.com/2021/12/08/europe/germany-covid-europe-intl/index.html', output_format='json')

print(article.all_elements)

{
    "published_date": "2021-12-08T13:05:07Z",
    "modified_date": "2021-12-08T15:12:44Z",
    "language": "english (united states)",
    "title": "Germany records highest number of Covid-19 deaths since February - CNN",
    "description": "Germany recorded its highest number of daily deaths from Covid-19 since February on Wednesday, as it struggles to bring a fourth wave of the pandemic under control.",
    "keywords": [
        "europe",
        "Germany records highest number of Covid-19 deaths since February - CNN"
    ],
    "categories": "europe",
    "authors": [
        "Laura Smith-Spark",
        "Stephanie Halasz"
    ],
    "text": "A total of 69,601 new infections were reported and an additional 527 people died in the past 24 hours, according to the Robert Koch Institute (RKI), the national disease and control center. That marked the highest Covid-19 daily death toll since February 18, when there were 534 fatalities.Germany's seven-day incidence rate dropped slightly, but remains high at 427 per 100,000 inhabitants. The country has recorded 104,047 deaths from Covid-19 in total since the outbreak of the pandemic.The grim news came on the day that Olaf Scholz was sworn in as Germany's Chancellor, replacing Angela Merkel at the helm of Europe's largest economy. The country's new health minister is Karl Lauterbach, an MP and prominent epidemiologist.Germany last week announced a nationwide lockdown for the unvaccinated, barring them from accessing all but the most essential businesses, such as supermarkets and pharmacies, as it battles to curb infections. The ban doesn't apply to those who have recently recovered from Covid-19.Its leaders also backed plans for mandatory vaccinations in the coming months, which, if voted through the German parliament, could take effect from February at the earliest.Many hospitals are struggling to cope with the increasing number of intensive care patients and German medics have warned that intensive care occupancy could soon exceed that seen during last winter's peak.The emergence of the fast-spreading Omicron coronavirus variant has heightened concerns in Germany as elsewhere.Researchers working in South Africa reported Tuesday that the Omicron variant partly escapes the protection offered by the Pfizer vaccine, although people who have been previously infected and then vaccinated are likely to be well protected. The research team cautioned that it was a small, preliminary study.If approved, Germany's vaccine mandate would follow in the footsteps of neighboring Austria, which also plans to make inoculations for eligible adults compulsory from February.Greece announced last week that vaccines would be mandatory for people aged over 60 from mid-January. Those refusing to do so would face 100 euro (US $113) fines for each passing month, the government said.The United Kingdom marked a year Wednesday since it became the world's first nation to begin vaccinating its citizens with a fully vetted and authorized Covid-19 shot.The UK government is under pressure from leading scientists to introduce tougher restrictions to try to limit infections amid rising case numbers. The seven-day rolling average on November 29 was over 45,000, the highest it's been since a peak around October 17.UK health officials are urging all those eligible to get vaccinated against Covid-19 and has accelerated its booster shot rollout, amid wide concern over the potential impact of the Omicron variant. Last week, the government reimposed the requirement to wear a face covering in shops and on public transport after a number of cases of the new variant were detected in the UK.\"We can conclude there is now community transmission across multiple regions of England,\" UK Health Secretary Sajid Javid said Monday of the Omicron variant.At the same time, the UK government is facing an uproar over reports of a staff Christmas party at Downing Street during last year's lockdown.",
    "url": "https://www.cnn.com/2021/12/08/europe/germany-covid-europe-intl/index.html",
    "top_image": "https://cdn.cnn.com/cnnnext/dam/assets/211208054441-germany-hospital-coronavirus-patient-11-30-2021-super-tease.jpg"
}

```

<b>Dataframe Output</b>

```python 
from newshound import Article

article = Article(source_url='https://www.cnn.com/2021/12/08/europe/germany-covid-europe-intl/index.html', output_format='dataframe')

print(article.all_elements)


```




    



# Additional Features

## In-memory cache
   
<p align="justify">
<i>NewsHound</i> uses an in-memory cache, which helps prevent redundant queries to an individual resource for the same article.  This cache is currently being erased after each session. 
</p>


## Rate limiting

<p align="justify">
Some sources have ratelimits, which can impact querying and extraction for that source. In some cases exceeding these ratelimits will trigger a <i>Cloudflare</i> challenge session.  Errors related to these blocked sessions are written the <i>newshound_error.yaml</i> file.  Such entries can have a <i>status code</i> of 521, which is a Cloudflare-specific error message. The maintainers of <i>NewsHound</i> have added ratelimits to mutiple modules.  These ratelimits can be modified, but reducing these predefined limits can lead to querying sessions being dropped or blocked by a source.  

Currently there are 2 parameters that can be set:
   
- max_number_of_requests
- rate_limit_timeout_period
   
These parameters are currently set to 30 requests every 60 seconds. 
   
When a ratelimit is trigger a warning message is written to both the console and the <i>newshound_error.yaml</i> file.  The ratelimit will automatically reset after a set time period, which currently cannot be modified using a parameter passed in a `Class object`.  

</p>

```python 
from newshound import Article

article = Article(article_url='https://www.cnn.com/world/live-news/covid-variant-omicron-11-29-21/h_ba3ad8e4fe31cd243ef13c4526ef4fbd', 
                  max_number_of_requests=30, 
                  rate_limit_timeout_period=60)

```

## Proxy usage 

<p align="justify">
<i>NewsHound</i> provides out of the box usage of proxies. Just define your proxies config as a dictionary and pass it to the corresponding module as shown below.
</p>

```python 
from newshound import Article
proxies_example = {
    "http": "your http proxy if available" # example: http://149.28.94.152:8080
    "https": "your https proxy"  # example: https://128.230.60.178:3128
}

article = Article(article_url='https://www.cnn.com/world/live-news/covid-variant-omicron-11-29-21/h_ba3ad8e4fe31cd243ef13c4526ef4fbd', 
                  proxies=proxies_example)
```
<p align="justify">
There is a known bug in <i>urllib3</i> between versions 1.26.0 and 1.26.7, which will raise different errors. <i>NewsHound</i> will be using <i>urllib3</i> version 1.25.11 until the bug is fixed in a future release.  
</p>

## Output Formatting

<p align="justify">
The default output of <i>NewsHound</i> is a <i>Python</i> Dictionary.  The output format can be changed to output the extraction results to JSON, Pandas DataFrame or HTML. The code example below shows how to change the formatting.  
</p>

```python
from newshound import Article

# output_format='dictionary'
# output_format='dataframe'
# output_format='json'
# output_format='html'
article = Article(article_url='https://www.cnn.com/world/live-news/covid-variant-omicron-11-29-21/h_ba3ad8e4fe31cd243ef13c4526ef4fbd', 
                  output_format='dictionary')

```

## Logging 
<p align="justify">
This application also uses <i>Python logging</i> to the logfile <i>newshound_error.yaml</i>.  The maintainers of <i>NewsHound</i> have attempted to catch any potential exception and write these error messages to the logfile. The logfile is useful to troubleshooting any issue with this package or with the sources being queried by <i>NewsHound</i>.
</p>

# Predefined Extraction

<p align="justify">
The maintainers of <i>NewsHound</i> have developed and tested multiple <a href="https://github.com/johnbumgarner/newshound/blob/master/predefined_extraction_sources.md">predefined extraction modules</a> for various news sources around the world.  Additional sources will be added periodically.  
</p>

# Dependencies

<p align="justify">
This package has these core dependencies:
  
1. <b>backoff</b>
2. <b>BeautifulSoup</b>
3. <b>deckar01-ratelimit</b>
4. <b>langdetect</b>
5. <b>lxml</b>
6. <b>requests</b>
7. <b>tldextract</b>
8. <b>urllib3</b>
</p>

# Development

<p align="justify">
If you would like to contribute to the <i>NewsHound</i> project please read the <a href="https://github.com/johnbumgarner/newshound/blob/master/CONTRIBUTING.md">contributing guidelines</a>.
   
Items currently under development:
   - TDB after BETA release
</p>

# Issues

<p align="justify">
This repository is actively maintained.  Feel free to open any issues related to bugs, coding errors, broken links or enhancements. 

You can also contact me at [John Bumgarner](mailto:newshoundproject@gmail.com?subject=[GitHub]%20newshound%20project%20request) with any issues or enhancement requests.
</p>


# Limitations
   
<p align="justify">
   
The querying capabilities of this Python package is highly dependent on the navigational structure of each source in the query pool.  If a source modifies its navigational structure then extraction from that specific source will likely have some challenges. The maintainers of <i>NewsHound</i> will correct these navigational extraction issues when they are discovered in periodic testing or reported as an issue.  

Some of the news sources located in the European Union have a General Data Protection Regulation (GDPR) warning.  For instance, the Die Zeit news site has an advertisement and GDPR tracking acknowledgement button, which requires the use of the Python library <i>selenium</i> coupled with <i>NewsHound</i> to extract article elements from this news source.  The maintainers of <i>NewsHound</i> are exploring options to generically acknowledge these warning messages.  
  
News sources that require subscription services to access content is another limitation.  The maintainers of <i>NewsHound</i> are looking at ways to generically handle login to these news sites. 

The maintainers of <i>NewsHound</i> have developed this package with both targeted extraction for predefined news sites and generic extraction techniques for other sites.  The latter technique will make its best effort to extract content from an unknown news source.  
</p>

# Sponsorship
   
If you would like to contribute financially to the development and maintenance of the <i>NewsHound</i> project please read the <a href="https://github.com/johnbumgarner/newshound/blob/master/SPONSOR.md">sponsorship information</a>.

# License

<p align="justify">
The MIT License (MIT).  Please see <a href="https://github.com/johnbumgarner/newshound/blob/main/LICENSE">License File</a> for more information.
</p>
