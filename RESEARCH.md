
| WebScraping | Research |
| -------- | -------------- |
| Article:| Beautiful Soup: Build a Webscarper With Python |
| Source: | https://realpython.com/beautiful-soup-web-scraper-python/ |
| Reason: | Wanted to learn the basics of webscraping |


**Challenges of web scraping:**

Variety: every website is different, while you can encounter general structures that repeat themselves, website is unique and will need personal treatment of you want to extract relevant info

Durability: websites constantly change, first time you run your script it might work flawlessly but if you run it again a while later you might get a stack of tracebacks

-scrapers generally require constant maintenance

-you can set up continuous integration to run scarping tests periodically to ensure that your main script doesn’t break without your knowledge 

Continuous integration: practice of frequently building and testing each change done to your code automatically and as early as possible 

-API’s (application programming interfaces) allow you to access websites data in a predefined manner

* API structures don’t change as frequently but CAN still be changed, it is usually more permanent an is a more reliable source if the site’s data 
* HOW TO GATHER INFO USING API’s


**How to webscrape:**

Step 1: Inspect your data source

-First step is to inspect the website you want to scrape, need to understand the cite structure to extract the info that relevant 
* likely when you click on an internal link within the website, the website url will change
* learn to decipher info in urls 

Example:

	https://realpython.github.io/fake-jobs/jobs/senior-python-developer-0.html

-can deconstruct the URL into two main parts 

The base url represents the path to the search functionality of the website

The specific site location that ends with .html is the path to the job description’s unique resource

-URLs can hold more info than just the location of a file, some websites use query parameters to encode values that you submit when performing a search 

-Query parameters can be thought of as query strings that you send to the database to retrieve specific records 

	URL example:  https://au.indeed.com/jobs?q=software+developer&l=Australia

-the query parameters in this URL are: ?q=software+developer&l=Australia

Query parameters consist of three parts:

Start: the beginning of the query parameters is denoted by a question mark (?)

Information: the pieces of info constituting one query parameter are encoded in key-value pairs, where related keys and values are joined together by an equals sign (key=value)

Separator: Every URL can have multiple query parameters, separated by an ampersand symbol (&)

Can look at the URL’s query parameters into two key value pairs:

q=software+developer selects the type of job.

l=Australia selects the location of the job.

