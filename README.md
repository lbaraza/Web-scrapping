# Web-scrapping

# Web Scraping Project

## Project Overview

In this lab, the objective is to extract information from a given website and write the scraped data into a CSV file. The specific data to be extracted includes the name of programming languages and their average annual salaries.

## Objectives

In this lab, you will perform the following tasks:

1. Extract information from a given website.
2. Write the scraped data into a CSV file.

## Data Source

The data will be scraped from the following URL:

```
https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DA0321EN-SkillsNetwork/labs/datasets/Programming_Languages.html
```

The webpage contains a table with the name of programming languages and their corresponding average annual salaries.

## Tools and Libraries

- **Python**: The primary programming language used for web scraping.
- **Requests**: Used to send HTTP requests to the webpage.
- **BeautifulSoup**: Used to parse HTML content and extract data.
- **Pandas**: Used to manipulate and store the scraped data.
- **CSV**: Format used to save the scraped data.

## Installation

To run this project, you need to have Python installed along with the following libraries:

```bash
pip install requests beautifulsoup4 pandas html5lib
```

## Usage

### Step-by-Step Instructions

1. **Import Required Libraries:**

```python
import requests
from bs4 import BeautifulSoup
import pandas as pd
```

2. **Extract Information from the Website:**

```python
# Define the URL containing the data
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DA0321EN-SkillsNetwork/labs/datasets/Programming_Languages.html"

# Send a GET request to the URL
response = requests.get(url)

# Parse the HTML content of the page
soup = BeautifulSoup(response.content, 'html5lib')

# Find the table in the HTML
table = soup.find('table')

# Initialize empty lists to store the scraped data
languages = []
salaries = []

# Loop through the table rows and extract the data
for row in table.tbody.find_all('tr'):
    cols = row.find_all('td')
    languages.append(cols[1].text.strip())
    salaries.append(cols[2].text.strip())

# Create a DataFrame to store the data
data = pd.DataFrame({
    'Programming Language': languages,
    'Average Annual Salary': salaries
})
```

3. **Write the Scraped Data into a CSV File:**

```python
# Save the DataFrame to a CSV file
data.to_csv('programming_languages_salaries.csv', index=False)
```

### Sample Code

Here is the complete code to perform the web scraping and save the data into a CSV file:

```python
import requests
from bs4 import BeautifulSoup
import pandas as pd

# Define the URL containing the data
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DA0321EN-SkillsNetwork/labs/datasets/Programming_Languages.html"

# Send a GET request to the URL
response = requests.get(url)

# Parse the HTML content of the page
soup = BeautifulSoup(response.content, 'html5lib')

# Find the table in the HTML
table = soup.find('table')

# Initialize empty lists to store the scraped data
languages = []
salaries = []

# Loop through the table rows and extract the data
for row in table.tbody.find_all('tr'):
    cols = row.find_all('td')
    languages.append(cols[1].text.strip())
    salaries.append(cols[2].text.strip())

# Create a DataFrame to store the data
data = pd.DataFrame({
    'Programming Language': languages,
    'Average Annual Salary': salaries
})

# Save the DataFrame to a CSV file
data.to_csv('programming_languages_salaries.csv', index=False)

print(data)
```

## Conclusion

This project demonstrates how to scrape data from a webpage and store it in a CSV file using Python. By extracting the names of programming languages and their average annual salaries, we can analyze the data to gain insights into salary trends in the programming industry.

