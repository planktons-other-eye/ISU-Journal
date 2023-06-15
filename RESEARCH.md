
| WebScraping | Research | Practice
| -------- | -------------- | ---------- |
| Article:| Beautiful Soup: Build a Webscarper With Python | Books.toscrape.com |
| Source: | https://realpython.com/beautiful-soup-web-scraper-python/ | http://books.toscrape.com/index.html |
| Reason: | Wanted to learn the basics of webscraping | Want to practice webscraping on static html website |


**Challenges of web scraping:**

Variety: every website is different, while you can encounter general structures that repeat themselves, website is unique and will need personal treatment of you want to extract relevant info

Durability: websites constantly change, first time you run your script it might work flawlessly but if you run it again a while later you might get a stack of tracebacks

-scrapers generally require constant maintenance

-you can set up continuous integration to run scarping tests periodically to ensure that your main script doesn’t break without your knowledge 

Continuous integration: practice of frequently building and testing each change done to your code automatically and as early as possible 

-API’s (application programming interfaces) allow you to access websites data in a predefined manner

* API structures don’t change as frequently but CAN still be changed, it is usually more permanent an is a more reliable source if the site’s data 
* HOW TO GATHER INFO USING API’s
  
</br>

# How to webscrape:

### Step 1: Inspect your data source

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

**Inspect the Site Using Developer Tools**

-developer tools can help you understand the structure of a website

-can use developer tools on chrome 

-developer tools allow you to interactively explore the site's document object model (DOM)

</br>

### Step 2: Scrape HTML Content From a Page

-want to get the sites html code into python script so you can interact with it, need to do this by going through pythons request library

-want to get html code into python script to interact with it 

-use pip to install requests 

-want to issue an http get request to the given url of site site you want to webscrape 

-retrives html data that the srever sends back and stores that data in a python object

-fetching static site content from the internet 

**Static Websites**

-website I'm webscraping is *static html content*

-when deciphering a block of html code, you can use html formatter to clean it up automatically 

-html of this site uses descriptive class names 

Examples:

	class = "title is-5" contains title of the job posting
	class = "subtitle is-6 company" contains name of the company that offers the position
	class = "location" contains location of job
	
**2 challenging situations you might encounter when scraping websites**

1. Hidden Websites 
	* some pages contain info that's hidden behind login
	* that means you need an account to scrape anything from the page
	* process to make an http request from your python script is different from how you access a page from your browser, just cause you can log in to page from browser doesn't mean you'll be able to scrape it with python scrape 
	* requests library  comes with built in capacity to handle authentication
	* using this technique you can log in to websites when making the http request from python script and then scrape info hidden behind login

2. Dynamic Websites
	* static websites: server sends you an html page that already contains all the page info in the response, you can parse html response and immediately begin to pick out relevant data 
	* dynamic website: server might not send back anyhtml at all, might send back javascript code as a response (doesn't return the same html that you see when viewing page from browser)
	* what happens in browser is not the same as what happens in script
	* browser will execute the js code it recieves from a server and create the dom and html for you locally
	* only way to go from js code to content you need is to execute code just like the browser
	* requests library can't do that but there are other solutions
	* requests-html allows you to render js using syntax similar to syntax in requests and also includes capabilities for parsing the data by using bs under the hood (selenium is also a good library, slimmed down browser that executes the js code for you before passing on the rendered html response to your script)

</br>

### Step 3: Parse HTML Code With Beautiful Soup

-beautiful soup is a python library for parsing structured data 

-allows you to interact with HTML in a similar way to how you interact with a web page using dveloper tools 

-need to install beautiful soup from terminal, then import library into python script to create beautiful soup object

**Find elements by ID**

-in an html webpage, every element can have an ID attribute assigned 

-id attribute makes the element uniquely identifiable on the page, you can begin to parse a page by selecting a specific element by its ID

-bs allows you to find that specific HTML element by its ID

-can use .prettify for easier viewing

**Finding elements by HTML Class name**

-can work with the object you created and select more specific info, to do this, you call .find_all() on your bs object which returns an terable containing all the HTML for the new element you've selected to inspect

-can further skim the html by picking out child elements from the parent element, use .find()

**Extract Text From HTML Elements**

-if you add .text to a bs object, you can return only the text content of the html elements that the object contains 

-it's possible that after running this you will end up with extra whitespace, since we are now working with python strings you can .strip() any of the unwanted whitespace 

-other python string methods can be applied to further clean up the text

**Find elements by class name and text content**

-can filter job listings by using key words

-know that the job titles are kept within h2 elements, to filter for a specific job you can use the string argument, this doesn't always work though because the script will look for that string exactly and will not accept differences of capitalization, whitespaces, and spelling

-need to make the string search more general

**Pass a function to a bs method**

-in addition to strings, you can csometimes pass functions as arguments to bs methods

-bs allows you to use either exact strings or functions as arguments for filtering text in bs objects 

**Identifying error conditions**

-when filtering for one element, it is possible that you will get aan error trying to print the rest of the information, teh code is trying to find each element in python_jobs, but only one of the elements was specified within python_jobs, the parsing library is still looking for the other elements anyways, it returns None because it can't find them, print() then fails when you try to extract the .text attribute from one of the None objects 

-the text needed is nested in the sibling elements of the h2 elements the filter returned, bs helps select sibling, child, and parent elements of each bs object 

**Access parent elements**

-one way to access all the need info is to look at the closest parent element from your specified element when looking at the HTML

-the class that has all the info I want is a third parent class, use elements in python_jobs to fetch great grandparents elements to get all info

-now code has access to all relevant info, due to teh fact that now looping over third parent class elements instead of just h2 title elements 

-using .parent attribute on bs object allows access to DOM structure for addressing elements you need 

**Extract attributes from html elements**

-in order to retrieve html attributes you need to extract the value of the html attruibute instead of discarding it, look at the a tag and retrieve href attribute (in this case) 

-you could then give your code a final makeover and create a command-line interface (CLI) app that scrapes one of the job boards and filters the results by a keyword that you can input on each execution. Your CLI tool could allow you to search for specific types of jobs or jobs in particular locations (will be my next step when learning more about webscraping)

**Conclusion**

-requests library allows you to fetch static html from internet using python 
-can parse html with package called beautiful soup 

-learned how to:
* step through web scraping pipeline from start to finish
* inspect html structure of target site with my browser's developer tools
* decipher data encoded in urls
* download html content with pythons requests library
* parse html with beautiful soup
* build a script that fetches relavent info to me

</br>

### Going to apply these webscraping skills on another static website

Website: http://books.toscrape.com/index.html
 
 	
 






