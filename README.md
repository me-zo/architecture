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
|   |   ├── repositories    --> uses classes from core to get data from data sources
|   |   |   └── *    --> sample repository
|   |   |       ├── *_repository.dart   --> abstract class
|   |   |       └── *_repository_impl.dart --> its default implementation
|   |   └── Shared_preferences  --> app-wide Notifiers such as settings, and permissions 
|   ├── presentation    --> containes a list of features
|   |   └── home    --> sample feature
|   |   |   ├── domain    
|   |   |   |   ├── models    --> models that communicate data between service and UI
|   |   |   |   └── service    --> uses classes from core and data to present in UI
|   |   |   |       ├── home_service.dart   --> abstract class
|   |   |   |       └── home_service_impl.dart --> its default implementation
|   |   |   └── presentation  
|   |   |       ├── manager    --> a cubit/bloc plus a function_home.dart for further refactoring
|   |   |       ├── screens    --> screens inside a feature (each screen in a single file 
|   |   |       |               unless it containes a common widget from multiple features)
|   |   |       └── home_page.dart    --> a widget that has a route name (basically an 
|   |   |                             enterance to the feature that can be used in other features)
|   |   └── route_generator.dart    --> to navigate between features
│   └── main.dart
├── pubspec.lock
├── pubspec.yaml
```

### Samples
1. [E-Invoice QR Code Reader](https://github.com/Mezo0099/e_invoice_qrcode_reader)
2. [Mezo Movies](https://github.com/Mezo0099/mezo_movies) (in production)

