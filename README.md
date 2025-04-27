# LinkedIn Jobs Scaper

First, I do not condone scraping LinkedIn data in any way. Anyone who wishes to do so should first read LinkedIn's statement on their <a href="https://www.linkedin.com/help/linkedin/answer/56347/prohibition-of-scraping-software?lang=en" target="_blank">prohibition of scraping software</a>.


But if one were to scrape LinkedIn job postings using selenium webdriver with access to premium user insights, say, then this repository could serve as a collection of tools that one may find useful. I found the selenium webdriver to be key in this process, as LI dynamically renders their pages with JavaScript, so using a tool like BeautifulSoup will grab the initial JS code but not the data that is displayed on the page. Also, note that LinkedIn actively suspends accounts due to 'excessive activity' on a given account.


This module requires python bindings for the selenium webdriver
```bash
$ pip install selenium
```


Here is a quick demo of how one can use the LinkedIn client and scrape tools.

From the command line:
```bash
$ python main.py --username uname --password pword --keyword software --location "san francisco bay area" --sort_by date
```

Or alter settings and run main
```python
from selenium import webdriver
from client import LIClient
from settings import search_keys
import time


# initialize Selenium Web Driver
driver = webdriver.Chrome()
driver.get("https://www.linkedin.com/uas/login")
# initialize LinkedIn web client
liclient = LIClient(driver, **search_keys)
liclient.login()
# wait for page load
time.sleep(3)

liclient.keyword  = "software"
liclient.location = "san francisco bay area"
liclient.navigate_to_jobs_page()
liclient.enter_search_keys()
liclient.customize_search_results()
liclient.navigate_search_results()
liclient.driver_quit()
```

csfxibryfo