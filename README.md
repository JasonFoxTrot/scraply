Scraply
========
> Scraply a simple dom scraper to fetch information from any html based website and convert that info to JSON APIs

Overview
=======
```hcl
# this is the configurations file [sample]

# /macros/exec/m1
macro m1 {
    // the url to scrap
    url = "http://webpage.url/here"

    // cache [time to live] in seconds
    ttl = 120

    // code to be executed
    //
    // this is a javascript code
    // you must set your returns in the exports variable
    // there are two global variables available there `document` and $
    // `document` is the DOM object you use to work with the DOM
    // `$` similar to jQuery's `$`, just look at the following comparison
    //
    //  jQuery              :   Scraply
    //  -------------           ---------------
    //  $(..).first()       :   $(..).First()
    //  $(..).html()        :   $(..).Html()
    //  $(..).text()        :   $(..).Text()
    //  $(..).last()        :   $(..).Last()
    //  $(..).find()        :   $(..).Find()
    //  $(..).attr()        :   $(..).Attr()
    //  $(..).children()    :   $(..).Children()
    //  $(..).prev()        :   $(..).Prev()
    //  $(..).next()        :   $(..).Next()
    //  $(..).has()         :   $(..).Has()
    exec = <<JS
        exports = {
            title: $("title").Text()
        }
    JS
}

# aggregators enable you to call multiple macros in just one call!
aggregators {
    # /aggregators/exec/all
    all = ["m1"]
}
```

Why?
====
> I wanted a simple tool that fetches the required information in a simple way from web pages, I'm using it in the following cases:

- Scraping data from currency rates websites
- Scraping product pricing data from e-commerce sites
- Scraping news from news websites
- Scraping search data
- there are more use cases ...

How?
====
- Download the binary that fits your OS from [here](https://github.com/alash3al/scraply/releases)
- Create a configuration file i.e `scraply.hcl`
- Run scrapply `./path/to/downloaded/scrapply --config=./scraply.hcl --listen=:9080`

