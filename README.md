# How find my location in vue2-google-map

For geolocation

```
<gmap-map :center="{lat:currentLocation.lat, lng:currentLocation.lng}" 
:zoom="17" 
:options="{disableDefaultUI:true}"
>
```
```
  data() {
    return {
      currentLocation : { lat : 0, lng : 0},
      searchAddressInput: ''
    }
  }
```
```
mounted : function() {
    this.geolocation();
 }
```
```
methods: {
    geolocation : function() {
      navigator.geolocation.getCurrentPosition((position) => {
        this.currentLocation = {
          lat: position.coords.latitude,
          lng: position.coords.longitude
        };
      });
    }
}
```
You can after add easily a DIV in your ui, hover the gmaps, to launch your geoloc method
```
  <div class="geolocation" v-on:click="geolocation()">
      <img src="../../static/images/geolocation.png" />
    </div>
    ```
For search your location, same things. Add an input hover your google map

    <div class="search">
      <input type="text" v-model="searchAddressInput" v-on:change="searchLocation()"></input>
    </div>
and the following methods:

searchLocation: function() {
      var geocoder = new google.maps.Geocoder();
      geocoder.geocode({'address': this.searchAddressInput}, (results, status) => {
        if (status === 'OK') {
          this.currentLocation.lat = results[0].geometry.location.lat();
          this.currentLocation.lng = results[0].geometry.location.lng();
        }
      });
    }
