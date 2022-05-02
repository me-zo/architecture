# Application Architecture
The architecture that I follow my applications is based on two completely different architectures 
1. The Onion Architecture similar to the open source .NET application [nopcommerce](https://docs.nopcommerce.com/en/developer/tutorials/architecture-of-nopCommerce.html) 
2. The [Clean Architecture Course](https://resocoder.com/2019/08/27/flutter-tdd-clean-architecture-course-1-explanation-project-structure/)  which is based on [This Blog](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html) by Uncle Bob and is made by [Reso Coder](https://resocoder.com/) 

Now these two architectures are similar in one aspect which is that they both aim to accomplish a Loosely Coupled Testable Code, and I am all about that.

## Project Structure

```
├── lib
|   ├── app
│   │   ├── app_theme
│   │   │   ├── styles
|   |   |   └── themes.dart
|   |   └── localization
|   |   |   ├── resources
|   |   |   └── resources.dart
│   │   └── app.dart
|   ├── core    --> this layer containes classes that can be used throughout the app
|   |   ├── common
|   |   |   ├── models
|   |   |   └── widgets
|   |   ├── dependency_registrar
|   |   |   ├── feature_dependencies
|   |   |   └── dependencies.dart
|   |   ├── failures
|   |   |   ├── failures.dart
|   |   |   └── failure_handler.dart
|   |   ├── fixtures
|   |   ├── helpers
|   |   └── network
|   ├── data 
|   |   ├── entities    --> models to communicate with databases grouped by relevance
|   |   ├── dtos    --> models to communicate with APIs grouped by relevance
|   |   ├── repositories    --> uses classes from core to get data from data sources
|   |   |   └── *    --> sample repository
|   |   |       ├── *_repository.dart   --> abstract class
|   |   |       └── *_repository_impl.dart --> its default implementation
|   |   └── Shared_preferences  --> app-wide Notifiers such as settings, and permissions 
|   ├── features    --> containes a list of features
|   |   └── home    --> sample feature
|   |   |   ├── domain    
|   |   |   |   ├── models    --> models that communicate data between service and UI
|   |   |   |   └── service    --> uses classes from core and data to present in UI
|   |   |   |       ├── home_service.dart   --> abstract class
|   |   |   |       └── home_service_impl.dart --> its default implementation
|   |   |   └── presentation  
|   |   |       ├── manager    --> a cubit/bloc/provider plus a function_home.dart for further refactoring
|   |   |       ├── screens    --> screens inside a feature (each screen in a single file unless it containes a common widget from multiple features)
|   |   |       └── home_page.dart    --> a widget that has a route name (basically an enterance to the feature that can be used in other features)
|   |   └── route_generator.dart    --> to navigate between features
│   └── main.dart
├── pubspec.lock
├── pubspec.yaml
```
## The Dependency Rule
following [The Blog by Uncle Bob](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html) 

> The concentric circles represent different areas of software. In general, the further in you go, the higher level the software becomes. The outer circles are mechanisms. The inner circles are policies.<br/>The overriding rule that makes this architecture work is The Dependency Rule. This rule says that _**source code dependencies can only point inwards**_. Nothing in an inner circle can know anything at all about something in an outer circle. In particular, the name of something declared in an outer circle must not be mentioned by the code in the an inner circle. That includes, functions, classes. variables, or any other named software entity.<br/>By the same token, data formats used in an outer circle should not be used by an inner circle, especially if those formats are generate by a framework in an outer circle. We don’t want anything in an outer circle to impact the inner circles.


## The Core Layer

As noted above in the Project Structure this layer can be accessed by the entire application and here are few examples of this:
1. An HTTP Client that handles http calls => used in data layer 
2. A Common helper that uses regex expressions to validate Strings => used in presentation layer 

## The Data Layer

Following the Project Structure this layer is reponsible for dealing with data sources such as Local/Remote Databases, and APIs through using classes from the core layer only and example of that:
Lets say [Here](https://github.com/Mezo0099/e_invoice_qrcode_reader/blob/master/lib/data/repositories/invoice/invoice_repository.dart) we are getting data from a local database and as you can see we are returning an entity so when this method is used we have to fill or map it to a model object in order to pass it through the Domain to the presentation layer.  

## The Features Layer

This is the outmost layer in the application it is a combination of the domain and the presentation layers which leads me to the feature based development side of the application.

### Feature Based Development
Noted in the [Clean Architecture Course](https://resocoder.com/2019/08/27/flutter-tdd-clean-architecture-course-1-explanation-project-structure/) Provided By [Reso Coder](https://resocoder.com/) feature based development allows us to have an application that is **Open To Expansion**. What do I mean by this ? Well as an application grows the development pace usually slows down due to the complication increase in the code so the solution we came up with was to seperate related parts of the application together in features giving us more flexiblity so that we can add more features without having to warry about references and other complication in other words following the [**Open-Closed Principle**](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle) this leads us to a Stable Productivity as denoted by Uncle Bob in [Lesson 3 of Clean Code](https://youtu.be/Qjywrq2gM8o?t=1552)


### Samples
1. [E-Invoice QR Code Reader](https://github.com/Mezo0099/e_invoice_qrcode_reader)
2. [Mezo Movies](https://github.com/Mezo0099/mezo_movies) (in production)

> Note: This architecture should work with any object-oriented Language not just dart i just happened to have an implementation in dart so Please feel free to share with me an Implementation in other languages that should be interesting

