# React Native IBM Push Sample
This is a React-Native Sample Application for demonstrating usage of IBM Push Notifications.

Checkout this link to know more:
[JSONStore - IBM Mobile Foundation Developer Center](http://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/application-development/jsonstore/)

## Setting up the Sample
1. Get into the project directory:
> cd JSONStoreReactNative
2. Install the project dependencies:
> npm install

## Running the Sample
For android: 
> react-native run-android 
For iOS:
> react-native run-ios

## Understanding the Sample
##### Creating a collection:
To create a collection, we use the JSONStoreCollection constructor. We must specify the name of the Collection.
> var collection = new JSONStoreCollection('people');

##### Opening a collection:
Just creating a collection won’t let you interact with it. One must open that JSONStoreCollection to start manipulating it.

For this purpose we use openCollections API of WLJSONStore class. It accepts an array of name of collections to be opened.

Optionally, you can also pass Initialization Options to openCollections API, to open a collection with configuration like [Synchronization](http://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/application-development/jsonstore/reactnative/syncData/). 
- Without InitOptions:
```
var collection = new JSONStoreCollection('people');
WLJSONStore.openCollections(['people'])
.then(res => {
  // success
}).catch(err => {
	// failure
});
```
- With InitOptions:
```
var collection = new JSONStoreCollection('people');
var options = new JSONStoreInitOptions();
options.setSyncOptions(
	JSONStoreSyncPolicy.SYNC_UPSTREAM, 	"JSONStoreCloudantSync"
);
WLJSONStore.openCollections(['people'], options)
.then(res => {
  // success
}).catch(err => {
	// failure
});
```

##### Adding a JSONStore Document:
You can use addData API of JSONStoreCollection class to add data to the collection. It accepts both, a single JSON and array of JSON as a parameter.
```
var data = {"name": "John Doe", "age": 25};
collection.addData(data)
.then(res => {
	// success          
}).catch(err => {
	// failure
});
```

##### Finding Documents:
JSONStoreCollection provides you with a rich set of APIs to find your documents. To find all the documents in a collection use findAllDocuments API. For more info about querying your data check [this](http://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/application-development/jsonstore/reactnative/queryData/)	
```
collection.findAllDocuments().then(data => {
 	// success
}).catch(err => {
 	// failure
});
```

##### Clearing a Collection:
Clearing a collection means to remove all the contained documents	in a JSONStore collection. Remember, the Collection still exist, just that it will be empty now.
```
collection.clearCollection().then(res => {
 	// success
}).catch(err => {
 	// failure
});
```
