Invscrap's usage!
=================
To start using invscrap clone first the repository of the project:

.. code-block:: bash

    git clone --recursive https://github.com/alvaro1552/nvy_scraper.git

Note that the --recursive option is used because the current doc is hosted in a
different repository.

Install the following dependencies: +Python 2.8, `scrapy <https://scrapy.org/>`_,
`selenium <https://www.selenium.dev/>`_

Or alternatively, you can just do::

    pip install -r requirements.txt

Don't forget to select the path to your browser driver in main.py::

    DRIVER_PATH = 'path/to/driver'

Running scrapper
################
Run the following command in the root folder of the project::

    python main.py dataSources/datasource.json

replacing 'datasource' with the name of the file containing the scrapping instructions.

Note that the scrapped information is printed directly into the console. There is
no support yet to feed this info into a json file, or to a db. Those features will
be added later once the program is fully functional and has been completely tested.

Format of datasource.json
#########################
The contents of the json file is a set of instructions that should prevent the user from
modifying the source code of the program when scrapping any website.

Complete list of examples::

   /dataSources

See below the meaning and options available for each of the keys of the json file:

First: "metada"
***************
The metada key is not used by the scrapper in any way. It is only intended to
the keep the list of scrapping instructions organised. Its usage is recommended
but not mandatory. The program still works without the metadata entry.

.. highlight:: json

futureInese.json::

    "metadata": {
        "baseURL": "https://example.com/",
        "author": "firstname lastname",
        "date": "dd/mm/yyyy"
    }


Note that

