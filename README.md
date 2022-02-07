# ConnectToInternet-Lesson8

This is the Real estate on Mars app for lesson 8 of the Udacity: Developing Android Apps with Kotlin Course.
- Connecting with the internet. 
- Using Retrofit
- Using Glide
- Using RecyclerView
- Using enum and filter overflow menu


Introduction:
There’s not much you can do these days without Internet. Almost any Android app you build will need to connect to the Internet at some point. In this lesson, we’ll build an application that connects to an Internet server to retrieve and display data, and eventually allows you to browse real estate on Mars. It will display the real live images from Mars captured from NASA’s Mars rovers. 

You can look to these photos and see generated details about the land and the picture, such as the price and whether the property is available for sale or lease. 

![Ul Controller](https://user-images.githubusercontent.com/43662326/152711166-e9a7d7e1-267a-44b8-b65c-2d5eecad0ee2.png)

For this lesson, we’re going to have a network layer without a database layer.  So the ViewModel will depend on the network layer without repository in between. 

We will be using community developed libraries to build out network layer. This greatly simplifies fetching the data and images. These libraries also help out app conform to some Android best practices, such as loading images on a background thread and caching loaded images, for the asynchronous or parallel sections within out codes, such as talking to our web services layer, we’re going to integrate with co-routines. 

—
RESTful Services

Our Mars Real Estate data is stored on a Web server. To get this data into our apps. We need to understand how to establish a connection and communicate with our server on the Internet. Most Web servers today run Web services using a common stateless Web architecture known as REST, which stands for Representational State Transfer. Web services that offer this architecture are known as RESTful services. 

Requests are made to RESTful Web services in a standardized way via URIs. 

![URI specifies the data you want](https://user-images.githubusercontent.com/43662326/152711192-a597df8f-0b64-46a3-bafe-9aabdc53de75.png)

URI and URL are used interchangeably.

Each Web services requests contains a URI and is transferred to our server using the same HTTP protocol that’s used by Web browsers. 

![Screen Shot 2022-02-03 at 3 38 56 PM](https://user-images.githubusercontent.com/43662326/152711205-a8d17eaf-985d-4128-a7cc-522248d9837e.png)

Here are some most common HTTP request:
![HTTP Protocol](https://user-images.githubusercontent.com/43662326/152711220-b1ca142a-6325-4f74-abb3-5d0ab0c2a0ed.png)

We will get the response in a JSON format. 

Queries in URI
- Queries are like function parameters

This course provides a complete backend service. And we will be using RetroFit Library to communicate with the backend in this lesson. 

——
### Libraries

We are using community build libraries.

Example of the things to look for when using libraries: 
- Only user reasonable API’s/Permissions (networking libraries need to access the Internet, but they probably should not need access to sensitive data such as your user’s contacts or call logs.
- Supports Targeting Latest Android SDK 

——
### How does app architecture look like:

![For Sale](https://user-images.githubusercontent.com/43662326/152711235-1caf9297-d680-498a-a616-066bb3bcf4b9.png)

——
### Connecting to the Internet
The first step in exploring our Mars app is to use the retrofit library to talk to the Mars web service and display the raw JSON response as a string. 

Retrofit Basics:
What Retrofit needs to build our Network API

![Retrofit Basics](https://user-images.githubusercontent.com/43662326/152711251-b8168129-1151-42d3-b552-834978cc095f.png)

Reference link: https://classroom.udacity.com/courses/ud9012/lessons/2be0ed85-721d-4a8d-a484-909b5c98336c/concepts/bef51cd0-1e3b-4350-8b75-c234aa400e14 

Watch the video to understand more about Retrofit.

— 
### Parsing the Json Response
There’s a library called Moshi which parses JSON into Kotlin objects. Retrofit has a converter that works with Moshi. In this step we will use the Moshi library with Retrofit to parse the JSON into useful Mars property Kotlin objects and change the App from displaying the raw Json to displaying the number of Mars properties returned. 

Reference link: https://classroom.udacity.com/courses/ud9012/lessons/2be0ed85-721d-4a8d-a484-909b5c98336c/concepts/80db996b-1f75-400d-814c-cabe8dbc154a

——
### Using Coroutines to make the network call instead of using the Callback

Needed to make the getProperties function in MarsApiService to be suspend and remove the Deferred and .await() extension.
 
Reference link: https://classroom.udacity.com/courses/ud9012/lessons/2be0ed85-721d-4a8d-a484-909b5c98336c/concepts/b36af08e-1bce-48e8-9a31-2e268907d2f0

——

### Display an Internet Image
We will be using a community developed library called Glide to download, buffer, decode, and cache out images, leaving us with a lot less work that if we had to do all of this from scratch. 

Glide basically needs two things: 
1. The URL of the image you want to load and show
2. And ImageView. -> It then displays the loaded image in that ImageView. 

Please view the link to know more about it. 
Reference link: https://classroom.udacity.com/courses/ud9012/lessons/2be0ed85-721d-4a8d-a484-909b5c98336c/concepts/2a8f9f52-a210-4ecd-8fb3-b9909b271138

I will not be using the @BindingAdapter.
 
—

### Display Images in a Grid 
Using the recycler view. I did not use data binding in the adapter file. Look at the PhotoGridAdapter.kt file to see what I did. 

Reference link: https://classroom.udacity.com/courses/ud9012/lessons/2be0ed85-721d-4a8d-a484-909b5c98336c/concepts/cdc3ee7e-ab78-45c3-928c-4592bc14b36c

———

### Error Handling with RecyclerView 

Using enum to see if the items are loading, done or error has occurred. 
Reference link: https://classroom.udacity.com/courses/ud9012/lessons/2be0ed85-721d-4a8d-a484-909b5c98336c/concepts/961a272f-8ba9-44ce-a7ac-ce08264e5d8e

— 

### Parcel and Parcelables
In android, parceling is a way of sharing objects between different processes by flattening an object into a string of data called a parcel. 

A complex object can be stored into the parcel and then recreated from the parcel by implementing the parcel able interface, and they become parcelable objects. 

Each value in the object is written in sequence to the parcel. The object is recreated by reading data from the parcel in the same order it was written to populate data in a new object.  

Using a parcel to share an object between processes, is functionally similar to using XML or JSON to share data between web services and clients. 

A bundle is a parcelable object that contains a key value store of parcel able objects. We use bundles as the argument property in fragments, primarily because of the way the Android lifecycle works. 

Add :Parcelable and @Parcelable tag. 

—
### Going to different fragment and sending data as well using SafeArgs

Reference link: https://classroom.udacity.com/courses/ud9012/lessons/2be0ed85-721d-4a8d-a484-909b5c98336c/concepts/28d1ca47-364e-49b2-8384-fb00393919ab



