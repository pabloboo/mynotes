# mynotes

A new Flutter project.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.

# Basic Application Concepts

Follow [this video](https://www.youtube.com/watch?v=VPvVD8t02U8&ab_channel=freeCodeCamp.org) implementing all the concepts into an app (the video creates a notes app). Test with exercises in [Dartpad](https://dartpad.dev/?id).

# Developer Accounts

Why have a developer account: to register diverse domains for the app ID. Instead of using com.pabloboo, you can have a developer account to use a real one. In the case of Apple, it's necessary to avoid running the app on a simulator.

- Individual account vs. Business account: if you have a personal account, you're responsible for all errors or potential user complaints.

[Apple Developer Account](https://developer.apple.com/programs/enroll/)
[Google Play Developer Account](https://play.google.com/console/u/O/signup)

To create and publish an app on the App Store, you will need a Mac.

# Setup

Flutter is a rich UI framework developed by Google.

Framework: tools to create an app. A framework is a collection of tools.

Dart: language used by Flutter.

[Dartpad](https://dartpad.dev/?id) → website to write Dart/Flutter code directly on the web.

[Flutter Installation Guide](https://docs.flutter.dev/get-started/install?gclid=CjwKCAiAlJKuBhAdEiwAnZb7ld-FaVgOyCB4jXcw0yNr9By6qwTvfGmogP4-ohZ3Ceb_JW2q2o87bhoCJ9wQAvD_BwE&gclsrc=aw.ds)

Run `flutter doctor` to check that the installation has been done correctly.

If you're on a Mac, install Xcode to ensure the application works correctly on iOS.

Install Android Studio and Android SDK: [Installation Guide](https://developer.android.com/studio/install?hl=es-419)

After doing these actions, `flutter doctor` should have Xcode and Android Studio checked.

Recommended code editor: VS Code.

Extensions:

- Error Lens: see the error on the line without clicking.
- Bracket Pair Colorizer: no need to do it manually, it's already installed.
- Install Flutter and Dart extensions.
- bloc
- Tokyo Night: free theme for VS Code.

# Introduction to Dart

```bash
cd projects
flutter create learningdart
code .
```

Ctrl+Shift+P → Flutter: Select Device → connect to a simulator or a mobile device.

Run → Run without debugging → run the application.

final vs const → final allows you to tell Flutter that the value of the variable will not change once assigned. Using final, you can assign a value later.

# Dart Control Statements and Collections

Lists: `const list = ['foo', 'bar', 'baz']`

Sets: `var names = {'foo', 'bar', 'baz'}` → unique list of things.

Maps: key-value information. `var person = {'age': 20, 'name': 'Foo'}; person['name'] = 'Bar';`

# Sound Null-safety in Dart

Null: absence of value.

`String? name` → nullable data type.

Cherry-picking non-null values:

```dart
const String? firstName = null;
const String? middleName = 'Bar';
const String? lastName = 'Baz';
final firstNonNullValue = firstName ?? middleName ?? lastName;
```

Null-aware assignment operator:

```dart
name ??= middleName // if name is null, assign middleName
name ??= lastName
```

Conditional invocation:

```dart
List<String>? names = null;
final numberOfNames = names?.length;
```

# Dart Enumerations, Classes, and Objects

Enumerations and switch statement:

```dart
enum PersonProperties {
 firstName, lastName, age
}
PersonProperties.firstName

enum AnimalType {cat, dog, bunny}
void test(AnimalType animalType) {
	// switch statement
	switch (animalType) {
		case AnimalType.bunny:
			print("Bunny");
			break;
		case AnimalType.cat:
			print("Cat");
			break;
	}
}
void main() {
	test(AnimalType.cat);
}
```

Classes, Constructors, and Methods:

```dart
class Person {
	final String name;
	
	Person(this.name); // constructor

	void printName() { // method
		print(name);
	}

	void run() {
		print('Running');
	}
	
	void breathe() {
		print('Breathe');
	}
}

void main() {
	final person = Person('Foo Bar');
	person.run();
	person.breathe();
}
```

Inheritance and subclassing:

```dart
abstract class LivingThing {
	void breathe() {
		print('Living thing is breathing');
	}
	
	void move() {
		print('Living thing is moving');
	}
}

class Cat extends LivingThing {
}

void test() {
	final fluffers = Cat();
	fluffers.move();
	fluffers.breathe();
}
```

Abstract class is like a normal class but it cannot have instances.

Factory constructor: create a product like a factory does, super fast.

```dart
class Cat {
	final String name;
	Cat(this.name);
	factory Cat.fluffBall() {
		return Cat('Fluff Ball');
	}
}

void main() {
	final fluffBall = Cat.fluffBall();
}
```

Custom operators:

```dart
class Cat {
	final String name;
	Cat(this.name);
	
	@override // every Class extends by default from Object
	// Covariant: tells to forget about what type of object the function is using
	bool operator ==(covariant Cat other) => other.name == name;
	
	@override
	int get hashCode => name.hashCode;
}

void test() {
	final cat1 = Cat('Foo');
	final cat2 = Cat('Foo');
	if (cat1 == cat2) {
		print('They are the same cats');
	}
}
```

# Advanced Dart

Extensions: adding logic to existing classes

```dart
class Cat {
	final String name;
	Cat(this.name);
}

extension Run on Cat {
	void run() {
		print('Cat $name is running');
	}
}

void test() {
	final meow = Cat('Fluffers');
	meow.run();
}
```

Future: data to be returned in the future, in asynchronous programming.

async/await: mechanism for controlling asynchronous flow of data.

await → wait for the execution of the function and continue to the next line.

```dart
// Return int in the future
Future<int> heavyFutureThatMultipliesByTwo(int a) {
	return Future.delayed(Duration(seconds: 3), () => a * 2);
}

void test() async {
	final result = await heavyFutureThatMultipliesByTwo(10);
	print(result);
}
```

Streams: an asynchronous “pipe” of data. A future that sends data and never ends, it continues working.

```dart
Stream<String> getName(){
	return Stream.periodic(const Duration(seconds: 1), (value) {
		return 'Foo';
	});
}

void test() async {
	await for (final value in getName())

 {
		print(value);
	}
	print('Stream finished working');
}
// every second it sends a value and never reaches the last print.
```

Generators: for generating “iterables”, marked with sync* and async*

```dart
// sync generator
Iterable<int> getOneTwoThree() sync* {
	yield 1;
	yield 2;
	yield 3;
}

void test() {
	for (final value in getOneTwoThree()) {
		print(value);
		if (value == 2) { // never calculates the last yield
			break;
		}
	}
}

// async generator
Stream<Iterable<int>> getOneTwoThree() async* {
	yield [1];
	yield [2];
	yield [3];
}
```

Generics: to avoid re-writing similar code.

```dart
class Pair<A, B> {
	final A value1;
	final B value2;
	Pair(this.value1, this.value2);
}

void test() {
	final names = Pair('foo', 20);
}
```

# Project Setup

`flutter create --org xxx.domain appname`

pubspec.yaml: fundamental configuration file used to define and manage project dependencies, as well as to specify important metadata about the application.

[pub.dev](http://pub.dev) → search for dependencies, see who maintains the dependency.

dev_dependencies: packages that are necessary only during the development of the application, but are not required for the application to run in production. These packages can include testing tools, development utilities, code generators, among other useful resources for the development process.

Dependencies needed: firebase_core, firebase_auth, cloud_firestore, firebase_analytics.

Firebase: tool that allows you to go serverless but also have a server. (serverless is a server that you do not have to write, a server that is written by somebody else).

**flutter pub add** → add a dependency (not necessary to do it in the pubspec.yaml).

```bash
flutter pub add firebase_core
flutter pub add firebase_auth
flutter pub add cloud_firestore
flutter pub add firebase_analytics
```

firebase_core → core of firebase that is the server we will use.

firebase_auth → authentication, registration, login, email verification, etc.

cloud_firestore → save user notes on the firebase backend.

firebase_analytics → free analytics when using firebase.

# iOS App Setup (App Identifier, Certificates, and Profiles)

Certificate → Apple knows the app is yours and then certifies it so it can be published on the App Store. The certificate is your developer ID.

Profiles → identify your app.

debug flavor → application that only a few people close to the developer can install to have detailed error monitoring and be able to fix them.

production flavor → similar to the debug flavor but with fewer logs, hidden information, etc.

profiles → having a production or development profile when signing the app with that profile you can configure what the application can and cannot do.

create the certificate → with the certificate, the profile is created → with the profile, the application is signed → the application is sent to apple → apple confirms everything is in order.

App ID → identifier that Apple and you use to know which app it is communicating with at all times.

keychain → from your private key it links with a certificate downloaded from Apple.

Development certificate → needed to be able to run your app while you're developing it on a real iPhone or iPad device.

# Android App Setup

emulator ≠ simulator → emulator is closer to the real functioning of the device.

scrcpy → mirror a real Android device on the screen.

[scrcpy GitHub](https://github.com/Genymobile/scrcpy?tab=readme-ov-file)

Developer options → stay awake (prevent the screen from locking when testing).

# Firebase Backend Setup

[Firebase Overview](https://firebase.flutter.dev/docs/overview/)

Firebase CLI: A CLI to help us interact with Firebase right from our terminal.

[Firebase CLI Installation Guide](https://firebase.google.com/docs/cli?hl=es)

Install Firebase CLI on Windows → run firebase-tools-instant-win.exe → firebase login

Navigate to the project folder.

flutterfire configure → configure our backend.

Test that the application works correctly:

Ctrl+shift+p → select device

terminal → flutter run → y (add multidex support for Android)

# Basic Registration Screen

State: data created.

Stateless and Stateful: stateful widget can keep the state. Stateful is something that you cannot see, that it contains data and that can redraw itself after hot reloading.

Stateless widget does not contain mutable pieces of information.

TIP: type ‘stl’ in VSC to write a stateless widget.

Scaffold: basic building structure of an application that makes it presentable to the user.

In Flutter, almost everything is a widget, either stateful or stateless.

TIP: type ctrl+. in VSC inside a widget to wrap the widget with something.

If you don't have any Firebase user, use an anonymous user.

Column: stack widget one upon the other.

Text editing controller: a proxy you pass to the TextField that writes every time its content so you can use it to store the input value.

TIP: ctrl+. in VSC can be used to delete a widget, transform a stateless widget into a stateful widget, etc.

initState: function that is called when it creates the page.

dispose: function that is called when the page is destroyed.

Hint on text fields: help the user understand what the text fields are for.

In a Future function like FirebaseAuth.instance.createUserWithEmailAndPassword, you have to await it so it executes its function.

Make our password text field secure: `obscureText: true`, `enableSuggestions: false`, `autocorrect: false`

Firebase needs initialization before other calls to firebase.

Error “CONFIGURATION_NOT_FOUND” can be solved by going to [console.firebase.google.com](http://console.firebase.google.com) → project → get started → Email/Password → Enable → Press save.

Widget flutter binding: Enable widget binding before Firebase.initializeApp. [Flutter Architectural Overview](https://docs.flutter.dev/resources/architectural-overview#architectural-layers)

FutureBuilder: It takes a Future, performs a Future, and when this future has succeeded or failed, it gives you a callback that can let you render a widget depending on the result.

Loading screen while waiting: We can use connection states (`snapshot.connectionState`) to determine the state of a Future.

# Login View
Right-click on a Class name → rename symbol (rename a class).

It is not a good practice to write the code in the main.dart class.

TIP: in VSC, if you create a new file with the complete path, it creates the necessary folder. Example “views/login_view.dart”

Handling exceptions example:

```dart
try {
  final userCredential =  await FirebaseAuth.instance.createUserWithEmailAndPassword(
    email: email, 
    password: password
  );
  print(userCredential);
} on FirebaseAuthException catch (e) {
  print('Something bad happened');
  print(e.code);
  if (e.code == 'weak-password') {
    print('Weak password');
  } else if (e.code == 'email-already-in-use') {
    print('Email already in use');
  } else if (e.code == 'invalid-email') {
    print('Invalid email');
  } else {
    print(e.code);
  }
}
```

# Separating App Initialization from Login and Register Screens

This is usually not a good idea, we need to clean this app.

Email verification is important so another person doesn’t use your email address in another apps.

user? → conditionally access a property of the user variable.

# Email verification view

Push a view into a screen: when you have an screen and after pressing a button or something another screen pushes itself on top of another screen.

```dart
Navigator.of(context).push(
  MaterialPageRoute(
    builder: ((context) => const VerifyEmailView()
    )
  )
);
```

BuildContext is a package of information to pass information from one widget to another.

# Link between login and register views

Named routes: https://docs.flutter.dev/cookbook/navigation/named-routes 

Named routes vs anonymous routes: anonymous routes are not as reusable.

A named route has a name asotiated. ‘routes’ property on MaterialApp widget.

Navigator.of(context).pushNamedAndRemoveUntil → remove everything before putting the next screen.

# Logout view

https://api.flutter.dev/flutter/material/AppBar-class.html 

Flutter tells you to avoid print calls in production because it can be stored on the mobile and accessed by other people. Use logs instead.

PopupMenuButton and PopupMenuItem are usually used together.

PopupMenuItem<T>: T means something you define.

import …….. show → only import a specific part of the dependency.

TIP: On Windows Shift + Alt + F → auto indent code.

# Go from login to notes view

pushNamedAndRemoveUntil → pushing is the concept of having a screen and moving phisically another screen on top of it. Remove means that you first remove the other screens and then put the new one on top.

Put a comma at the end of each parameter so when you tap shift+alt+f it indents correctly.

# Cleaning up our routes

Hardcoding is copy-pasting a value everywhere you use it so when you have to change it you have to change the value everywhere you used it. You should create a variable to avoid hardcoding so you only have to change the value in only one place. You don’t want to repeat yourself.

Put route maps in one files as constants.

# Error handling in login view

A better way of popping error dialogs is to use overlays but it is too complicated for this part of the tutorial.

We have to handle other fireExceptions that might occurre and also another FirebaseAuthExceptions that might occurre because maybe on the future there is another FirebaseAuthException.

# Error Handling in Register View, Next Screen After Registration

After registration we need to confirm the user’s mail.

Changes on the main function can’t be reloaded using hot reload, you have to do hot restart.

In this case we can use pushNamed instead of pushNamedAndRemoveUntil because if the user realizes that he has done something wrong on the registration screen he can push the back button without removing so many screens.

We can make the verification email process better by sending the email verification when the user registers instead of on the next screen.

# Confirm identity before going to main UI

On the login button even if the user has not confirmed the email it directly sends it to the notes view. We have to take care of that checking if the user has confirmed its email on the login view.

# Auth Service

We need an auth provider abstract class and AuthService.

We are missing a layer between our code and the firebase dependency. Maybe in the future you will want another form for authentication. Firebase authentication is a provider.

The abstract class is a contract. The concrete provider of that class will be called firebaseAuthProvider. The AuthService class will take the provider and expose its functionalities (the UI talks to the service, the service talks to the provider and the provider talks to Firebase).

We need an auth user. We shouldn’t expose Firebase’s user to the UI.

@immutable → tells that the class can only have immutable fields.

We need a factory initializer that creates an AuthUser from an AuthUser. factory AuthUser fromFirebase(User user) ⇒ AuthUser(user.emailVerified)

We also need an auth provider. auth_provider.dart groups all the providers.

Why is AuthService an AuthProvider? it relays the messages of the given auth provider, but can have more logic.

# Migrating to Auth Service

AuthService.firebase → we need this so we don’t have to instantiate it everywhere.