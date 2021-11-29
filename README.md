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

<b>COMING SOON</b>


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
