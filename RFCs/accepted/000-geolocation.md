- 2022-02-21
- Members: Melvin Hernández, Juan Manzanero
- RFC PR:

# Sumary

Implement [Google Maps API](https://developers.google.com/maps) to show to the user the locations in the map.

# Basic example

## Integration of Google Maps in the Website

At first, when a user is on the search results page they will see the google map working at the right part of the screen, an then the map automatically find they location and show up the most closest point locations of the service even if they didn’t search anything in the search bar. As well in the **accommodation detail page.**

![Image example, showing Google Maps integration](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc7f87dd8-aba6-4914-9aa9-4c78ccf00730%2FUntitled.png?table=block&id=cff272f6-9936-4e05-afd7-2c3d36057bc6&spaceId=2d01c268-733d-49c1-9053-1ab41589891a&width=960&userId=90b788a9-e5a9-4ef0-b79c-6608966d969a&cache=v2)
“Accommodation detailed page”

![Detailed page](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3d758949-bc1b-467f-b966-85de19eeb9cc%2FUntitled.png?table=block&id=0b492519-329f-4a53-9dc1-23fd4e5cea22&spaceId=2d01c268-733d-49c1-9053-1ab41589891a&width=930&userId=90b788a9-e5a9-4ef0-b79c-6608966d969a&cache=v2)
## Places Service

And how our partners (Anfitriones) can mark by themselves point locations and prices in the map.

![Partners page](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff4873522-3edc-42d8-90c7-ac3ab2f1a688%2FUntitled.png?table=block&id=303a39c4-3ffa-47c1-9732-d383ff7f08c3&spaceId=2d01c268-733d-49c1-9053-1ab41589891a&width=1170&userId=90b788a9-e5a9-4ef0-b79c-6608966d969a&cache=v2)

## Usage

#### Installation

	npm install --save react-google-maps
	
### Code
	
Import the components to your .jsx | .js file.

The component needs some styles to render on the view.

It needs some coordinates to focus a point.

Return the Google Map component inside the LoadSrcipt with your API_KEY.

	import React from 'react';

	import { GoogleMap, LoadScript } from '@react-google-maps/api';
	
	const Map = () => {
		const mapStyles = {
			width: "100%",
			height: "50vh"
		};

	const defaultCenter = { 0, 0 };
	
	return (
		<LoadScript googleMapsApiKey='API_KEY'>
			<GoogleMap
			mapContainerStyle={mapStyles}
			zoom={10}
			center={defaultCenter}
			>
			</GoogleMap>
		</LoadScript>
	);

	};
	
	export default Map;

To implement markers, import the Marker component and add it as a child of GoogleMap component.

It needs coordinates like the map.

	import React from 'react';

	import { GoogleMap, LoadScript, Marker } from '@react-google-maps/api';

	const Map = () => {
		const mapStyles = {
			width: "100%",
			height: "50vh"
		};

		const defaultCenter = { 0, 0 };

		return (
			<LoadScript googleMapsApiKey='API_KEY'>
				<GoogleMap
				mapContainerStyle={mapStyles}
				zoom={10}
				center={defaultCenter}
				>
				<Marker position={defaultCenter} />
				</GoogleMap>
			</LoadScript>
			);
		};

		export default Map;

# Motivation

It’s necessary to the user know at first impression how well work the service with the automatically closest point location system if they didn’t used the search bar, we want that they will feel acquainted with the map in the **results search page** and **accommodation detail page.**

And give to our **partners** the fastest and efficient way to put in the map service their **locations points.**

# Detailed design

Generally we need to do know how to improve 2 services, Google Maps API and the creation of Places Services.(https://developers.google.com/maps/documentation).

## Places Service: How to add point markers and prices over the map

We need to get information from the partner, we do that with the “partners program pages”.

If someone is interest on this, they need to give us information. But we see necessary more pages that are not created in the Figma file design for more information.

[Markers documentation](https://developers.google.com/maps/documentation/javascript/markers#accessible)

### We have this mainly idea:
- The partner will give us the information: address of the property, price per night, services (Wi-fi, kitchen etc.). But not all information is necessary, for example his name, birth day etc. we already have it in User Team DB.
![Partner diagram](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F26df4f64-db7b-43e1-a2f1-4de2bb59f0e0%2FUntitled.png?table=block&id=f8750062-f934-4fb1-ac1f-9bff8ac7b12f&spaceId=2d01c268-733d-49c1-9053-1ab41589891a&width=670&userId=90b788a9-e5a9-4ef0-b79c-6608966d969a&cache=v2)
- All this Data will go to our DB and then we will create automatically new places over the Google Map service.
![Data Base Diagram](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fdb24430d-647c-4213-ba75-05680761b149%2FUntitled.png?table=block&id=b64f9838-ee60-4d53-a94e-0462adc8ba67&spaceId=2d01c268-733d-49c1-9053-1ab41589891a&width=1050&userId=90b788a9-e5a9-4ef0-b79c-6608966d969a&cache=v2)
### More specific explanation:

“This is our idea, we know create a automatically system that create location points sounds easy, but this is our conclusion. Right now I feel that I don’t have the enough experience to have an specific way about how to do this”

-   We need to create an object per users property with data . And taking from the User team DB take some specific data like name, or age.
-   With this objects automatically create the location points. Changing type of variables or as we will see necessary.

### About the prices

- The prices are basically the icon images of point markers but edited. How we do that?
- First of all this is the documentation. 
[https://developers.google.com/maps/documentation/javascript/examples/marker-simple](https://developers.google.com/maps/documentation/javascript/examples/marker-simple)
- And how to edit the point mark to another icon and put content into the icon, this is the documentation. 
[https://stackoverflow.com/questions/40979600/create-a-google-map-marker-containing-price](https://stackoverflow.com/questions/40979600/create-a-google-map-marker-containing-price)

Basically we need to use an image or icon from google. 

```javascript
var image = {
          url: 'OUR-IMAGE-FROM-GOOGLE',
          // This marker is 35 pixels wide by 35 pixels high.
          size: new google.maps.Size(35, 35),
          // The origin for this image is (0, 0).
          origin: new google.maps.Point(0, 0),
          // The anchor for this image is the base of the flagpole at (0, 32).
          anchor: new google.maps.Point(0, 35)
        };
```

And then create a variable that is the price, of course our idea is create an script that can put this price automatically based on the data from the user property. 

```javascript
var clickMarker = new google.maps.Marker({
    position: map.getCenter(),
    map: map,
    draggable: true,
    icon: image,
    label: {
      text: "50€", THIS WOULD BE THE PRICE
      color: 'white',
      fontSize: '15px',
      fontWeight: 'bold'
    }
  });
```

**And this is an example**

![Example icon price image](https://user-images.githubusercontent.com/80364422/155444272-4f0a66d3-baa6-4e97-93b5-3d8bba2c757b.png)

***As we can see, there is an icon and a price***

# Drawbacks

-   The service give us a credit of $200 dll, and per every request the credit down.
-   We don’t know how many experience in react our team members has. So we need to have in mind maybe the possibility of more **carry overs.**
-   We don’t know how many experience in more big APIs like Google Maps our team members has. So we need to have in mind maybe the possibility of more **carry overs.**
-   How partners are going to add in the map their point locations to future reservations by the users. Right now we didn’t see in the Figma design file any plans for it.
- There’s gonna be an impact of time if we didn’t worked before with DB. That’s because there is a part of our proposals that we need to use information from the USERS TEAM DB. 

# Alternatives

We have other services, the problem is the amount of documentation of Google Maps API that we can find online it’s not comparable to other smaller services. So maybe we must choose Google Maps.

-   Mymappi [](https://mymappi.com/)[https://mymappi.com/](https://mymappi.com/)

## Adoption strategy

-   We think Google Maps API implementation will not going to “ break” our team and the C9 cohort will be feel more comfortable because the amount of documentation and tutorials that we can find going to help us a lot to be more efficient results.
- At least our team needs to coordinate with the users team, because they have information in their DB about users and it can be more practical take information from their DB.

# How we teach this
- We have the necessity of read a lot of documentation, and not just that. Make a research about real situations, for example we didn’t find how to change the icon instead of someone of another webpage in the Google’s documentation.

- We decided to call or divide this RFC in 2 subtopics. How integrate Googles Map API in the web page, and How to put prices. So it can be more easy to understand if you are from other team. Of course all the explanation is dense, but with this “subtopics” you quickly understand on what this is focused.

# Unresolved questions

-   We are on charge about how to make locations points, but we don’t see the design page on the figma file, but this is more related in a global way than a problem in the project.

- There is more alternatives about the automatically script to put prices over the map? Until now, yes. We didn’t thought or know a better alternative, but of course this can be changed if it’s too hard. 
