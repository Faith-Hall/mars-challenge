# mars-challenge
---
## Part 1: Scrape Titles and Preview Text from Mars News
For the first part of this challenge I visited the Mars news website and identified the elements that I needed to scrape.  Then I extracted all of the text elements by using soup.
```
text_elements = soup.find_all('div', class_='list_text')
print(text_elements)
```
