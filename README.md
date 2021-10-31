# In App Purchase Example

<img src="https://github.com/DwikiWitmanGeekseat/IAP/blob/master/iap_ios.gif" width="320" height="560">

Demonstrates how to use the In App Purchase (IAP) library on flutter.

## Getting Started on iOS

### Preparation

There's a significant amount of setup required for testing in app purchases
successfully, including registering new app IDs and store entries to use for
testing in App Store Connect. App Store require developers to configure an app with in-app items
for purchase to call their in-app-purchase APIs. IAP library have extensive
documentation on how to do this, and we've also included a high level guide
below.

* [In-App Purchase (App Store)](https://developer.apple.com/in-app-purchase/)
* [Code Lab In-App Purchase Flutter](https://codelabs.developers.google.com/codelabs/flutter-in-app-purchases)
* [StoreKit Testing Example](https://www.appcoda.com/storekit-testing/)


### Develop environment.

- Flutter SDK Version: 2.5.3 (support Apple Silicon M1)
- Xcode Version: 13
- VSCode
- OS Version: MacOS BigSur 11.6

### Set up StoreKit Testing

Set up to use StoreKit Testing. Configured
in the `example/ios/Runner/Configuration.storekit` file (as documented in the article [Setting Up StoreKit Testing in Xcode](https://developer.apple.com/documentation/xcode/setting_up_storekit_testing_in_xcode?language=objc)).
To run the application take the following steps (note that it will only work when running from Xcode):

1. Open the example app with Xcode, `File > Open File` `example/ios/Runner.xcworkspace`;

2. Within Xcode edit the current scheme, `Product > Scheme > Edit Scheme...` (or press `Command + Shift + ,`);

3. Enable StoreKit testing:
  a. Select the `Run` action;
  b. Click `Options` in the action settings;
  c. Select the `Configuration.storekit` for the StoreKit Configuration option.

4. Click the `Close` button to close the scheme editor;

5. Select the device you want to run the example App on;

6. Run the application using `Product > Run` (or hit the run button).


### Set up Product on App Store Connect (Online), StoreKit Testing (Offline), and XCode

Configure an app in App Store Connect. You can do so by following the steps below:

1. Complete this step from [Apple store connect](https://appstoreconnect.apple.com/)
   a. ("Sign a Paid Applications Agreement")
   b. ("App must be approved and published on AppStore first")
   c. ("Configure in-app purchases in StoreKit Testing (offline)") , or ("Configure in-app purchases in App Store Connect (online)")
   
   For a. "Sign a Paid Applications Agreement," you'll setup the paid apps contract under the 'Agreement, Tax, and Banking' section in AppStore Connect.

   For b. "App must be approved and published on AppStore," you must published your app first without IAP, so it can fetch the product ID & do the payment.

   For c. "Configure in-app purchases in App Store Connect,"
   Go to [Apple store connect > Apps > (Choose your apps) > In-App Purchases > Manage](https://appstoreconnect.apple.com/) and 
   Create your products: consumable, upgrade, auto-renewing subscription, or non-renewing subscription.
   Then, check to your code (on lib/main.dart):

   - A consumable with product ID on variable `_kConsumableId`
   - An upgrade with product ID on variable `_kUpgradeId`
   - An auto-renewing subscription with product ID on variable `_kSilverSubscriptionId`
   - An non-renewing subscription with product ID on variable `_kGoldSubscriptionId`

   Replace that String variable by a product ID that you created in App Store Connect. 
   Note: product will not fetched until you complete step a & b.

   For c. "Configure in-app purchases in StoreKit Testing," 
   Follow Set up StoreKit Testing first.
   In XCode, `File > Open File` `iap/ios/Runner.xcworkspace`, open `Configuration.storekit` and create your product (like create product in AppStore Connect).
   
   
2. In XCode, `File > Open File` `iap/ios/Runner.xcworkspace`. 
   Update the Bundle ID to match the Bundle ID of the app created in step #1, to know your Bundle ID app, go to [Apple store connect > Apps > (Choose your apps) > General > App Information](https://appstoreconnect.apple.com/). 
   Set your certificate development on Signing & Capabilities.
   Add IAP capability: on Signing & Capabilities, click +capability, search "In-App Purchase", then click to add.

### Set up Sandbox Tester and Run on Real Device

1. [Create a Sandbox tester
   account (User and Access > Sandbox > Testers) ](https://appstoreconnect.apple.com/access/users) to test the
   in-app purchases with.

2. Use `flutter run` to install the app and test it. Note that you need to test
   it on a real device instead of a simulator. Next click on one of the products
   in the example App, this enables the "SANDBOX ACCOUNT" section in the iOS
   settings. You will now be asked to sign in with your sandbox test account to
   complete the purchase (no worries you won't be charged). If for some reason
   you aren't asked to sign-in or the wrong user is listed, go into the iOS
   settings ("Settings" -> "App Store" -> "SANDBOX ACCOUNT") and update your
   sandbox account from there. This procedure is explained in great detail in
   the [Testing In-App Purchases with Sandbox](https://developer.apple.com/documentation/storekit/in-app_purchase/testing_in-app_purchases_with_sandbox?language=objc) article.


**Important:** signing into any production service (including iTunes!) with the
sandbox test account will permanently invalidate it.

### Integration test
1. Use `flutter drive --driver=test_driver/integration_test.dart --target=integration_test/in_app_purchase_test.dart`

### Interrupted Purchases test
1. To test interrupted purchases, In XCode, `File > Open File` `iap/ios/Runner.xcworkspace` , select the `Configuration.storekit` file in the project navigator. Then go to menu Editor > Enable Interrupted Purchases. By doing so, any purchase you’ll be making from now on will be handled as interrupted, so don’t forget to go to the Editor > Disable Interrupted Purchases menu to switch back to normal later.


