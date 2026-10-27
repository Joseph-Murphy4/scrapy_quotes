# scrapy_quotes

A [Scrapy](https://scrapy.org/) spider that collects every quote and its author from
[quotes.toscrape.com](http://quotes.toscrape.com/), a site built for scraping practice.

## Setup

Requires Python and Scrapy. With Pipenv (the Pipfile pins Python 3.9):

```sh
pipenv install
pipenv shell
```

Or with pip:

```sh
pip install scrapy
```

## Usage

Run from the project root (the folder containing `scrapy.cfg`):

```sh
scrapy crawl quotes -O quotes.json   # overwrite quotes.json
scrapy crawl quotes -O quotes.csv    # overwrite quotes.csv
```

`-O` overwrites the output file; use `-o` to append instead. The format is chosen from
the file extension.

## How it works

The spider (`quotes/spiders/quotes_spider.py`):

1. Starts at the home page.
2. For each `div.quote`, yields the author and the quote text, with the curly quote
   marks stripped.
3. Follows the **Next** link until there isn't one. The site has 10 pages, so a full
   crawl yields 100 quotes.

## Output

Each item has two fields:

| Field    | Example                          |
|----------|----------------------------------|
| `author` | `Albert Einstein`                |
| `text`   | `Try not to become a man of success. Rather become a man of value.` |

`quotes.json` and `quotes.csv` in the repo hold the results of a full crawl.

## Project layout

```
scrapy.cfg                     Scrapy project config
quotes/
  settings.py                  Scrapy settings (obeys robots.txt, UTF-8 feed output)
  spiders/quotes_spider.py     The `quotes` spider
  items.py, pipelines.py,
  middlewares.py               Unused scaffolding from `scrapy startproject`
quotes.json, quotes.csv        Sample output
```
