---
nav_title: iOS
page_title: iOS Initial SDK Setup
platform: iOS
page_order: 1
description: "This reference article shows how to integrate the Braze SDK for iOS, using CocoaPods, Carthage, or Swift Package Manager."
---

# iOS Initial SDK Setup

Installing the Braze iOS SDK will provide you with basic analytics functionality (session handling) as well as basic in-app messages. You must further customize your integration for additional channels and features. 

The Braze iOS SDK can be installed or updated using CocoaPods, Carthage, Swift Package Manager, or a manual integration.

- [CocoaPods Integration](#cocoa_pods)
- [Carthage Integration](#carthage_integration)
- [Swift Package Manager Integration](#swift_package_manager)

{% alert important %}
The iOS SDK will add 1MB to 2MB to the app IPA file, in addition to App File, and 30MB for the Framework.
{% endalert %}

After you have integrated using one of the three options above, as well as enabled other SDK Customizations (optional), move on to integrating, enabling, and customizing additional channels and features to fit the needs of your future campaigns.

## CocoaPods Integration {#cocoa_pods}

### Step 1: Install CocoaPods

Installing the iOS SDK via [CocoaPod][1] automates the majority of the installation process for you. Before beginning this process please ensure that you are using [Ruby version 2.0.0][2] or greater. Don't worry, knowledge of Ruby syntax isn't necessary to install this SDK.

Simply run the following command to get started:

```bash
$ sudo gem install cocoapods
```

__Note__: If you are prompted to overwrite the `rake` executable please refer to the [Getting Started Directions on CocoaPods.org][3] for further details.

__Note__: If you have issues regarding CocoaPods, please refer to the [CocoaPods Troubleshooting Guide][6].

### Step 2: Constructing the Podfile

Now that you've installed the CocoaPods Ruby Gem, you're going to need to create a file in your Xcode project directory named `Podfile`.

Add the following line to your Podfile:

```
target 'YourAppTarget' do
  pod 'Appboy-iOS-SDK'
end
```

__Note__: We suggest you version Braze so pod updates automatically grab anything smaller than a minor version update. This looks like 'pod 'Appboy-iOS-SDK' ~> Major.Minor.Build'. If you want to integrate the latest version of Braze SDK automatically even with major changes, you can use `pod 'Appboy-iOS-SDK'` in your Podfile.

> We recommend that integrators import our full SDK as outlined above. However, if you are certain that you are only going to integrate a particular Braze feature then you have the option to import just the desired UI subspec instead of the full SDK.

| Subspec | Details |
| ------- | ------- |
| `pod 'Appboy-iOS-SDK/InAppMessage'` | The `InAppMessage` subspec contains the Braze In-App Message UI and the Core SDK.|
| `pod 'Appboy-iOS-SDK/ContentCards'` | The `ContentCards` subspec contains the Braze Content Card UI and the Core SDK. |
| `pod 'Appboy-iOS-SDK/NewsFeed'` | The `NewsFeed` subspec contains the Braze News Feed UI and the Core SDK. |
| `pod 'Appboy-iOS-SDK/Core'` | The `Core` subspec contains support for analytics, such as custom events and attributes. |
{: .ws-td-nw-1}

### Step 3: Installing the Braze SDK

To install the Braze SDK Cocoapod, navigate to the directory of your Xcode app project within your terminal and run the following command:
```
pod install
```

At this point, you should be able to open the new Xcode project workspace created by CocoaPods.

![New Workspace][5]

### Step 4: Updating your App Delegate

{% tabs %}
{% tab OBJECTIVE-C %}

Add the following line of code to your `AppDelegate.m` file:

```objc
#import "Appboy-iOS-SDK/AppboyKit.h"
```

Within your `AppDelegate.m` file, add the following snippet within your `application:didFinishLaunchingWithOptions` method:

```objc
[Appboy startWithApiKey:@"YOUR-APP-IDENTIFIER-API-KEY"
         inApplication:application
     withLaunchOptions:launchOptions];
```

{% endtab %}
{% tab swift %}

If you are integrating the Braze SDK with CocoaPods or Carthage, add the following line of code to your `AppDelegate.swift` file:

```swift
import Appboy_iOS_SDK
```

For more information about using Objective-C code in Swift projects, please see the [Apple Developer Docs](https://developer.apple.com/library/ios/documentation/swift/conceptual/buildingcocoaapps/MixandMatch.html).

In `AppDelegate.swift`, add following snippet to your `application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool`:

```swift
Appboy.start(withApiKey: "YOUR-APP-IDENTIFIER-API-KEY", in:application, withLaunchOptions:launchOptions)
```

__Note__: Braze's `sharedInstance` singleton will be nil before `startWithApiKey:` is called, as that is a prerequisite to using any Braze functionality.

{% endtab %}
{% endtabs %}

{% alert important %}
Be sure to update `YOUR-APP-IDENTIFIER-API-KEY` with the correct value from your **Settings** page. For more information on where to find your App Identifier API key, check out our [API documentation]({{site.baseurl}}/api/api_key/#the-app-identifier-api-key).
{% endalert %}

{% alert warning %}
Be sure to initialize Braze in your application's main thread. Initializing asynchronously can lead to broken functionality.
{% endalert %}


### Step 5: Specify Your Data Cluster

{% alert note %}
Note that as of December 2019, custom endpoints are no longer given out, if you have a pre-existing custom endpoint, you may continue to use it. For a list of our available endpoints, <a href="{{site.baseurl}}/api/basics/#endpoints">click here</a>.
{% endalert %}

#### Compile-time Endpoint Configuration (Recommended)

If given a pre-existing custom endpoint...
- Starting with Braze iOS SDK v3.0.2, you can set a custom endpoint using the `Info.plist` file. Add the Braze dictionary to your `Info.plist` file. Inside the `Braze` dictionary, add the `Endpoint` string subentry and set the value to your custom endpoint URL's authority (for example, `sdk.iad-01.braze.com`, not `https://sdk.iad-01.braze.com`). Note that prior to Braze iOS SDK v4.0.2, the dictionary key `Appboy` must be used in place of `Braze`.

Your Braze representative should have already advised you of the [correct endpoint]({{site.baseurl}}/user_guide/administrative/access_braze/sdk_endpoints/).

#### Runtime Endpoint Configuration

If given a pre-existing custom endpoint...
- Starting with Braze iOS SDK v3.17.0+, you can override set your endpoint via the `ABKEndpointKey` inside the `appboyOptions` parameter passed to `startWithApiKey:inApplication:withLaunchOptions:withAppboyOptions:`. Set the value to your custom endpoint URL's authority (for example, `sdk.iad-01.braze.com`, not `https://sdk.iad-01.braze.com`).

{% alert important %}
To find out your specific cluster, please ask your Customer Success Manager or reach out to our support team.
{% endalert %}

### SDK Integration Complete

Braze should now be collecting data from your application and your basic integration should be complete. {% if include.platform == 'iOS' %}Please see the following sections in order to enable custom event tracking, push messaging, the news-feed and the complete suite of Braze features.{% endif %}

### Updating the Braze SDK via CocoaPods

To update a Cocoapod simply run the following commands within your project directory:

```
pod update
```

### Customizing Braze On Startup

If you wish to customize Braze on startup, you can instead use the Braze initialization method `startWithApiKey:inApplication:withLaunchOptions:withAppboyOptions` and pass in an optional `NSDictionary` of Braze startup keys.
{% tabs %}
{% tab OBJECTIVE-C %}

In your `AppDelegate.m` file, within your `application:didFinishLaunchingWithOptions` method, add the following Braze method:

```objc
[Appboy startWithApiKey:@"YOUR-APP-IDENTIFER-API-KEY"
          inApplication:application
      withLaunchOptions:launchOptions
      withAppboyOptions:appboyOptions];
```

{% endtab %}
{% tab swift %}

In `AppDelegate.swift`, within your `application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool` method, add the following Braze method:

```swift
Appboy.start(withApiKey: "YOUR-APP-IDENTIFIER-API-KEY",
                 in:application,
                 withLaunchOptions:launchOptions,
                 withAppboyOptions:appboyOptions)
```

where `appboyOptions` is a `Dictionary` of startup configuration values.

{% endtab %}
{% endtabs %}

__Note__: This method would replace the `startWithApiKey:inApplication:withLaunchOptions:` initialization method from above.

This method is called with the following parameters:

- `YOUR-APP-IDENTIFIER-API-KEY` – Your [App Identifier]({{site.baseurl}}/api/api_key/#the-app-identifier-api-key) API Key from the Braze Dashboard.
- `application` – The current app
- `launchOptions` – The options `NSDictionary` that you get from `application:didFinishLaunchingWithOptions:`
- `appboyOptions` – An optional `NSDictionary` with startup configuration values for Braze

See [Appboy.h][4] for a list of Braze startup keys.

### Appboy.sharedInstance() and Swift nullability

Differing somewhat from common practice, the `Appboy.sharedInstance()` singleton is optional. The reason for this is that, as noted above, `sharedInstance` is `nil` before `startWithApiKey:` is called, and there are some non-standard but not-invalid implementations in which a delayed initialization can be used.

If you call `startWithApiKey:` in your `didFinishLaunchingWithOptions:` delegate before any access to Appboy's `sharedInstance` (the standard implementation), you can use optional chaining, like `Appboy.sharedInstance()?.changeUser("testUser")`, to avoid cumbersome checks. This will have parity with an Objective-C implementation that assumed a non-null `sharedInstance`.

## Carthage Integration {#carthage_integration}

Starting from version 3.24.0 of the SDK, you can integrate the Braze SDK using Carthage by including the following in your `Cartfile`:
```
binary "https://raw.githubusercontent.com/Appboy/appboy-ios-sdk/master/appboy_ios_sdk_full.json"
```

You can integrate earlier versions of the SDK by including the following in your `Cartfile`:
```
github "Appboy/Appboy-iOS-SDK" "<BRAZE_IOS_SDK_VERSION>"
```

Make sure to replace `<BRAZE_IOS_SDK_VERSION>` with the latest version of the Braze iOS SDK in "x.y.z" format. Release versions are available [here](https://github.com/Appboy/appboy-ios-sdk/releases).

For further instructions using Carthage, please refer to their [user guide][7] on Github.

Once you've synced the Braze SDK release artifacts (we support Carthage via a zip of release artifacts attached to our Github releases), integrate the `Appboy_iOS_SDK.framework` and `SDWebImage.framework` into your project. Then, in your Application delegate do:


{% tabs %}
{% tab OBJECTIVE-C %}

Add the following line of code to your `AppDelegate.m` file:

```objc
#import <Appboy-iOS-SDK/AppboyKit.h>
```

Within your `AppDelegate.m` file, add the following snippet within your `application:didFinishLaunchingWithOptions` method:

```objc
[Appboy startWithApiKey:@"YOUR-API-KEY"
         inApplication:application
     withLaunchOptions:launchOptions];
```

{% endtab %}
{% tab swift %}

If you are integrating the Braze SDK with CocoaPods or Carthage, add the following line of code to your `AppDelegate.swift` file:

```swift
import Appboy_iOS_SDK
```

For more information about using Objective-C code in Swift projects, please see the [Apple Developer Docs](https://developer.apple.com/library/ios/documentation/swift/conceptual/buildingcocoaapps/MixandMatch.html).

In `AppDelegate.swift`, add following snippet to your `application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool`:

```swift
Appboy.start(withApiKey: "YOUR-API-KEY", in:application, withLaunchOptions:launchOptions)
```

__Note__: Braze's `sharedInstance` singleton will be nil before `startWithApiKey:` is called, as that is a prerequisite to using any Braze functionality.

{% endtab %}
{% endtabs %}

{% alert important %}
Be sure to update `YOUR-API-KEY` with the correct value from your **Settings** page.
{% endalert %}

{% alert warning %}
Be sure to initialize Braze in your application's main thread. Initializing asynchronously can lead to broken functionality.
{% endalert %}

### Dependency-Free Integration
If you want to use SDWebImage in your project along with the Braze SDK, you can install a thin version of the Braze Carthage framework. To do so, include the following lines in your Cartfile:

```
binary "https://raw.githubusercontent.com/Appboy/appboy-ios-sdk/master/appboy_ios_sdk.json"
github "SDWebImage/SDWebImage"
```

### Core Only Integration
If you want to use the Core SDK without any UI components, you can install the core version of the Braze Carthage framework by including the following line in your Cartfile:

```
binary "https://raw.githubusercontent.com/Appboy/appboy-ios-sdk/master/appboy_ios_sdk_core.json"
```

### Specifying Your Custom Endpoint or Data Cluster

Your Braze representative should have already advised you of the [correct endpoint]({{site.baseurl}}/user_guide/administrative/access_braze/sdk_endpoints/).

#### Compile-time Endpoint Configuration (Recommended)

{% alert note %}
Note that as of December 2019, custom endpoints are no longer given out, if you have a pre-existing custom endpoint, you may continue to use it. For a list of our available endpoints, <a href="{{site.baseurl}}/api/basics/#endpoints">click here</a>.
{% endalert %}

If given a pre-existing custom endpoint...
- Starting with Braze iOS SDK v3.0.2, you can set a custom endpoint using the `Info.plist` file. Add the Braze dictionary to your `Info.plist` file. Inside the `Braze` dictionary, add the `Endpoint` string subentry and set the value to your custom endpoint URLs authority (for example, `sdk.iad-01.braze.com`, not `https://sdk.iad-01.braze.com`). Note that prior to Braze iOS SDK v4.0.2, the dictionary key `Appboy` must be used in place of `Braze`.

#### Runtime Endpoint Configuration

If given a pre-existing custom endpoint...
- Starting with Braze iOS SDK v3.17.0+, you can override set your endpoint via the `ABKEndpointKey` inside the `appboyOptions` parameter passed to `startWithApiKey:inApplication:withLaunchOptions:withAppboyOptions:`. Set the value to your custom endpoint URLs authority (for example, `sdk.iad-01.braze.com`, not `https://sdk.iad-01.braze.com`).

{% alert note %}
Support for setting endpoints at runtime using `ABKAppboyEndpointDelegate` has been removed in Braze iOS SDK v3.17.0. If you already use `ABKAppboyEndpointDelegate`, note that in Braze iOS SDK versions v3.14.1 to v3.16.0, any reference to `dev.appboy.com` in your `getApiEndpoint()` method must be replaced with a reference to `sdk.iad-01.braze.com`.
{% endalert %}

{% alert important %}
To find out your specific cluster or custom endpoint, please ask your Customer Success Manager or reach out to our support team.
{% endalert %}

## Swift Package Manager Integration {#swift_package_manager}

### Requirements

Installing the iOS SDK via [Swift Package Manager][8] (SPM) automates the majority of the installation process for you. Before beginning this process please ensure that you are using Xcode 12 or greater.

> Note that tvOS is not yet available via _Swift Package Manager_.

### Step 1: Adding the dependency to your project

Open your project and navigate to your project's settings. Select the tab named _Swift Packages_ and click on the add button (+) at the bottom left.

![Swift Package Manager: Menu 1][9]

When importing SDK version `3.33.1` and above, enter the url of our iOS SDK repository (`https://github.com/braze-inc/braze-ios-sdk`) in the text field and click _Next_:

> For versions `3.29.0` through `3.32.0`, use the URL `https://github.com/Appboy/Appboy-ios-sdk`.

![Swift Package Manager: Menu 2][10]

On the next screen, select the SDK version and click _Next_.

> Versions 3.29.0 and higher are compatible with _Swift Package Manager_.

![Swift Package Manager: Menu 3][11]

Select the package that best fits your needs and click _Finish_:
- `AppboyUI`
  - Best suited if you plan to use UI components provided by Braze.
  - Includes `AppboyKit` automatically.
- `AppboyKit`
  - Best suited if you don't need to use any of the UI components provided by Braze (e.g. Content Cards, In-App Messages, etc.).
- `AppboyPushStory`
  - Include this package if you have integrated Push Stories in your app. This is supported as of version 3.31.0.
  - In the dropdown under `Add to Target`, select your `ContentExtension` target instead of your main app's target. 
  
> Make sure you select **either** `AppboyKit` **or** `AppboyUI`. Including both packages can lead to undesired behavior.

![Swift Package Manager: Menu 4][12]

### Step 2: Configuring your project

Next, navigate to your project build settings and add the `-ObjC` flag to the _Other Linker Flags_ setting. Please note that this flag __must be added and [errors](https://developer.apple.com/library/archive/qa/qa1490/_index.html) resolved__ in order to further integrate the SDK.

![Swift Package Manager: Menu 5][13]

Edit the scheme of the target including the Appboy package (_Product > Scheme > Edit Scheme_ menu item):
- Click the expand ▶︎ next to _Build_ and select _Post-actions_. Press _+_ and select _New Run Script Action_.
- In the dropdown next to _Provide build settings from_, select your app's target.
- Copy this script into the open field:
```sh
# iOS
bash "$BUILT_PRODUCTS_DIR/Appboy_iOS_SDK_AppboyKit.bundle/Appboy.bundle/appboy-spm-cleanup.sh"
# macOS (if applicable)
bash "$BUILT_PRODUCTS_DIR/Appboy_iOS_SDK_AppboyKit.bundle/Contents/Resources/Appboy.bundle/appboy-spm-cleanup.sh"
```

![Swift Package Manager: Menu 7][14]

### Step 3: Updating your App Delegate

{% tabs %}
{% tab OBJECTIVE-C %}

Add the following line of code to your `AppDelegate.m` file:

```objc
#import "AppboyKit.h"
```

Within your `AppDelegate.m` file, add the following snippet within your `application:didFinishLaunchingWithOptions` method:

```objc
[Appboy startWithApiKey:@"YOUR-APP-IDENTIFIER-API-KEY"
         inApplication:application
     withLaunchOptions:launchOptions];
```

{% endtab %}
{% tab swift %}

Add the following line of code to your `AppDelegate.swift` file:

```swift
import AppboyKit
```

For more information about using Objective-C code in Swift projects, please see the [Apple Developer Docs](https://developer.apple.com/library/ios/documentation/swift/conceptual/buildingcocoaapps/MixandMatch.html).

In `AppDelegate.swift`, add following snippet to your `application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool`:

```swift
Appboy.start(withApiKey: "YOUR-APP-IDENTIFIER-API-KEY", in:application, withLaunchOptions:launchOptions)
```

__Note__: Braze's `sharedInstance` singleton will be `nil` before `startWithApiKey:` is called, as that is a prerequisite to using any Braze functionality.

{% endtab %}
{% endtabs %}

{% alert important %}
Be sure to update `YOUR-APP-IDENTIFIER-API-KEY` with the correct value from your **Settings** page. For more information on where to find your App Identifier API key, check out our [API documentation]({{site.baseurl}}/api/api_key/#the-app-identifier-api-key).
{% endalert %}

{% alert warning %}
Be sure to initialize Braze in your application's main thread. Initializing asynchronously can lead to broken functionality.
{% endalert %}

### Step 4: Specify Your Data Cluster

{% alert note %}
Note that as of December 2019, custom endpoints are no longer given out, if you have a pre-existing custom endpoint, you may continue to use it. For a list of our available endpoints, <a href="{{site.baseurl}}/api/basics/#endpoints">click here</a>.
{% endalert %}

#### Compile-time Endpoint Configuration (Recommended)

If given a pre-existing custom endpoint...
- Starting with Braze iOS SDK v3.0.2, you can set a custom endpoint using the `Info.plist` file. Add the Braze dictionary to your `Info.plist` file. Inside the `Braze` dictionary, add the `Endpoint` string subentry and set the value to your custom endpoint URL's authority (for example, `sdk.iad-01.braze.com`, not `https://sdk.iad-01.braze.com`). Note that prior to Braze iOS SDK v4.0.2, the dictionary key `Appboy` must be used in place of `Braze`.

Your Braze representative should have already advised you of the [correct endpoint]({{site.baseurl}}/user_guide/administrative/access_braze/sdk_endpoints/).

#### Runtime Endpoint Configuration

If given a pre-existing custom endpoint...
- Starting with Braze iOS SDK v3.17.0+, you can override set your endpoint via the `ABKEndpointKey` inside the `appboyOptions` parameter passed to `startWithApiKey:inApplication:withLaunchOptions:withAppboyOptions:`. Set the value to your custom endpoint URL's authority (for example, `sdk.iad-01.braze.com`, not `https://sdk.iad-01.braze.com`).

{% alert important %}
To find out your specific cluster, please ask your Customer Success Manager or reach out to our support team.
{% endalert %}


[1]: http://cocoapods.org/
[2]: https://www.ruby-lang.org/en/installation/
[3]: http://guides.cocoapods.org/using/getting-started.html "CocoaPods Installation Directions"
[4]: https://github.com/braze-inc/braze-ios-sdk/blob/master/AppboyKit/include/Appboy.h
[5]: {% image_buster /assets/img_archive/podsworkspace.png %}
[6]: http://guides.cocoapods.org/using/troubleshooting.html "CocoaPods Troubleshooting Guide"

[7]: https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos

[8]: https://swift.org/package-manager/
[9]: {% image_buster /assets/img/ios/spm/image1.png %}
[10]: {% image_buster /assets/img/ios/spm/image2.png %}
[11]: {% image_buster /assets/img/ios/spm/image3.png %}
[12]: {% image_buster /assets/img/ios/spm/image4.png %}
[13]: {% image_buster /assets/img/ios/spm/image5.png %}
[14]: {% image_buster /assets/img/ios/spm/image6.png %}