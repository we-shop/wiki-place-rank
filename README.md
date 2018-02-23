A project for computing the PageRank of Wikipedia pages for places
found in [GeoNames](http://geonames.org/).

A current Wikipedia XML dump is used to generate the
Wikipedia link graph.  The Geonames RDF dump is used for a mapping
between Geonames entities and Wikipedia pages.  The resulting
collection of ranked locations can be used for estimating the
prominence of each interpretation of a toponym.

To run, first download:

- A dump of the [English Language Wikipedia][1]

- The Geonames [RDF Dump][2]

[1]: http://en.wikipedia.org/wiki/Wikipedia:Database_download#English-language_Wikipedia
[2]: http://www.geonames.org/ontology/documentation.html

Install this package:

```go get github.com/weshop/travel-wiki-place-rank/```

Run the following:

    wiki-place-rank all $WIKIDUMP $GEONAMESDUMP geo-ranks.txt
    
Alternatively, you can run each step of the process individually:

1) `wiki-place-rank graph $WIKIDUMP 1-page-graph.gob`

2) `wiki-place-rank pagerank 1-page-graph.gob 2-page-rank.gob`

3) `wiki-place-rank locations $GEONAMESDUMP 3-locations.gob`

4) `wiki-place-rank georank 2-page-rank.gob 3-locations.gob 4-geo-ranks.txt`


# WeShop notes

1. We recommend to download these data dumps:

    - `enwiki-(latest_date)-pages-articles.xml.bz2` using BitTorrent client
    - RDF dump (`http://download.geonames.org/all-geonames-rdf.zip` as of Feb 2018)
  
1. We recommend to process each step individually

2. The output file (`4-geo-ranks.txt`) includes 7 columns:
    * geonameid (integer)
    * geonames_place_name (string)
    * wikipedia_place_name (string)
    * wikipedia_article_slug (string)
    * popularity_score (float) 
    * ordinal_number (integer)
    * alternative names (string, pipe-separated list), based on the wikipedia article aliases (aka Wikipedia:Redirect)