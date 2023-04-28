To find a rider’s best (i.e., lowest generalised cost) public transport alternative, the origin and destination coordinates and the timestamp of their e-scooter trip were used as input to query a trip planner that returns a list of possible itineraries that could be completed solely by foot and/or public transport. Open Trip Planner (OTP) is open-source software project that provides passenger information and transportation network analysis services.

OTP’s underlying network (referred to as a ‘graph’) was constructed by combining an Open Street Map (OSM) network of Gothenburg with Västrafik’s public transport offering. Västtrafik’s routes, schedules, and transport modes were extracted from GTFS files (General Transit Feed Specification) publicly downloadable from [TrafikLab](trafiklab.se/). Since Västtrafik’s regular schedule differs from the summer one, separate GTFS files representing each schedule were used. The [KoDa API](https://www.trafiklab.se/api/trafiklab-apis/koda/) in specific was deployed given the need for specific GTFS time frames. The schedule differentiation is important for a valid comparison to be drawn between an e-scooter trip and a potential public-transport equivalent. I.e., it is aimed to evaluate the public transport options at the time an e-scooter was taken at a reasonably sufficient level of fidelity. Details on the necessary data transformation are given in section below.

Given the large geographical coverage, network data was downloaded as a .osm file for the entirety of Sweden from [Geofabrik.de](http://download.geofabrik.de/) and then clipped using [Osmium](https://docs.osmcode.org/osmium/latest/osmium-extract.html) to a rectangle with bounding coordinates covering only central Gothenburg. The reduced .osm file was then converted to .pbf (the required format for OTP) using [Osmconvert](https://wiki.openstreetmap.org/wiki/Osmconvert).

For the setup and configuration of OTP V2, reference was continually made to the manual published by Open Trip Planner and an instructional case-study in the [city of Manchester](https://www.researchgate.net/publication/321110774_OpenTripPlanner_-_creating_and_querying_your_own_multi-modal_route_planner), as well as to the public [GitHub repository of Cats et. al 2022 case-study](https://github.com/RafalKucharskiPK/query_PT) (comparing ride-hailing and public transport), that this repo is forked from, for Python scripts to batch-query a locally hosted OTP server.


### Input:
 * .csv file with requests 
 * .pbf file with OSM network
 * .zip with GTFS file for the area and date that we query (available from [TrafikLab using KoDa API]([https://www.transit.land/](https://www.trafiklab.se/api/trafiklab-apis/koda/))
 
 ### Output:
 * .csv with trip details (time, transfers, modes, wait and walk times, etc.)  
