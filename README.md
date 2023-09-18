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
For the second part of this challenge I visited the [Mars Temperature Data Site](https://static.bc-edx.com/data/web/mars_facts/temperature.html)
