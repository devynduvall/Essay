
# Surveillance Planes During Protests

The map that is going to be discussed in this project was developed by Peter Aldhous. The maps in the article written by Peter show the plane surveillance by the local, state, federal and military during the civil unrest after George Floyd’s murder in Minneapolis. The country erupted in protest and the government had to act to ensure the health and safety of everyone involved. These maps, made by Peter Aldhous, reflect the level of security that was occurring during this time.
> Surveillance planes are always in action over the nation. To give an overview of the airborne response to the current civil unrest, we mapped flights by local police, state and federal law enforcement, and military planes from 7 p.m. Central Time on Friday, May 29, to 7 p.m. Central Time on Sunday, May 31. The locations of large demonstrations coincided with the most intense aircraft activity. Peter Aldhous

This data was collected soon after the initial protests occurred in the United States. With the ability to distinguish between local, state, federal, and military planes give a greater sense of who was involved and to what extent each branch of the government responded.
All the data that was collected for the creation of these maps was found from the [Federal Aviation Administration](https://www.faa.gov/licenses_certificates/aircraft_certification/aircraft_registry/releasable_aircraft_download/) , or FAA. The FAA keeps flight path records of every aircraft that is flying over US Airspace. While the FAA does not have flight tracking data, [ADS-B Exchange](https://www.adsbexchange.com/)  tracks physical tracks of aircraft without any filtering.
>ADS-B Exchange differs from typical flight tracking sites in two primary ways.
First and foremost ADS-B Exchange does not participate in the filtering performed by most other flight tracking websites which do not share data on military or certain private aircraft. Because ADS-B Exchange does not use any FAA data there are no FAA BARR/LADD, military, or other “filters” preventing you from seeing the the data you collected.  ADS-B Exchange simply does not accept payment or requests to remove aircraft from public tracking!
Second, we are a community. The data we have comes from volunteers, which is supplied back to the community through APIs. Donations are appreciated as they are used to help cover the costs of the infrastructure, archive, and all of the great things you see when using our site.

The first map that is shown is the response to Minneapolis during the time window of 7:00pm May 29 to 7:00pm May 31. This map sets the scene of why this story is important for people interested in government response to civil unrest, aircraft tracking, and the safety of the communities that live within these cities. Minneapolis had a huge presence of surveillance occurring during this first weekend of protests.
![Map of Minneapolis](img/Minneapolis.JPG)

## Map Design
The choice in basemap and thematic colors is very intentional. The reason for this is to draw the viewer into the map in a way that shocks or provokes a feeling. The use of the dramatic contrast between the thematic colors and the dark basemap create a sense of shock and awe. The dark basemap has very little information besides roadways and towns. The reason for this is to show major throughways and places of interest for officials and civilians. Within the map there are three tools that are being used: a search bar, popups, navigation, and zoom levels.

### Search Bar
![Search Bar Example](img/Search.JPG)
The use of a search bar is interesting because it allows the viewer to find cities that are closely related to themselves. The viewers are able to search for any major city within the United States and find information that is related to their communities. This is powerful because instead of having a static map with limited information, the viewer is able to make their own decisions and observations.

### Popups
![Popup Example](img/popup.JPG)
Popups are used to provide more information to the viewer. In the case of this map the popups are used to provide aircraft registration, operator, and model of aircraft. This is important to the understanding of what types of surveillance was occurring and how moveable the aircraft was. A plane has very different characteristic than a helicopter in its ability to land, hover, and move through a city.

### Navigation
![Navigation Example](img/Nav.JPG)
The only way to navigate through the map is by using the zoom level toggle, and dragging with you mouse or finger depending on the device the viewer is using. These are normal ways of interacting with the map.

### Zoom Levels
![Zoom levels Example](img/zoom.JPG)
Zoom levels are an important aspect to map design because depending on the decisions of the author in how detailed they want to make the map, changes the uses of that map. This map has a very high level of detail when it comes to zoom levels. The viewer is able to zoom directly to street level and find the paths that were above their homes or places of work. This level of detail furthers the ability for the viewer to find information about themselves and create their own conclusions.

## Code
### Map Building Code
    mapboxgl.accessToken = 'pk.eyJ1IjoicGFsZGhvdXMtYmYiLCJhIjoiY2pvN25uY24zMHVzMjN3cHVvdW45enlnZCJ9.fkZVsl0uxcHs2Mw2_iHnJA';
      var map = new mapboxgl.Map({
          container: 'map',
          style: 'mapbox://styles/paldhous-bf/ckaymc39y0t9r1in23sheabuw',
          center: [-77.0387238,38.8976763],
          zoom: z,
          minZoom: 5
      });

The way that Peter Aldous is creating the map objects is through the Mapbox API. 
### Popup Code
      map.on('click', function(e) {
        var features = map.queryRenderedFeatures(e.point, {
          layers: ['this-wkd-clzt2d']
        });

        if (!features.length) {
          return;
        }

        var feature = features[0];

        var popup = new mapboxgl.Popup({ offset: [0, -15] })
          .setLngLat(e.lngLat) // this is the position where the cursor clicked
          .setHTML('<b>Registration: </b>' + feature.properties.reg + '<br><b>Operator: </b>' + feature.properties.name_edit +
          '<br><b>Model: </b>' + feature.properties.model)
          .addTo(map);
      });
