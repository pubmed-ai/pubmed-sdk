# pubmed-sdk
python SDK for searching PubMed 

# pubmed_sdk

[![PyPI version](https://badge.fury.io/py/pubmed_sdk.svg)](https://badge.fury.io/py/pubmed_sdk)
![Python 3.6](https://img.shields.io/badge/python-3.6-blue.svg)
![Python 3.7](https://img.shields.io/badge/python-3.7-blue.svg)
![Python 3.8](https://img.shields.io/badge/python-3.8-blue.svg)
![Python 3.9](https://img.shields.io/badge/python-3.9-blue.svg)
![Build Status](https://travis-ci.org/yourusername/pubmed_sdk.svg?branch=master)

Pubmed_SDK is a Python client library for searching PubMed using the NCBI E-Utilities.

- [Examples](#examples)
- [About Pubmed_sdk](#about)
- [Usage](#usage)


## About Pubmed_sdk

Pubmed_SDK is a Python SDK that facilitates searching PubMed and retrieving article details using the NCBI E-Utilities. It abstracts the process of making HTTP requests to the E-Utilities API and parsing the XML responses, making it easier to focus on the data itself.

## Installation

```terminal
pip install pubmed_sdk
```

## Usage

### Search PubMed
You can search PubMed by creating a `PubMed` object and calling the `search` method with your search term:

```python
from pubmed_sdk import PubMed

pubmed = PubMed()
results = pubmed.search('COVID-19')
```


The `search` method supports the following parameters:

* **term**: The search term.
* **db**: The database to search (default is 'pubmed').
* **retmax**: The maximum number of results to return (default is 20).
* **usehistory**: Whether to use the NCBI history feature (default is 'y').


### Fetch Article Details
After searching, you can fetch the details of the articles using the fetch_details method:

```python
id_list = results['id_list']    # ['33725716', '33725717']
details = pubmed.fetch_details(id_list).get('PubmedArticle')
```

This method accepts a list of IDs and returns a list of dictionaries containing the details of each article.

Here's an example of how to iterate through the results and print some information about each article:

```python
for detail in details:
    article = detail['MedlineCitation']['Article']
    print(article['ArticleTitle'])
    print(article['Abstract']['AbstractText'], '\n\n')
```