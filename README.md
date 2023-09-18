# mars-challenge
---
## Part 1: Scrape Titles and Preview Text from Mars News
For the first part of this challenge I visited the [Mars news](https://static.bc-edx.com/data/web/mars_news/index.html) website and identified the elements that I needed to scrape.  Then I extracted all of the text elements by using soup:
```
text_elements = soup.find_all('div', class_='list_text')
print(text_elements)
```
After that, I extracted the titles and preview text and stored the results in a Python data structure: 
```
for text_element in text_elements:
    content_title = text_element.find('div', class_='content_title').text
    article_teaser_body = text_element.find('div', class_='article_teaser_body').text
    dictionary = {
        "title": content_title,
        "preview": article_teaser_body
    }
    articles.append(dictionary)
```
---
## Part 2: Scrape and Analyze Mars Weather Data
For the second part of this challenge I visited the [Mars Temperature Data Site](https://static.bc-edx.com/data/web/mars_facts/temperature.html) and inspected the page to identify the elements that I needed to scrape.  I created the Beautiful Soup object and used it to scrape the data in the HTML table.  
Step 1: 
```
soup = soup(html, 'html.parser')
```
Step 2: I scrapted the data to create a list of rows using a for loop: 
```
for row in rows:
    table_data = row.find_all('td')
    id = table_data[0].text
    terrestrial_date = table_data[1].text
    sol = table_data[2].text
    ls = table_data[3].text
    month = table_data[4].text
    min_temp = table_data[5].text
    pressure = table_data[6].text
    list.append([id, terrestrial_date, sol, ls, month, min_temp, pressure])
```
Step 3: I Created a Pandas DataFrame by using the list of rows and colum names:
```
df = pd.DataFrame(list, columns=['id', 'terrestrial_date', 'sol', 'ls', 'month', 'min_temp', 'pressure'])
```
Step 4: I prepared the data for analysis by changing the data types:
```
df['id']=df['id'].astype(int)
df['terrestrial_date']=pd.to_datetime(df['terrestrial_date'])
df['sol']=df['sol'].astype(int)
df['ls']=df['ls'].astype(int)
df['month']=df['month'].astype(int)
df['min_temp']=df['min_temp'].astype(float)
df['pressure']=df['pressure'].astype(float)
```
Step 5: I analyzed the data: 
- How many months exist on Mars: 12 months
```
month_count = df['month'].nunique()
month_count
```
- How many Martian days' worth of data are there?: 1,867 days
```
martain_days = df['sol'].nunique()
martain_days
``` 
- Which month, on average, has the lowest temperature? The highest?: The coldest month is month #3 and the warmest month is month #8.
![image](https://github.com/Faith-Hall/mars-challenge/assets/135525815/a68829f5-9fcb-4df3-9282-13f0fa1c0f6c)

- Which month, on average, has the lowest atmospheric pressure? The highest?: The lowest atmospheric pressure is month #6 and the highest is month #9
  ![image](https://github.com/Faith-Hall/mars-challenge/assets/135525815/a9e03ac2-237a-49f3-bbe3-e531f82c343e)

- How many terrestrial days exist in a Martian year? A visual estimate within 25% was made.
![image](https://github.com/Faith-Hall/mars-challenge/assets/135525815/f514d2f3-9b21-459c-ab4b-b6125d82605b)
