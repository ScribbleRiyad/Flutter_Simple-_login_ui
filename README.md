# Flutter_Simple-_login_ui
# Flutter Login
[![pub package](https://img.shields.io/pub/v/flutter_login?include_prereleases)](https://pub.dartlang.org/packages/flutter_login)
[![Join the chat](https://img.shields.io/discord/817442412313051220)](https://discord.gg/kP7jXHeNtS)
[![Workflow](https://github.com/NearHuscarl/flutter_login/actions/workflows/test.yml/badge.svg?branch=master)](https://github.com/NearHuscarl/flutter_login/actions)

`FlutterLogin` is a ready-made login/signup widget with many animation effects to
demonstrate the capabilities of Flutter

<p align="center">
  <a href='https://i.imgur.com/z3FJSe7.mp4'>
    <img src='https://github.com/NearHuscarl/flutter_login/raw/master/demo/demo.gif' width=320>
  </a>
</p>

## Installation

Follow the install instructions [here](https://pub.dev/packages/flutter_login#-installing-tab-)

## Reference

Property |   Type     | Description
-------- |------------| ---------------
onSignup |   `AuthCallback`     | <sub>Called when the user hit the submit button when in sign up mode. It receives a `SignupData` object, with name, password and, if `additionalSignUpFields` is not null, the additional fields filled in by the user in a `Map<String,String>`</sub>
onConfirmSignup | `ConfirmSignupCallback` | <sub>Called when the user hits the submit button when confirming signup. If not specified, signup will not be confirmed by user.</sub>
onResendCode | `AuthCallback` | <sub>Called when the user hits the resend code button when confirming signup. Only required when onConfirmSignup is provided.</sub>
onLogin |   `AuthCallback`     | <sub>Called when the user hit the submit button when in login mode</sub>
onRecoverPassword |   `RecoverCallback`     | <sub>Called when the user hit the submit button when in recover password mode</sub>
onConfirmRecover | `ConfirmRecoverCallback` | <sub>Called when the user submits confirmation code and sets password in recover password mode. If not specified, a confirmation code will not be used to recover password.</sub>
title |   `String`     | <sub>The large text above the login [Card], usually the app or company name. Leave the string empty or null if you want no title.</sub>
logo |   `ImageProvider or String`     | <sub>The image provider or asset path string for the logo image to be displayed</sub>
messages |   [`LoginMessages`](#LoginMessages)     | <sub>Describes all of the labels, text hints, button texts and other auth descriptions</sub>
theme |   [`LoginTheme`](#LoginTheme)     | <sub>FlutterLogin's theme. If not specified, it will use the default theme as shown in the demo gifs and use the colorsheme in the closest `Theme` widget</sub>
userType |   [`LoginUserType`](#LoginUserType)     | <sub>FlutterLogin's user type. If not specified, it will use the default user type as email</sub>
userValidator |   <sub>`FormFieldValidator<String>`</sub>     | <sub>User field validating logic, add your custom validation here. The default is email validation logic. Expects to return an error message [String] to be display if validation fails or [null] if validation succeeds</sub>
passwordValidator | <sub>`FormFieldValidator<String>`</sub>     | <sub>Same as `userValidator` but for password</sub>
<sub>onSubmitAnimationCompleted</sub> |   `Function`     | <sub>Called after the submit animation's completed. Put your route transition logic here</sub>
logoTag |   `String`     | <sub>`Hero` tag for logo image. If not specified, it will simply fade out when changing route</sub>
titleTag |   `String`     | <sub>`Hero` tag for title text. Need to specify `LoginTheme.beforeHeroFontSize` and `LoginTheme.afterHeroFontSize` if you want different font size before and after hero animation</sub>
showDebugButtons |   `bool`     | <sub>Display the debug buttons to quickly forward/reverse login animations. In release mode, this will be overridden to `false` regardless of the value passed in</sub>
hideForgotPasswordButton |   `bool`     | <sub>Hides the Forgot Password button if set to true</sub>
hideProvidersTitle |   `bool`     | <sub>Hides the title above login providers if set to true. In case the providers List is empty this is uneffective, as the title is hidden anyways. The default is `false`</sub>
disableCustomPageTransformer |   `bool`     | <sub>Disables the custom transition which causes RenderBox was not laid out error. See [#97](https://github.com/NearHuscarl/flutter_login/issues/97) for more info.</sub>
additionalSignUpFields | `Map<String, UserFormField>` | <sub> Used to specify the additional form fields; the form is shown right after signin up. You can provide at most 6 additional fields. </sub>
navigateBackAfterRecovery |   `bool`     | <sub>Navigate back to the login page after successful recovery.</sub>
savedEmail |   `String`     | <sub>Prefilled value for user field (ie. saved from previous session via other means, ie. via SharedPreferences)</sub>
savedPassword |   `String`     | <sub>Prefilled value for password field (ie. saved from previous session via other means, ie. via SharedPreferences). Will set also confirmation password in Auth class</sub>
termsOfService | [`TermOfService`](#TermOfService) | <sub>List of terms of service to be listed during registration. On onSignup callback LoginData contains a list of [`TermOfServiceResult`](#TermOfServiceResult) </sub>
children | [`Widget`] | <sub>List of widgets that can be added to the stack of the login screen. Can be used to show custom banners or logos. </sub>
scrollable |   `bool`     | <sub>When set to true, the login card becomes scrollable instead of resizing when needed.

*NOTE:* It is recommended that the child widget of the `Hero` widget should be the
same in both places. For title's hero animation use the
`LoginThemeHelper.loginTextStyle` in the next screen to get the style of the
exact text widget in the login screen. `LoginThemeHelper` can be accessed by adding
this line

```dart
import 'package:flutter_login/theme.dart';
```

### LoginMessages

Property |   Type     | Description
-------- |------------| ---------------
userHint | `String` | Hint text of the user field [TextField] (Note: user field can be name, email or phone. For more info check: [`LoginUserType`](#LoginUserType))
passwordHint | `String` | Hint text of the password [TextField]
confirmPasswordHint | `String` | Hint text of the confirm password [TextField]
forgotPasswordButton | `String` | Forgot password button's label
loginButton | `String` | Login button's label
signupButton | `String` | Signup button's label
recoverPasswordButton | `String` | Recover password button's label
recoverPasswordIntro | `String` | Intro in password recovery form
recoverPasswordDescription | `String` | Description in password recovery form, shown when the onConfirmRecover callback is not provided
recoverCodePasswordDescription | `String` | Description in password recovery form, shown when the onConfirmRecover callback is provided
goBackButton | `String` | Go back button's label. Go back button is used to go back to to login/signup form from the recover password form
confirmPasswordError | `String` | The error message to show when the confirm password not match with the original password
recoverPasswordSuccess | `String` | The success message to show after submitting recover password
confirmSignupIntro | `String` | The intro text for the confirm signup card
confirmationCodeHint | `String` | Hint text of the confirmation code [TextField]
confirmationCodeValidationError | `String` | The error message to show if confirmation code is empty
resendCodeButton | `String` | Resend code button's label
resendCodeSuccess | `String` | The success message to show after resending a confirmation code
confirmSignupButton | `String` | Confirm signup button's label
confirmSignupSuccess | `String` | The success message to show after confirming signup
confirmRecoverIntro | `String` | The intro text for the confirm recover password card
recoveryCodeHint | `String` | Hint text of the recovery code [TextField]
recoveryCodeValidationError | `String` | The error message to show if recovery code is empty
setPasswordButton | `String` | Set password button's label for password recovery
confirmRecoverSuccess | `String` | The success message to show after confirming recovered password
flushbarTitleError | `String` | The Flushbar title on errors
flushbarTitleSuccess | `String` | The Flushbar title on successes
providersTitle | `String` | A string shown above the login Providers, defaults to `or login with`

### LoginTheme

Property |   Type     | Description
-------- |------------| ---------------
primaryColor | `Color` | The background color of major parts of the widget like the login screen and buttons
accentColor | `Color` | The secondary color, used for title text color, loading icon, etc. Should be contrast with the [primaryColor]
errorColor | `Color` | The color to use for [TextField] input validation errors
cardTheme | `CardTheme` | The colors and styles used to render auth [Card]
inputTheme | `InputDecorationTheme` | Defines the appearance of all [TextField]s
buttonTheme | `LoginButtonTheme` | A theme for customizing the shape, elevation, and color of the submit button
titleStyle | `TextStyle` | Text style for the big title
bodyStyle | `TextStyle` | Text style for small text like the recover password description
textFieldStyle | `TextStyle` | Text style for [TextField] input text
buttonStyle | `TextStyle` | Text style for button text
beforeHeroFontSize | `double` | Defines the font size of the title in the login screen (before the hero transition)
afterHeroFontSize | `double` | Defines the font size of the title in the screen after the login screen (after the hero transition)
pageColorLight | `Color` | The optional light background color of login screen; if provided, used for light gradient instead of primaryColor
pageColorDark | `Color` | The optional dark background color of login screen; if provided, used for dark gradient instead of primaryColor
footerBottomPadding | `double` | The footer bottom Padding; defaults to 0 if not provided.
switchAuthTextColor | `Color` | The optional color for the switch authentication text, if nothing is specified [primaryColor] is used.
logoWidth | `double` | Width of the logo where 1 is the full width of the login card. ; defaults to 0.75 if not provided.
primaryColorAsInputLabel | `bool` | Set to true if you want to use the primary color for input labels. Defaults to false.


### LoginUserType
Enum     |   Description |
-------- |---------------|
EMAIL | The User Field will be set to be email
NAME  | The User Field will be set to be username
PHONE  | The User Field will be set to be phone

[LoginUserType] will change how the user field [TextField] behaves. Autofills and Keyboard Type will be adjusted automatically for the type of user that you pass.

### UserFormField
Property |   Type     | Description |
-------- |------------| ------------| 
keyName  | `String` | The identifier of the fields, it will be the key in the returned map. Please ensure this is unique, otherwise an Error will be thrown
displayName | `String` | The name of the field displayed on the form. Defaults to `keyName` if not given
defaultValue | `String` | The default value of the field, if given the field will be pre-filled in with this
fieldValidator | `FormFieldValidator<String>` | A function to validate the field. It should return null on success, or a string with the explanation of the error
icon | `Icon?` | The icon shown on the left of the field. Defaults to the user icon when not provided
userType | `LoginUserType` | The LoginUserType of the form. The right keyboard and suggestions will be shown accordingly. Defaults to `LoginUserType.user`


### LoginProvider
Property |   Type     | Description |
-------- |------------| ------------| 
button | `Widget` | Used for Buttons for [LoginProvider] - see example uses [SignInButton] package
icon | `IconData` | Icon that is used for a button for [LoginProvider]
label    | `String`   | The label shown under the provider |
callback | `ProviderAuthCallback` | A Function called when the provider button is pressed. It must return null on success, or a `String` describing the error on failure. |
providerNeedsSignUpCallback | `ProviderNeedsSignUpCallback?` | Optional. Requires that the `additionalSignUpFields` argument is passed to `FlutterLogin`. When given, this callback must return a `Future<bool>`. If it evaluates to `true` the card containing the additional signup fields is shown, right after the evaluation of `callback`. If not given the default behaviour is not to show the signup card.

*NOTE:* Both [button] and [icon] can be added to [LoginProvider], but [button] will take preference over [icon]
______________________________________________________________________________________________
main function
____________________________________________________________________________
import 'package:flutter/material.dart';
import 'package:login_ui/view/login.dart';
import 'package:login_ui/view/signup.dart';

void main() {
  runApp(const MaterialApp(
    debugShowCheckedModeBanner: false,
    home: HomePage(),
  ));
}

class HomePage extends StatelessWidget {
  const HomePage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(
        child: Container(
          // we will give media query height
          // double.infinity make it big as my parent allows
          // while MediaQuery make it big as per the screen

          width: double.infinity,
          height: MediaQuery.of(context).size.height,
          padding: const EdgeInsets.symmetric(horizontal: 30, vertical: 50),
          child: Column(
            // even space distribution
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            crossAxisAlignment: CrossAxisAlignment.center,
            children: <Widget>[
              Column(
                children: <Widget>[
                  const Text(
                    "Welcome",
                    style: TextStyle(
                      fontWeight: FontWeight.bold,
                      fontSize: 30,
                    ),
                  ),
                  const SizedBox(
                    height: 20,
                  ),
                  Text(
                    "Scribble Prodouction Studio",
                    textAlign: TextAlign.center,
                    style: TextStyle(
                      color: Colors.grey[700],
                      fontSize: 15,
                    ),
                  )
                ],
              ),
              Container(
                height: MediaQuery.of(context).size.height / 3,
                decoration: const BoxDecoration(
                    image: DecorationImage(
                        image: AssetImage("assets/welcome.png"))),
              ),
              Column(
                children: <Widget>[
                  // the login button
                  MaterialButton(
                    minWidth: double.infinity,
                    height: 60,
                    onPressed: () {
                      Navigator.push(
                          context,
                          MaterialPageRoute(
                              builder: (context) => const LoginPage()));
                    },
                    // defining the shape
                    shape: RoundedRectangleBorder(
                        side: const BorderSide(color: Colors.black),
                        borderRadius: BorderRadius.circular(50)),
                    child: const Text(
                      "Login",
                      style:
                          TextStyle(fontWeight: FontWeight.w600, fontSize: 18),
                    ),
                  ),
                  // creating the signup button
                  const SizedBox(height: 20),
                  MaterialButton(
                    minWidth: double.infinity,
                    height: 60,
                    onPressed: () {
                      Navigator.push(
                          context,
                          MaterialPageRoute(
                              builder: (context) => const SignupPage()));
                    },
                    color: const Color(0xff0095FF),
                    shape: RoundedRectangleBorder(
                        borderRadius: BorderRadius.circular(50)),
                    child: const Text(
                      "Sign up",
                      style: TextStyle(
                          color: Colors.white,
                          fontWeight: FontWeight.w600,
                          fontSize: 18),
                    ),
                  )
                ],
              )
            ],
          ),
        ),
      ),
    );
  }
}
----------------------------------------------
#SignUp Page
----------------------------------------------
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';

class SignupPage extends StatelessWidget {
  const SignupPage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      resizeToAvoidBottomInset: true,
      backgroundColor: Colors.white,
      appBar: AppBar(
        elevation: 0,
        backgroundColor: Colors.white,
        leading: IconButton(
          onPressed: () {
            Navigator.pop(context);
          },
          icon: const Icon(
            Icons.arrow_back_ios,
            size: 20,
            color: Colors.black,
          ),
        ),
        systemOverlayStyle: SystemUiOverlayStyle.dark,
      ),
      body: SingleChildScrollView(
        child: Container(
          padding: const EdgeInsets.symmetric(horizontal: 40),
          height: MediaQuery.of(context).size.height - 50,
          width: double.infinity,
          child: Column(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
            children: <Widget>[
              Column(
                children: <Widget>[
                  const Text(
                    "Sign up",
                    style: TextStyle(
                      fontSize: 30,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  const SizedBox(
                    height: 20,
                  ),
                  Text(
                    "Create an account, It's free ",
                    style: TextStyle(fontSize: 15, color: Colors.grey[700]),
                  )
                ],
              ),
              Column(
                children: <Widget>[
                  inputFile(label: "Username"),
                  inputFile(label: "Email"),
                  inputFile(label: "Password", obscureText: true),
                  inputFile(label: "Confirm Password ", obscureText: true),
                ],
              ),
              Container(
                padding: const EdgeInsets.only(top: 3, left: 3),
                decoration: BoxDecoration(
                    borderRadius: BorderRadius.circular(50),
                    border: const Border(
                      bottom: BorderSide(color: Colors.black),
                      top: BorderSide(color: Colors.black),
                      left: BorderSide(color: Colors.black),
                      right: BorderSide(color: Colors.black),
                    )),
                child: MaterialButton(
                  minWidth: double.infinity,
                  height: 60,
                  onPressed: () {},
                  color: const Color(0xff0095FF),
                  elevation: 0,
                  shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(50),
                  ),
                  child: const Text(
                    "Sign up",
                    style: TextStyle(
                      fontWeight: FontWeight.w600,
                      fontSize: 18,
                      color: Colors.white,
                    ),
                  ),
                ),
              ),
              Row(
                mainAxisAlignment: MainAxisAlignment.center,
                children: const <Widget>[
                  Text("Already have an account?"),
                  Text(
                    " Login",
                    style: TextStyle(fontWeight: FontWeight.w600, fontSize: 18),
                  )
                ],
              )
            ],
          ),
        ),
      ),
    );
  }
}

// we will be creating a widget for text field
Widget inputFile({label, obscureText = false}) {
  return Column(
    crossAxisAlignment: CrossAxisAlignment.start,
    children: <Widget>[
      Text(
        label,
        style: const TextStyle(
            fontSize: 15, fontWeight: FontWeight.w400, color: Colors.black87),
      ),
      const SizedBox(
        height: 5,
      ),
      TextField(
        obscureText: obscureText,
        decoration: const InputDecoration(
            contentPadding: EdgeInsets.symmetric(vertical: 0, horizontal: 10),
            enabledBorder: OutlineInputBorder(
              borderSide: BorderSide(color: Colors.grey),
            ),
            border:
                OutlineInputBorder(borderSide: BorderSide(color: Colors.grey))),
      ),
      const SizedBox(
        height: 10,
      )
    ],
  );
}
<img src="https://i.ibb.co/QnKd3jF/IMG-20220813-232327.jpg" width="300">
____________________________________________________________________
#login Page 
---------------------------------------------------------------------
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';

class LoginPage extends StatelessWidget {
  const LoginPage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      resizeToAvoidBottomInset: false,
      backgroundColor: Colors.white,
      appBar: AppBar(
        elevation: 0,
        backgroundColor: Colors.white,
        leading: IconButton(
          onPressed: () {
            Navigator.pop(context);
          },
          icon: const Icon(
            Icons.arrow_back_ios,
            size: 20,
            color: Colors.black,
          ),
        ),
        systemOverlayStyle: SystemUiOverlayStyle.dark,
      ),
      body: SizedBox(
        height: MediaQuery.of(context).size.height,
        width: double.infinity,
        child: Column(
          mainAxisAlignment: MainAxisAlignment.spaceBetween,
          children: <Widget>[
            Expanded(
                child: Column(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: <Widget>[
                Column(
                  children: <Widget>[
                    const Text(
                      "Login",
                      style:
                          TextStyle(fontSize: 30, fontWeight: FontWeight.bold),
                    ),
                    const SizedBox(
                      height: 20,
                    ),
                    Text(
                      "Login to your account",
                      style: TextStyle(fontSize: 15, color: Colors.grey[700]),
                    )
                  ],
                ),
                Padding(
                  padding: const EdgeInsets.symmetric(horizontal: 40),
                  child: Column(
                    children: <Widget>[
                      inputFile(label: "Email"),
                      inputFile(label: "Password", obscureText: true)
                    ],
                  ),
                ),
                Padding(
                  padding: const EdgeInsets.symmetric(horizontal: 40),
                  child: Container(
                    padding: const EdgeInsets.only(top: 3, left: 3),
                    decoration: BoxDecoration(
                        borderRadius: BorderRadius.circular(50),
                        border: const Border(
                          bottom: BorderSide(color: Colors.black),
                          top: BorderSide(color: Colors.black),
                          left: BorderSide(color: Colors.black),
                          right: BorderSide(color: Colors.black),
                        )),
                    child: MaterialButton(
                      minWidth: double.infinity,
                      height: 60,
                      onPressed: () {},
                      color: const Color(0xff0095FF),
                      elevation: 0,
                      shape: RoundedRectangleBorder(
                        borderRadius: BorderRadius.circular(50),
                      ),
                      child: const Text(
                        "Login",
                        style: TextStyle(
                          fontWeight: FontWeight.w600,
                          fontSize: 18,
                          color: Colors.white,
                        ),
                      ),
                    ),
                  ),
                ),
                Row(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: const <Widget>[
                    Text("Don't have an account?"),
                    Text(
                      " Sign up",
                      style: TextStyle(
                        fontWeight: FontWeight.w600,
                        fontSize: 18,
                      ),
                    )
                  ],
                ),
                Container(
                  padding: const EdgeInsets.only(top: 100),
                  height: 200,
                  decoration: const BoxDecoration(
                    image: DecorationImage(
                        image: AssetImage("assets/background.png"),
                        fit: BoxFit.fitHeight),
                  ),
                )
              ],
            ))
          ],
        ),
      ),
    );
  }
}

// we will be creating a widget for text field
Widget inputFile({label, obscureText = false}) {
  return Column(
    crossAxisAlignment: CrossAxisAlignment.start,
    children: <Widget>[
      Text(
        label,
        style: const TextStyle(
            fontSize: 15, fontWeight: FontWeight.w400, color: Colors.black87),
      ),
      const SizedBox(
        height: 5,
      ),
      TextField(
        obscureText: obscureText,
        decoration: const InputDecoration(
            contentPadding: EdgeInsets.symmetric(vertical: 0, horizontal: 10),
            enabledBorder: OutlineInputBorder(
              borderSide: BorderSide(color: Colors.grey),
            ),
            border:
                OutlineInputBorder(borderSide: BorderSide(color: Colors.grey))),
      ),
      const SizedBox(
        height: 10,
      )
    ],
  );
}

<img src="https://i.ibb.co/QDnYFLY/IMG-20220813-232347.jpg" width="300">
