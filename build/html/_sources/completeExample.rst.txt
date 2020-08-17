Example of datasource.json
==========================

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
            ["https://future.inese.es/lisa-y-hiscox-lanzan-un-ciberseguro-que-incorpora-el-concepto-insurance-in-a-box/", "parseTarget"],
            ["https://future.inese.es/category/insurtech/page/1", "pagination"],
            ["https://future.inese.es/category/tecnologia/page/1", "pagination"],
            ["https://future.inese.es/category/nuevos-productos/page/1", "pagination"],
            ["https://future.inese.es/category/opinion/page/1", "pagination"],
            ["https://future.inese.es/category/startups/page/1", "pagination"],
            ["https://future.inese.es/category/estrategia/", "clickRepeat"]
        ],
        "optParseTarget": {
            "dataPoints": {
                "title": "//*[contains(@id,\"td-outer-wrap\")]//*[contains(@class,\"entry-title\")]//text()",
                "date": "//meta[contains(@property,\"published_time\")]/@content",
                "contents": "//*[contains(@class,\"td-post-content\")]/descendant::*[self::p or self::h2]//text()"
            }
        },
        "optPagination": {
            "npages": "//*[@class=\"last\"]//text()",
            "targets": "//*[contains(@class,\"td-module-title\")]//a/@href",
            "optParseTarget": "global"
        },
        "optClickRepeat": {
            "button": "//*[contains(@class,\"td_ajax_load_more\")]",
            "targets": "//*[contains(@class,\"td-module-title\")]//a/@href",
            "optParseTarget": "global"
        },
        "global": {
            "optParseTarget": {
                "dataPoints": {
                    "title": "//*[contains(@id,\"td-outer-wrap\")]//*[contains(@class,\"entry-title\")]//text()",
                    "date": "//meta[contains(@property,\"published_time\")]/@content",
                    "contents": "//*[contains(@class,\"td-post-content\")]/descendant::*[self::p or self::h2]//text()"
                }
            }
        }
    }
