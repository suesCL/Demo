# Neighborhood-Map
NeiborhoodMap is a interactive client-side web app that pulls data from external APIs, and refreshes the page with AJAX requests. The app uses MVC architecture built with HTML and Javascript. It uses both vanila Javasript and jQuery to handle events and perform DOM manipulation. 

## Overview 
User can search for a place from a list of places and explore them on a Google map. User can click the marker to see information about the place. 

**Functionality**:
* A list view displays all places for exploring and user can filter the list by inputting text.
* A google map displays the markers of places filtered and user can open an info window by clicking the marker.
* The info window display information from third party APIs.
* Selecting a place in the list view or clicking on marker will animate the marker by bouncing. 
* When there is an error retrieving information from APIs, a error message will display to users.


## Implementation: 
*  **MVC:** 

Knockout framework is used to handle the list, store markers and filter the list and markers. 

* **Asynchrony and Error Handling:** 
The app uses a nested ajax request including "then" and "done" method to load data from Flickr adn Foursquare asynchronously. It uses "fail" method to send a message saying data cannot be loaded. Then, the initMap method creates a marker based location data.

* **Create a Map:**
The full screen map uses Google Maps API written in map.js file. 
1. Put the value of the Google API key in the index.html file: <script src="http://maps.googleapis.com/maps/api/js?libraries=places&key=[YOUR_API_KEY]"></script>. 
2. Create a initMap method to search for location data using google map's PLacesService API. 
3. Then create a marker for each location and add a click listener on each marker for animation. 
4. Store the content data from third party APIs into marker object. Add another click listener on marker for it to open an info window with content data. 

* **Filter the List and Markers:** The list view and the markers should update accordingly in real time after submitting input field. 
1. Create an observable called inputLocation and bind it to the text input field of the form in html.
2. Filter List : Create a function object "filterLocation" in ViewModel and bind it to form. Inside the function, it filters list items by removing all data in the location observable array and add the marker that matches input location into the obserbala array. The list of item names is the title of each marker. 
3. Filter markers: It passes null value to the setMap method of each marker, then passes map object into setMap method if the marker matches input location. 

* **Animate a Marker:**
1. When list item associated with the marker clicked: Create a function object called openInfo inside ViewModel and bind the function oject onto list item.
2. When the map marker itself is selected: Inside the createMapMarker function, add a click listener on marker. If the return value from marker's getAnimation method is null , pass bounce parameter to setAnimation method of marker, and if the return is not null, then pass null to setAnimation method. 

* **Open an infoWindow:**
Info window will open when either a location is selected from the list view or its map marker is selected directly. Similar to animating map marker, the data binding of openInfo onto list item will open info window clicking on the item. The marker is added a click listener where an infoWindow object will call setContent by passing content data extracted from APIs and then call open method. 


## References
1. Foursquare API : https://api.foursquare.com/v2/venues/explore
2. Googlemap API : http://maps.googleapis.com/maps/api/js
3. Flickr API : https://api.flickr.com/services/rest/?method=flickr.photos.search
