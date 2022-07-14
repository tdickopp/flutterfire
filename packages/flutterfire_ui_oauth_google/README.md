# FlutterFire UI OAuth Google

[![pub package](https://img.shields.io/pub/v/flutterfire_ui_oauth_google.svg)](https://pub.dev/packages/flutterfire_ui_oauth_google)

Google Sign In for [FlutterFire UI](https://pub.dev/packages/flutterfire_ui)

## Installation

Add dependency

```sh
flutter pub add flutterfire_ui
flutter pub add flutterfire_ui_oauth_google

flutter pub global activate flutterfire_cli
flutterfire configure
```

Enable Google provider on [firebase console](https://console.firebase.google.com/).

## Usage

```dart
import 'package:firebase_core/firebase_core.dart';
import 'package:flutterfire_ui/auth.dart';
import 'package:flutterfire_ui_oauth_google/flutterfire_ui_oauth_google.dart';

void main() {
    WidgetsFlutterBinding.ensureInitialized();
    await Firebase.initializeApp(options: DefaultFirebaseOptions.currentPlatform);

    FlutterFireUIAuth.configureProviders([
        GoogleProvider(clientId: 'clientId'),
    ]);

    runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: SignInScreen(
        actions: [
          AuthStateChangeAction<SignedIn>((context, state) {
            // redirect to other screen
          })
        ],
      ),
    );
  }
}
```

Alternatively you could use the `OAuthProviderButton`

```dart
class MyScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return AuthStateListener<OAuthController>(
      listener: (oldState, newState, controller) {
        if (newState is SignedIn) {
          // navigate to other screen.
        }
      },
      child: OAuthProviderButton(
        provider: GoogleProvider(clientId: 'clientId'),
      ),
    );
  }
}
```

Also there is a standalone version of the `GoogleSignInButton`

```dart
class MyScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GoogleSignInButton(
      clientId: 'clientId',
      loadingIndicator: CircularProgressIndicator(),
      onSignedIn: (UserCredential credential) {
        // perform navigation.
      }
    );
  }
}
```

For issues, please create a new [issue on the repository](https://github.com/FirebaseExtended/flutterfire/issues).

For feature requests, & questions, please participate on the [discussion](https://github.com/FirebaseExtended/flutterfire/discussions/6978) thread.

To contribute a change to this plugin, please review our [contribution guide](https://github.com/FirebaseExtended/flutterfire/blob/master/CONTRIBUTING.md) and open a [pull request](https://github.com/FirebaseExtended/flutterfire/pulls).

Please contribute to the [discussion](https://github.com/FirebaseExtended/flutterfire/discussions/6978) with feedback.