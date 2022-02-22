# RFC

- Start date: 2022/02/20
- Members: @Mike-droid , @ferdsng
- RFC PR:

## Summary

Using the Geocoding Service from Google Maps

## Basic Example

When, for instance, you’re looking for a place using Google Maps. You type the address on the search bar and the result gives you the coordinates of the place you’re looking for.

## Motivation

Since the final user is going to search for places to stay, the expected input in the search bar would be an address of the place or the name of the hotel. This service helps the user showing suggestions when typing so it’s easier to find the place that the user is looking for.

Also, this is the most familiarized behavior of the search address bar when a person looks up for a place.

Last but not least, we think we can trust Google to help us in the obtaining of coordinates of addresses and places in the world.

## ****Detailed design****

You can find the documentation of this geocoding service [in this link.](https://developers.google.com/maps/documentation/javascript/geocoding#Geocoding)

The next is extracted from the documentation:

### **Geocoding Requests**

Accessing the Geocoding service is asynchronous, since the Google Maps API needs to make a call to an external server. For that reason, you need to pass a *callback* method to execute upon completion of the request. This callback method processes the result(s). Note that the geocoder may return more than one result.

You access the Google Maps API geocoding service within your code via the `google.maps.Geocoder` constructor object. The `Geocoder.geocode()` method initiates a request to the geocoding service, passing it a `GeocoderRequest` object literal containing the input terms and a callback method to execute upon receipt of the response.

The `GeocoderRequest` object literal contains the following fields:

```JSON
{
 address: string,
 location: LatLng,
 placeId: string,
 bounds: LatLngBounds,
 componentRestrictions: GeocoderComponentRestrictions,
 region: string
}
```

**Required parameters:** You must supply one, and only one, of the following fields:

- `address` — The address which you want to geocode.
- **or** `location` — The `LatLng` (or `LatLngLiteral`) for which you wish to obtain the closest, human-readable address. The geocoder performs a *reverse geocode*. See [Reverse Geocoding](https://developers.google.com/maps/documentation/javascript/geocoding#ReverseGeocoding) for more information.
- **or** `placeId` — The place ID of the place for which you wish to obtain the closest, human-readable address. See more about [retrieving an address for a place ID](https://developers.google.com/maps/documentation/javascript/geocoding#place-id).

### **Geocoding Responses**

The Geocoding service requires a callback method to execute upon retrieval of the geocoder's results. This callback should pass two parameters to hold the `results` and a `status` code, in that order.

### Geocoding Results

The `GeocoderResult` object represents a single geocoding result. A geocode request may return multiple result objects:

```JSON
results[]: {
 types[]: string,
 formatted_address: string,
 address_components[]: {
   short_name: string,
   long_name: string,
   postcode_localities[]: string,
   types[]: string
 },
 partial_match: boolean,
 place_id: string,
 postcode_localities[]: string,
 geometry: {
   location: LatLng,
   location_type: GeocoderLocationType
   viewport: LatLngBounds,
   bounds: LatLngBounds
 }
}
```

`geometry` contains the following information:

- `location` contains the geocoded latitude,longitude value. Note that we return this location as a `LatLng` object, not as a formatted string.

## ****Drawbacks****

In order to use this service, Google offers $200USD monthly as a credit.

Each time we make a request for an address or location, a part of that $200USD is reduced.

We have around a maximum of 40,000 request calls each month so that we won’t run out or money.

## ****Alternatives****

There are other services or API’s that can help us do geocoding, we’ve listed them below:

- [HERE Geocoder REST API](https://developer.here.com/documentation/geocoding-search-api/dev_guide/index.html)
- [Nominatim](https://nominatim.org/release-docs/develop/api/Overview/)
- [GeoNames](http://www.geonames.org/export/web-services.html)
- [Mapbox Geocoding API](https://docs.mapbox.com/api/search/geocoding/)
- [ArcGIS World Geocoding Service](https://developers.arcgis.com/rest/geocode/api-reference/overview-world-geocoding-service.htm)
- [Bing Maps Locations API](https://docs.microsoft.com/en-us/bingmaps/rest-services/locations/)
- [OpenCage](https://opencagedata.com/)
- [Carto](https://carto.com/geocoding/)

## ****Adoption strategy****

We believe that we can create 1 Google Account exclusively for the purpose of this project, and all the members could have access to this account. Then we share the credentials only among these members.

This new account could be something like: ‘geocode-team-c9-platzimaster@gmail.com’.

## ****Unresolved questions****

What if we exceed the monthly requests for the addresses?
