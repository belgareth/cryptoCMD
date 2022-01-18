.. -*-restructuredtext-*-

cryptoCMD: cryptoCurrency Market Data (added scripts)
======================================

.. image:: https://img.shields.io/pypi/v/cryptoCMD.svg
    :target: https://pypi.python.org/pypi/cryptoCMD

.. image:: https://travis-ci.org/guptarohit/cryptoCMD.svg?branch=master
    :target: https://travis-ci.org/guptarohit/cryptoCMD
    
.. image:: https://app.fossa.io/api/projects/git%2Bgithub.com%2Fguptarohit%2FcryptoCMD.svg?type=shield
    :target: https://app.fossa.io/projects/git%2Bgithub.com%2Fguptarohit%2FcryptoCMD?ref=badge_shield
    :alt: FOSSA Status

.. image:: https://img.shields.io/pypi/l/cryptoCMD.svg
    :target: https://github.com/guptarohit/cryptoCMD/blob/master/LICENSE

.. image:: https://img.shields.io/pypi/pyversions/cryptoCMD.svg
    :target: https://pypi.python.org/pypi/cryptoCMD

.. image:: https://pepy.tech/badge/cryptoCMD
    :target: https://pepy.tech/project/cryptoCMD
    :alt: Downloads

.. image:: https://img.shields.io/badge/code%20style-black-000000.svg
    :target: https://github.com/ambv/black
    :alt: Code style: black

Cryptocurrency historical market price data scraper written in Python.

Note: This is a fork of the orignal repo. I wanted one that could do Multiples coins and specific dates. So i added on to this. 
-------------------------------------------------------------------------------------------------------------------------------
Installation
------------

::

    $ pip install cryptocmd

to install from the latest source use following command

::

    $ pip install git+git://github.com/guptarohit/cryptoCMD.git


Usage
------
=====================
CoinMarketCap Scraper
=====================

Following methods are available to get data in multiple formats from https://coinmarketcap.com

To get all time historical data of a cryptocurrency
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code:: python

    from cryptocmd import CmcScraper

    # initialise scraper without time interval
    scraper = CmcScraper("XRP")

    # get raw data as list of list
    headers, data = scraper.get_data()

    # get data in a json format
    xrp_json_data = scraper.get_data("json")

    # export the data as csv file, you can also pass optional `name` parameter
    scraper.export("csv", name="xrp_all_time")

    # Pandas dataFrame for the same data
    df = scraper.get_dataframe()

To get data of a cryptocurrency for some days
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code:: python

    from cryptocmd import CmcScraper

    # initialise scraper with time interval
    scraper = CmcScraper("XRP", "15-10-2017", "25-10-2017")

    # get raw data as list of list
    headers, data = scraper.get_data()

    # get data in a json format
    json_data = scraper.get_data("json")

    # export the data to csv
    scraper.export("csv")

    # get dataframe for the data
    df = scraper.get_dataframe()


Following are the columns of the data
"""""""""""""""""""""""""""""""""""""
``Date, Open, High, Low, Close, Volume, Market Cap``

=====================
Additions by Belgareth
=====================

To get all time historical data of a cryptocurrency from a range of dates (From DD-MM-YY to DD-MM-YY)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code:: python
    
    from cryptocmd import CmcScraper

    currency = input("enter currency: ") #eg.. ICX
    date_from = input("enter begining date: ") #(DD-MM-YYYY) or left blank to get all dates
    date_to = input ("enter end date: ")  #(DD-MM-YYYY) or can be left blank to get all dates

    # initialise scraper with time interval

    if date_from and date_to:
        scraper = CmcScraper(currency, date_from, date_to)
    else:
        scraper = CmcScraper(currency)

    # get raw data as list of list
    headers, data = scraper.get_data()

    # get data in a json format
    json_data = scraper.get_data("json")

    # export the data to csv
    scraper.export("csv")

    # get dataframe for the data
    df = scraper.get_dataframe()

Output file is a CSV

To get all time historical data of Multiple cryptocurrency from a range of dates (From DD-MM-YY to DD-MM-YY)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code:: python

    from cryptocmd import CmcScraper
    currency_n = input("enter currency: ") #must be multiple coins eg. BTC ICX (as many coins as you like)
    date_from = input("enter begining date: ") #Can be left blank to get all ranges (DD-MM-YYYY)
    date_to = input ("enter end date: ") #Can be left blank to get all ranges (DD-MM-YYYY)

    for currency in currency_n.split(" "):
        # initialise scraper with time interval

        if date_from and date_to:
            scraper = CmcScraper(currency, date_from, date_to)
        else:
            scraper = CmcScraper(currency)

        headers, data = scraper.get_data()

        # get data in a json format
        json_data = scraper.get_data("json")

        # export the data to csv
        scraper.export("csv")

        # get dataframe for the data
        df = scraper.get_dataframe()
    
Output: Each currency as its own CSV file.


Acknowledgements
----------------
The data is being scrapped from `coinmarketcap <https://coinmarketcap.com>`_ :v: and it's `free <https://coinmarketcap.com/faq/>`_ to use. :tada:


Contributing
------------

Feel free to make a pull request! :octocat:

If you found this useful, I'd appreciate your consideration in the below. ✨☕

.. image:: https://user-images.githubusercontent.com/7895001/52529389-e2da5280-2d16-11e9-924c-4fe3f309c780.png
    :target: https://www.buymeacoffee.com/beldin4000
    :alt: Buy Me A Coffee


License
-------

.. image:: https://app.fossa.io/api/projects/git%2Bgithub.com%2Fguptarohit%2FcryptoCMD.svg?type=large
    :target: https://app.fossa.io/projects/git%2Bgithub.com%2Fguptarohit%2FcryptoCMD?ref=badge_large
    :alt: FOSSA Status
