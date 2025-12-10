```python
import yfinance as yf
# DownLoad historical data for a stock
msft = yf.Ticker("MSFT")
msft_data = msft.history(period = "max")
msft_data.head()
```

![[Pasted image 20251005095012.png]]
***Extracting Stock Data Using a Web Scraping***
```python
The package should intsall
!pip install pandas
!pip install requests
!pip install bs4
!pip install html5lib 
!pip install lxml
!pip install plotly
```
```python
import pandas as pd
import requests
from bs4 import BeautifulSoup
import warnings

Ignore all warnings
warnings.filterwarnings("ignore", category = FutureWarning)

Step 1: Sending an HTTP request to the web page
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/netflix_data_webpage.html"

data = requests.get(url).text
print(data)
```

![[Pasted image 20251005100026.png]]
```python
Step 2: Parse the HTML content

soup = beautifulSoup(data, 'html.parser')

As stated above, the web page consists of a table so, we will scrape the content of the HTML web page and convert the table into a data frame.
Create an empty data frame using the pd.DataFrame() function with the following columns:

netflix_data = pd.DataFrame(colums =["Date", "Open", "High", "Low", "Close", "Volume"])

Use find() and find_all() methods of the BeautifulSoup object to locate the table body and table row respectively in the HTML.

for row in soup.find("tbody").find('tr')
	col = row.find_all('td')
	date = col[0].text
	Open = col[1].text
	high = col[2].text
	low = col[3].text
	close = col[4].text
	adj_close = col[5].text
	volume = col[6].text
# Finally we append the data of each row to the table
	netflix_data = pd.concat([netflix_data,pd.DataFrame({"Date":[date], 
	"Open":[Open], "High":[high], "Low":[low], "Close":[close], 
	"Adj Close":[adj_close], "Volume":[volume]})], ignore_index=True)    
```

![[Pasted image 20251005111631.png]]
[GitHub](https://github.com/donleaveher/Python-Project-for-Data-Science)
