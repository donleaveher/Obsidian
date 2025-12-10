![[Pasted image 20250926040551.png]]
### Rest APIs & HTTP Requests
***HTTP***
- Sending a message contain Json file to webserver, requiring the resources.
***URL(Uniform Resource Locators)***
- Find the resources on the web

| ***HTTP Methods*** | ***Description***                    |
| ------------ | :----------------------------- |
| GET          | Retrieves data from the server |
| POST         | Submits data to server         |
| PUT          | Update date already on server  |
| DELETE       | Deletes data from server       |
***HTTP Using the Requests Library in Python***
```python
import requests

url = "https://www.ibm.com/"
r = requests.get(url)
r.status_code
r.request.headers
# print(r.status_code)
# print(r.request.headers)
r.request.body
header = r.headers
print(header["date"])
url_get = "https://httpbin.org/get"
playload = {"name": "Joseph", "ID": "123"}
r = requests.get(url_get, params=playload)
print(r.url)
print(r.request.body)
r.json()
r.json()["args"]
# * Post request
url_post = "https//httpbin.org/post"
r_post = requests.post(url_post, data=playload)

#* compare Post and get
print(r_post.url) #* http://httpbin.org/post
print(r.url) #* http://httpbin.org/get?name=Joseph&ID=123

print(r_post.request.body) #* name=Joseph&ID=123
print(r.request.body) #* None
```

[***Web Scraping and HTML basic***](https://www.coursera.org/learn/python-for-applied-data-science-ai/ungradedWidget/RjmP5/reading-web-scraping-and-html-basics)
```python
import requests
from bs4 import BeautifulSoup
# Specify the URL of the webpage you want to scrape
url = 'https://en.wikipedia.org/wiki/IBM'
# Send an HTTP GET request to the webpage
response = requests.get(url)
# Store the HTML content in a variable
html_content = response.text
# Create a BeautifulSoup object to parse the HTML
soup = BeautifulSoup(html_content, 'html.parser')
# Display a snippet of the HTML content
print(html_content[:500])

html = '****'
soup = BeautifulSoup(html, 'html5lib')
tag_object = soup.title
tag_object = soup.h3
tag_child = tag_object.b
tag_child.parent
tag_child.attrs
tag_child.string

table_row = soup.find_all(name='tr')

for i, row in enumerate(table_row):
    print("row", i)
    cells = row.find_all("td")
    for j, cell in enumerate(cells):
        print(f"column: {j}, cell: {cell}")
```

[***The summary of  APIs and Date Collection***](https://www.coursera.org/learn/python-for-applied-data-science-ai/supplement/0dLP3/module-5-summary-apis-and-data-collection)
