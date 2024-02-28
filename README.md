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

# Unit testing our Auth Service

Why do we need unit tests? We need to guard ourselves against unintentional edits.

TDD (Test Driven Development): tests need to always be written before code, not the other way around. Search for resources on TDD in Flutter.

Different types of tests: unit, widget and integration tests.

Unit tests: examples are tests on the AuthProvider class (unit of code).

Widget tests: make sure the UI you create is working as it should. Example: if log in button stays disable until login is correctly.

Integration test: AuthService because you are testing an end to end fuctionality (AuthService calls Provider and Firebase and UI is not involved).

We are not be calling firebase, we are doing mocking (imitating firebaseAuthProvider).

Dev dependencies are not used in the final product, only on development.

We need our test dependencies: flutter pub add test --dev

Why do we use mocks? we need a mock auth provider.

Test groups are for grouping together similar tests.

TDD: write tests → write functionality for that tests → check that the tests pass.

# CRUD local storage

CRUD (Create, Read, Update, Delete).

SQLite: library created in C to store data in a file.

DB Browser: sqlite is what talks to the sqlite files, and db browser is the container where sqlite runs. Free open source program.

We need the path provider to get our app’s documents directory for database storage.

We need the patch package because it has a useful “join” function.

Add dependencies: flutter pub add sqflite, flutter pub add path_provider, flutter pub add path

Triple quotes (’’’ ‘’’) enables you to put any character without the need of scaping it.

# Working with Streams in Notes Service

We need the stream and stream controller to cache data.

Reactive programming: you have some data stored and you perform some operations, the date is updated and you get notified of those updates.

Streams: pipes of data.

Stream controller: interface to your streams.

Stream: evolution of data through time (example: going from an empty list to a list with one element).

# Preparing Notes View to read all notes

FutureBuilder: it subscribes to a Future and when the value of the Future changes it lets you display a widget. It ties your Future logic with your UI logic.

ConnectionState: done is when a Future completes it task. If you are working with a Stream it never ends so you must use ConnectionState.waiting when working with Streams.

NotesService should be a Singleton. A Singleton is a pattern where a class instance is the only one inside the entire application. NotesService should only have one copy on the entire application.

# Preparing to Create New Notes

The cons of using a floating action button is that it may hide some information and also iOS does not use it so, since we are developing a multiplatform application, may not be the best idea.

We can use the appBar to place action buttons (not inside the 3 dots because adding a new note is a key functionality).

We use pushNamed so the user can go back to the list of notes.

# Creating New Notes

Usually in mobile applications you don’t have a save button, all new changes are saved automatically.

# Displaying Notes in Notes View

We have changed the way to create the StreamController so it listens to all changes.

We delete the dispose function so we don’t loose state of the notes doing hot reload.

We provided a ListView for displaying the notes with maximum 1 line of text displayed.

# Deleting Existing Notes in Notes View

Place a delete item next to each note.

“When you do a thing 3 times think about refactoring it” → we are about to create our third dialog → Instead of doing that we create a generic dialog.

Delete dialog: Remember that we already have an error dialog? Can we make this generic? 1st break things and then code so you fix it (delete the error dialog we have).

TIP: Find a file by name using Ctrl+p

typedef DeleteNoteCallback = void Function(DatabaseNote note); → in listView we use that callback to pass the information of deleting a note to the parent widget (notes_view).

# Update Existing Notes

Instead of creating a view similar to the create note view we reuse the create note view.

Rename the name of the file and also rename the name of the widget (right click → rename symbol).

We created a getArgument function to pass arguments from one widget to another and we also changed the Callback name to make it general for every function that needs to use a note parameter.

# Protecting NotesService with Current User

We had to create an extension so we can filter the notes by user id inside a stream.

Now by filtering notes by id only the user who created the note can see them displayed on the notes view.

# Writing Notes to Cloud Firestore

Now the data is only stored on the phone, we have to store them on the cloud.

First we stored the data locally to understand CRUD because Firebase abstracts most of the logic.

https://firebase.flutter.dev/docs/firebase/overview 

We are going to use cloud Firestore to store our notes.

Two important concepts in Firestore are collections and documents. In noSQL there is a looser definition of information.

Productions vs test mode: in test mode, as you are developing your application, you can use your database without having a user authenticated. We already have our authentication implemented so we are going to use production mode directly.

You can specify various rules for your data: https://firebase.google.com/docs/firestore/security/get-started?authuse=0auth-required 

This rules help you secure your database.

[console.firebase.google.com](http://console.firebase.google.com) 

Firestore → europe west → test mode → change rules to: reques.auth ≠ null

Collections: https://firebase.flutter.dev/docs/firestore/usage 

Collections: Start a collections → notes (in this collection you will store the notes, each document in this collection is a note).

Documents: they are stored inside collections. 

Streams of data: Firebase cloud storage gives us streams to work with.

# Migrating to our Firestore Service

In this chapter we had to comment all notesService and refactor de code so now we use the FirestoreDatabase.

# Sharing notes

Share-plus plugin: https://pub.dev/packages/share_plus 

A plugin goes well beyond flutter can deliver, unlike a dependency.

flutter pub add share_plus → clean and rebuild app (flutter clean, flutter pub get, flutter run).

By using that plugin we already have all the functionality we need to share a note.

# Introduction to Bloc

Bloc is used to separte the login of the UI from the business logic.

Bloc is a library that allows us to separate our buisness logic from our presentation.

flutter_bloc is a set of flutter specific bloc code that helps us with creating widgets.

Bloc class is the core of the bloc library, you add events to that class and it produces states.

Events → Bloc → states (input → Bloc → states).

BlocProvider: Creates a Bloc instance and provides it to you. [bloclibrary.dev](http://bloclibrary.dev) 

BlocListener: It can react to changes in your Bloc.

BlocBuilder: uses your Bloc state changes to provide you with a widget.

BlocConsumer: combines BlocListener and BlocBuilder.

add dependencies: flutter pub add bloc, flutter_bloc. → flutter clean, flutter pub get, flutter run.

emit() → function that allows you to pass a state out of your Bloc.

Visibility widget: lets you show or not info depending on a variable value.

Send an event from BlocConsumer to a Bloc:

```dart
onPressed: () {
	context.
		read<CounterBloc>()
		.add(IncrementEvent(_controller.text));
}
```

# Converting our Auth Process to Bloc

We need 3 main Bloc components: AuthBlocState, AuthBlocEvent, AuthBloc.

Event→AuthBloc→State

A constant constructor can’t call a non-constant super constractor of ‘AuthState’ → that’s why we have a constant constructor in AuthState, so extended classes can have constant constructors.

In AuthStateLoggedIn we only need the user.

In auth_event.dart we have the inputs to the AuthBloc and in auth_state.dart we have the outputs of AuthBloc.

AuthStateLoading is a generic state that we created to say that we are doing the login, logout, etc. If we didn’t have it we would have to create a state for each async function loading.

emit(…) is to communicate with the outside.

vsc extensions → install bloc extension to be able to wrap widgets with bloc components.

BlocBuilder is like FutureBuilder but using our bloc.

We are using BlocProvider and BlocBuilder in our main.dart file.

Now we are not telling the code to change between screens. main.dart file does this work so we only have to pass the event to AuthBloc without doing the change of screens.

# Handling Auth Bloc Exceptions During Login

With the changes of the previous step now we are not handling auth exceptions.

If you haven’t login correctly the state you are in is logged out, that’s why we have to change auth_state.dart so that AuthStateLoginFailure is removed and optional exception is added to AuthStateLoggedOut so we have less states to manage.

BlocListener: only listens to changes on the state of a bloc. It’s great for side effects such as displaying dialogs while some other operation is ongoing.

# Moving to Bloc for Routing and Dialogs

We are using some direct calls to AuthService (we have to change that to call AuthBloc) and we also are using Navigator.of to change between screens. We should get rid of manual work related to routing and authentication.

Import equatable → flutter pub add equatable

We are using equatable because we need to produce various mutations of the AuthStateLoggedOut.

# Loading Screens

The loading dialog must be transaction based. Loading must user overlays and not dialogs.

Overlays are good for loading screens because they have the ability to place themselves on top of another layers.

Loading screen controller: so that we can change the contents of the loading screen as it is displayed. This controller allows us to dissmiss the loading screen and update the contents of the loading screen.

Loading dialog should handled in just one place in the entire application.

In main.dart we need a BlocConsumer because we need to retrieve something (BlocBuilder) and also listen to the value of isLoading (BlocListener).

# Final Touches Before App Release

We need to clean up the design of the app.

We don’t have a password reset at the moment, this will make it easier to reset their passwords themselves. → add a new authEvent → add a new AuthStateForgotPassword → Declare sendPasswordReset function in auth_provider.dart → Implement the funciton in firebase_auth_provider.dart → implement the function in auth_service.dart → Handle AuthEventForgotPassword in auth_bloc.dart → create new dialog for password reset → create new view for password reset → In main.dart, for AuthStateForgotPassword return ForgotPasswordView() → In login view we have to add a button to go to forgotPasswordView.

In Flutter if you catch an exception with catch(\_) you are really not ignoring it, you are calling the exception ‘_’.

# App Icons and App Name

Splash screen: screen that displays while flutter is loading when opening the app.

https://www.stockio.com/ → find free app icons.

https://www.stockio.com/free-icon/sticky-note-filo-icon

https://appicon.co → generate different icon sizes.

https://pub.dev/packages/flutter_launcher_icons → tool for setting flutter app icons.

flutter pub add flutter_launcher_icons → add dependency.

Create flutter_launcher_icons.yaml → upload icon.png → flutter pub run flutter_launcher_icons:main

flutter clean → flutter pub get → flutter run

App name:

- iOS: info.plist → CFBundleDisplayName → MyNotes
- AndroidManifest.xml → android:label → MyNotes

# Splash Screen

Splash screen: screen that displays while flutter is loading when opening the app.

https://docs.flutter.dev/development/ui/advanced/splash-screen 

We can use our icon to make a splash screen. All we need is a simple design tool like Figma.

Storyboard on iOS → this is only dedicated to the splash screen.

mynotes/ios/Runner. → execute the Runner to open it on xCode on a mac.

If you don’t have a macintosh you will need someone to help you edit this file and send you back the storyboard file.

Open up figma and use the app icon to design a new splash screen using iPhone 13 Pro Max resolution of 1284x2778 (create a rectangle with that dimensions). Give the rectangle a background color, for example, use the tokyo night theme of vsc, search for colors in the readme of the github project. Create a gradiant on the background, put a soft color on the center with a linear gradiant. import appstore.png and put it in the center. Download from Figma in 3x, 2x and 1x flavors (all png).

https://marketplace.visualstudio.com/items?itemName=enkia.tokyo-night 

Open xcode → assets → bring the 3 new images to LaunchImage → Launch Screen → change dimensions to make the splash screen fit the screen.

Now on Android:

https://developer.android.com/guide/topics/ui/splash-screen 

https://stackoverflow.com/questions/28507609/image-resolution-for-mdpi-hdpi-xhdpi-and-xxhdpi/52152009 

https://marketplace.visualstudio.com/items?itemName=enkia.tokyo-night

Use the figma splash screen created for ios but export the desing with the following sizes:

LDPI - 0.75x
MDPI - Original size // means 1.0x here
HDPI - 1.5x
XHDPI - 2.0x
XXHDPI - 3x
XXXHDPI - 4.0x

Then put each one in the corresponding folder in android/app/res/ make sure all of them are called splash.png in their folders.

search for “android:windowBackground”

<item name="android:windowBackground">@mipmap/splash</item>

there are 2  files styles.xml, you have to change the value in the first ocurrence of those two files.

If you get the error:

```powershell
E/AndroidRuntime(23528): FATAL EXCEPTION: wmshell.splashscreen
E/AndroidRuntime(23528): Process: com.android.systemui, PID: 23528
E/AndroidRuntime(23528): java.lang.RuntimeException: Canvas: trying to draw too large(107907360bytes) bitmap.
```

Try changing the figma rectangle size to 1080x1920.

# Sending our iOS app to App Store Connect

We need an .ipa file (contains all the app resources, similar to a .zip but with another extension) to send to Aple but before that we need to prepare App Store Connect.

App Store Connect: your developer portal to releasing iOS and macOS apps. Firebase console for iOS developers.

First you have to create a new app in App Store Connect.

To take the screenshots you can have inside MaterialApp the property debugShowCheckedModeBanner:false so that the debug tag is hidden.

Then provide all the app information.

In XCode make a release build and send it to App Store Connect.

# Releasing our iOS App

TestFlight is used to test the app before submitting it to the App Store.

Install TestFlight for Mac and your iOS decive.

Add your test users to TestFlight.

Add your build to App Store Connect.

Complete App Information.

Publish the app and wait for Apple to review it.

# Fixing Firebase Security Rules and Resubmitting the iOS App

Remove the version from App Store Connect, even if it’s already in review.

Remove your build as well.

Clean our FirebaseDB (users and notes).

https://firebase.google.com/docs/firestore/security/rules-conditions 

[console.firebase.google.com](http://console.firebase.google.com) → Cloud firestore database → rules

```
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
    	allow read, update, delete: if request.auth != null 
      	&& request.auth.uid == resource.data.user_id;
      allow read, write: if request.auth != null;
    }
  }
}
```

Filter the notes before getting the snapshot → notes.where(…).snapshot.

In pubspec.yaml update your version to 1.1.0+1

flutter clean, flutter pub get, flutter run

Make a new build and send to Apple using XCode.

# Releasing our Android App

We need an app bundle.

https://play.google.com/

https://developer.android.com/distribute/console 

https://play.google.com/console/about → create app → complete app info.

Mobile screenshots: open up scrcpy and in terminal: adb exec-out screencap -p > fileX.png

https://www.xda-developers.com/install-adb-windows-macos-linux/ 

https://developer.android.com/tools/releases/platform-tools?hl=es-419 → descargar adb y abrir una terminal dentro de la carpeta descargada.

.\adb.exe

.\adb.exe exec-out screencap -p > homepage.png

In Android Studio create a 7 and 10 inch tablet → select this devices on vsc to open the emulator and do the app screenshots. (Nexus 10 y 7 WSVGA)

[https://docs.flutter.dev/deployment/andorid](https://docs.flutter.dev/deployment/android) 

Create signing key in ~/.android → create [key.properties](http://key.properties) → update build.gradle for signing → flutter clean, flutter pub get, flutter build appbundle.

Upload the appbundle (build/app/outputs/bundle/release/app-release.aab) to production/testing in google play console.