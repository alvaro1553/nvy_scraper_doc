..
    Auto-build the current doc
    - $ pip install sphinx-autobuild
    - [docs/documentation/]$ sphinx-autobuild ./source ./build/html

.. toctree::
   :maxdepth: 2
   :caption: Contents:

   Complete Example <completeExample>
   List of Steps <stepsReference>

..
    Indices and tables
    ==================

    * :ref:`genindex`
    * :ref:`modindex`
    * :ref:`search`

Invscrap's Getting Started!
===========================
To start using invscrap clone first the repository of the project:

.. code-block:: bash

    git clone --recursive https://github.com/alvaro1552/nvy_scraper.git

Note the --recursive option as the project documentation is hosted in a different repository.

Install the following dependencies: +Python 2.8, `scrapy <https://scrapy.org/>`_,
`selenium <https://www.selenium.dev/>`_

Or alternatively, you can just do::

    pip install -r requirements.txt

Don't forget to select the path to your browser driver in main.py::

    DRIVER_PATH = 'path/to/driver'

Running scrapper
################
Run the following command in the root folder of the project::

    python main.py datasource.json

replacing 'datasource' with the filename of the file containing the scrapping instructions.

Note that the scrapped information is printed directly into the console. There is
no support yet to feed this info into a json file, or to a db. Those features will
be added later once the program is fully functional and has been completely tested.

Build your first datasource.json
#################################
The contents of the json file is a set of instructions that should allow the user
to scrape the contents of any website without modifying the source code of the program.

Complete list of examples of datasource.json files can be found in::

   /dataSources

Each file consists of an unique js object, whose keys' meaning and options can be found below.

REMEMBER: json does not support comments, which are only included in snippets below for clarification.

Key: "metada"
***************
The metada key is not used by the scrapper in any way. It is only intended to
keep the list of scrapping instructions organised. Its usage is recommended
but not mandatory.

.. code-block:: js

    "metadata": {
        "baseURL": "https://example.com/", /*website to scrap*/
        "author": "firstname lastname",    /*author of the file*/
        "date": "dd/mm/yyyy"               /*date of creation of json file*/
    }

Key: "start"
************
The start key must contain a list of 'Starting Points'. Each entry within the list
is composed of 'startUrl' + 'step'. The step is the action to be taken by the
algorithm after reaching the startUrl.

.. code-block:: js

    "start": [
        ["https://example.com/path/to/target1", "parseTarget"],
        ["https://example.com/path/to/target2", "parseTarget"],
    ],

In the example above, each URL corresponds to the url of a **Target**, which is just a
name used to refer to the page URL containing the **Data Points** or info to be scrapped.

Each **step** defined within "start" must have another key within the json file
indicating the *options for that step*. Keep reading...

Key: "optParseTarget"
*********************
Options for the **parseTarget** step.

Note that all of the 'parseTarget' steps within 'start' will use the same options.
No support yet for different options for different targets.

.. code-block:: js

    "optParseTarget": {
        "dataPoints": {
            "title": "//h1/text()",   /* XPATH selector */
            "contents": "//p//text()" /* XPATH selector */
        }
    },

Note that the name of the key follows the pattern: **opt** + **StepNameInCamelCase**.

This way, after reaching the "StartURL" given above, the program will scrap the
data specified within the **datapoint** in the *optParseTarget* key.

Complete Example
****************

The example below fetches the datapoints 'title' and 'data' from both of the articles
defined in "start"

.. code-block:: js

    /* futureInese.json */
    {
        "metadata": {
            "baseURL": "https://future.inese.es/",
            "author": "Alvaro Garcia",
            "date": "30/07/2020"
        },
        "start": [
            ["https://future.inese.es/nace-el-barcelona-insurhub-como-punto-encuentro-entre-startups-mutualidades-e-inversores/", "parseTarget"],
            ["https://future.inese.es/lisa-y-hiscox-lanzan-un-ciberseguro-que-incorpora-el-concepto-insurance-in-a-box/", "parseTarget"]
        ],
        "optParseTarget": {
            "dataPoints": {
                "title": "//*[contains(@id,\"td-outer-wrap\")]//*[contains(@class,\"entry-title\")]//text()",
                "date": "//meta[contains(@property,\"published_time\")]/@content",
                "contents": "//*[contains(@class,\"td-post-content\")]/descendant::*[self::p or self::h2]//text()"
            }
        }
    }

SEE: :doc:`Complete Example Explained <completeExample>` for a more advanced example of how to set up a datasource.json file
