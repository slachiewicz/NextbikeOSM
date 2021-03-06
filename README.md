#NextbikeOSM
![Demo](https://github.com/javnik36/NextbikeOSM/blob/master/demo.png)

This application parses data about bicycle rentals in nextbike public bike-sharing systems like (for more data [see wikipedia](https://en.wikipedia.org/wiki/Nextbike)) from [their website](http://nextbike.net/maps/nextbike-official.xml) and compares with data from [OpenStreetMap](http://www.openstreetmap.org).

##How to run this?
###Dependencies
* [jinja2](http://jinja.pocoo.org/docs/dev/)

###Guide
You need to have [python 3](https://www.python.org/downloads/) installed.<br>
1. Download all files from this project.<br>
2. Download osm data for your area from for example [overpass-turbo](http://overpass-turbo.eu/). [Here is suitable link](http://overpass-turbo.eu/s/an2); you must only go into your location and click export->download raw data<br>
3. Run the [nextbike_valid.py](https://github.com/javnik36/NextbikeOSM/blob/master/nextbike_valid.py) (see help below)<br>
4. Open html with data :lollipop:

##Technical details
This script tries to match stations by ref, when impossible looks for closest node using Haversine formula. ***Note that sometimes the closest node is not correct node!*** Then checks tags and compares strings in name tag using [GESTALT.C (Ratcliff/Obershelp Pattern Recognition Algorithm)](http://collaboration.cmc.ec.gc.ca/science/rpn/biblio/ddj/Website/articles/DDJ/1988/8807/8807c/8807c.htm) built-in [python difflib module](https://docs.python.org/3.4/library/difflib.html). And of course...it make html from it :)

##Help
Open [nextbike_valid.py](https://github.com/javnik36/NextbikeOSM/blob/master/nextbike_valid.py) in command line using:
```
usage: nextbike_valid.py [-h] [-a NETWORK OSM_PATH HTML_PATH] [-i] [-u] [-f]

optional arguments:
  -h, --help            show this help message and exit
  -a NETWORK OSM_PATH HTML_PATH, --auto NETWORK OSM_PATH HTML_PATH
                        NETWORK is uid or name to be found in
                        nextbike_uids.txt
  -i, --interactive     runs interactive guide
  -u, --update          updates manually nextbike .xml file and .set file wit
                        uids
  -f, --feed            runs feed creation (only with -a!)
```
Atom feed creation uses sqlite database to store history data about given region. It makes sense to run it, when you run it periodically and saves files under the same names.<br>
If you need more help, ask me (email or whatever :smile:)!

####Examples
* Processes data for network *VETURILO Poland*, takes osm data from *export.osm* and saves html to *my.html*
```
python nextbike_valid.py -a "VETURILO Poland" export.osm my.html
```
* Processes data for city *Hamburg*(uids for cities you can find in nextbike_uids.txt in your directory after first program run), takes osm data from *export.osm* and saves html to *my.html*
```
python nextbike_valid.py -a 43 export.osm my.html
```
* Updates data from nextbike server. This data are downloaded by first run automatically, but if you want to keep it updated, this it for you.
```
python nextbike_valid.py -u
```

##More
Note that this application is suitable for quality assurance only. You should make changes in osm base very carefully and I don't take any responsibility!<br>
If you want to help me and add something to code or see any bug just call an issue or make pull request!

[Copyright (c) 2015 javnik36](https://github.com/javnik36/NextbikeOSM/blob/master/LICENCE)
