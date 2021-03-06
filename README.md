# webinos vehicle API #

**Service Type**: http://webinos.org/api/vehicle

The main concept of vehicle API is to provide the interface between webinos and your car's CAN bus. This API requires your car manufacturer to support webinos on your car. If you are looking for the universal ODBII experimental implementation, you should be looking in the [IoT sensors API](https://github.com/webinos/webinos-api-iot). 


## Installation ##

To install the vehicle API you will need to npm the node module inside the webinos pzp.

For end users, you can simply open a command prompt in the root of your webinos-pzp and do: 

	npm install https://github.com/webinos/webinos-api-vehicle.git

For developers that want to tweak the API, you should fork this repository and clone your fork inside the node_module of your pzp.

	cd node_modules
	git clone https://github.com/<your GitHub account>/webinos-api-vehicle.git
	cd webinos-api-vehicle
	npm install


## Getting a reference to the service ##

To discover the service you will have to search for the "http://webinos.org/api/vehicle" type. Example:

	var serviceType = "http://webinos.org/api/vehicle";
	webinos.discovery.findServices( new ServiceType(serviceType), 
		{ 
			onFound: serviceFoundFn, 
			onError: handleErrorFn
		}
	);
	function serviceFoundFn(service){
		// Do something with the service
	};
	function handleErrorFn(error){
		// Notify user
		console.log(error.message);
	}

Alternatively you can use the webinos dashboard to allow the user choose the vehicle API to use. Example:
 	
	webinos.dashboard.open({
         module:'explorer',
	     data:{
         	service:[
            	'http://webinos.org/api/vehicle'
         	],
            select:"services"
         }
     }).onAction(function successFn(data){
		  if (data.result.length > 0){
			// User selected some services
		  }
	 });

## Methods ##

Once you have a reference to an instance of a service you can use the following methods:

###get(vehicleDataId, callOnSuccess, callOnError)

Vehicle event types defines the possible vehicle data, which can be retrieved using the get method.

###addEventListener(vehicleDataId, eventHandler, capture)

Vehicle addEventListener method defines the possible vehicle data, which can be retrieved continously.

###removeEventListener(vehicleDataId, eventHandler, capture)

Vehicle removeEventListener method defines the possible vehicle data, which can be removed.

###POI(name, position, address)

The dictionary contains the name of a POI and its address and/or geolocation as a LatLng object

###Address(country, region, county, city, street, streetNumber, premises, additionalInformation, postalCode)

Address method denotes the address of the POI.

###LatLng(lat, lng)

LatLng method contains geolocation as a LatLng object

###requestGuidance(callOnSuccess, callOnError, destinations)

address properties, which can be passed to the navigation system using the requestGuidance() function

###findDestination(callOnSuccess, callOnError, search)

finalDestination method queries the navigation system to retrieve POIs for a given search string.


## Links ##

- [Specifications](http://dev.webinos.org/specifications/api/vehicle.html)
- [Examples](https://github.com/webinos/webinos-api-vehicle/wiki/Examples)

