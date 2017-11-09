# Neighborhood-Map
NeighborhoodMap is an interactive client-side web app that pulls data from external APIs, and refreshes the page with AJAX requests. The app uses MVC architecture built with knock-out framework, HTML and Javascript. It uses jQuery to handle events.

## Overview 
User can search for a place from a list of places and explore them on a Google map. User can click the marker to see information about the place. 

**Functionality**:
* A list view displays all places shown on map and user can filter the list by inputting text.
* A google map displays the markers of places filtered and user can open an info window by clicking the marker.
* The info window display information from third party APIs.
* Selecting a place in the list view or clicking on marker will animate the marker by bouncing. 
* When there is an error retrieving information from APIs, a error message will display to users.


## Implementation: 
*  **MVC:** 

Knockout framework is used to handle the list, store markers and filter the list and markers. The form is binded to function object called filterLocation in ViewModel. The input text box is binded to inputLocation observable. Each list item is binded to locations obsevable array. 

* **Asynchrony and Error Handling:** 
The app uses a nested ajax request to load data from Flickr adn Foursquare asynchronously. Then, use "then" and "done" methods to extract the data and save it as a marker's contentString property. It uses "fail" method to send a message saying data cannot be loaded. 

* **Create a Map:**
The full screen map uses Google Maps API written in map.js file. 
1. Put the value of the Google API key in the index.html file: <script src="http://maps.googleapis.com/maps/api/js?libraries=places&key=[YOUR_API_KEY]"></script>. 
2. Create a initMap method to first search for location data for each location name using google map's PlacesService API. 
3. Create a marker from each location data and add the marker into locations observable array in ViewModel.

* **Filter the List and Markers:** The list view and the markers should update accordingly in real time after submitting input field. 
1. Filter List : Create a function object "filterLocation" in ViewModel where it filters list items by removing all marker data in the location observable array and add the marker that matches input location into the observable array. 

3. Filter markers: Create a function called filterMarkers. It passes null value to the setMap method of each marker, then passes map object into setMap method if the marker matches input location. 

* **Animate a Marker:**
1. Animate when the map marker itself is selected: Inside the createMapMarker function, add a click listener on the marker. Inside the callback function, if the return value from marker's getAnimation method is null , pass bounce parameter to setAnimation method of the marker, and if the return value is not null, then pass null to the setAnimation method. 
2. Animate when list item associated with the marker clicked: Create a function object called openInfo inside ViewModel which contains a method called animateMarker which works the same as above.


* **Open an infoWindow:**
Info window will open when either a location is selected from the list view or its map marker is selected directly. 
1. List Item: Similar to animating map marker, the data binding of openInfo onto list item will open info window when clicking on the item. 
2. Marker: The marker is added a click listener where an infoWindow object will call setContent by passing content data extracted from APIs and then call open method. 


## References
1. Foursquare API : https://api.foursquare.com/v2/venues/explore
2. Googlemap API : http://maps.googleapis.com/maps/api/js
3. Flickr API : https://api.flickr.com/services/rest/?method=flickr.photos.search
