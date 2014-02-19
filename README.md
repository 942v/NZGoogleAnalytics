#NZGoogleAnalytics ![License MIT](https://go-shields.herokuapp.com/license-MIT-blue.png)

Quickly and easily integration with Google Analytics API for iOS.

[![Build Status](https://api.travis-ci.org/NZN/NZGoogleAnalytics.png)](https://api.travis-ci.org/NZN/NZGoogleAnalytics.png)
[![Cocoapods](https://cocoapod-badges.herokuapp.com/v/NZGoogleAnalytics/badge.png)](http://beta.cocoapods.org/?q=name%3Anzgoogleanalytics%2A)
[![Cocoapods](https://cocoapod-badges.herokuapp.com/p/NZGoogleAnalytics/badge.png)](http://beta.cocoapods.org/?q=name%3Anzgoogleanalytics%2A)

## Requirements

NZGoogleAnalytics works on iOS 5.0+ version and is compatible with ARC projects. It depends on the following Apple frameworks, which should already be included with most Xcode templates:

* Foundation.framework

You will need LLVM 3.0 or later in order to build NZGoogleAnalytics.

NZGoogleAnalytics uses [Google Analytics SDK for iOS](https://developers.google.com/analytics/devguides/collection/ios/resources) and [NZBundle](https://github.com/NZN/NZBundle).

## Adding NZGoogleAnalytics to your project

### Cocoapods

[CocoaPods](http://cocoapods.org) is the recommended way to add NZGoogleAnalytics to your project.

* Add a pod entry for NZGoogleAnalytics to your Podfile:

```
pod 'NZGoogleAnalytics'
```

* Install the pod(s) by running:

```
pod install
```

### Source files

Alternatively you can directly add source files to your project.

1. Download the [latest code version](https://github.com/NZN/NZGoogleAnalytics/archive/master.zip) or add the repository as a git submodule to your git-tracked project.
2. Open your project in Xcode, then drag and drop all files at `NZGoogleAnalytics` folder onto your project (use the "Product Navigator view"). Make sure to select Copy items when asked if you extracted the code archive outside of your project.
3. Install [Google Analytics SDK for iOS](https://developers.google.com/analytics/devguides/collection/ios/resources) and your frameworks dependencies
4. Install [NZBundle](https://github.com/NZN/NZBundle)

## Info

* Default values for debug/release mode:
	* `trackUncaughtExceptions`: NO
	* `dispatchInterval`: 5 seconds
	* `logLevel`: kGAILogLevelNone
	
* Default values for distribution mode:
	* `trackUncaughtExceptions`: YES
	* `dispatchInterval`: 20 seconds
	* `logLevel`: kGAILogLevelNone
	
* NZGoogleAnalytics use [NZBundle](https://github.com/NZN/NZBundle) for change build version name:
	* Debug and Relase: `X.X.Xa alpha`
	* Distribution: `X.X.Xa`	


## Usage

* Configure your `trackingID`:

```objective-c
...
#import "NZGoogleAnalytics.h"

@implementation NZAppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    [NZGoogleAnalytics setTrackingId:@"UA-000000-01"];
    return YES;
}

@end
```

* The NZGoogleAnalytics overrides the `+(void)load;` method of NSObject class, which is called every time the application starts.

* You can change the default setting:

```objective-c
#import "NZGoogleAnalytics.h"
...
[NZGoogleAnalytics setTrackUncaughtExceptions:YES];
BOOL trackUncaughtExceptions = [NZGoogleAnalytics trackUncaughtExceptions];
    
[NZGoogleAnalytics setDispatchInterval:60];
NSTimeInterval dispatchInterval = [NZGoogleAnalytics dispatchInterval];
    
[NZGoogleAnalytics setLogLevel:kGAILogLevelError];
GAILogLevel logLevel = [NZGoogleAnalytics logLevel];
```

* Easy track your View Controller:

	* Add `NZGoogleAnalytics-Tracker.plist` file to your project with the following configuration:
		* `class_name`: Your view controller class name
		* `view_name`: Your track view name

<p align="center">
  <img src="http://s21.postimg.org/mjlzwoz93/NZGoogle_Analytics_Tracker.jpg" alt="NZCircularImageView" title="NZCircularImageView" width="740" height="270">
</p>

* Configure your View Controller class:

```objective-c
#import "NZGoogleAnalyticsTracker.h"
...

// screen name: /ios/first_view
- (void)viewDidAppear:(BOOL)animated
{
    [super viewDidAppear:animated];
    [NZGoogleAnalyticsTracker trackViewWithController:self];
}
```

```objective-c
#import "NZGoogleAnalyticsTracker.h"
...

// screen name: /ios/first_view/id_001
- (void)viewDidAppear:(BOOL)animated
{
    [super viewDidAppear:animated];
    [NZGoogleAnalyticsTracker trackViewWithController:self withIdentifier:@"id_001"];
}
```

## License

This code is distributed under the terms and conditions of the [MIT license](LICENSE).

## Change-log

A brief summary of each NZGoogleAnalytics release can be found on the [wiki](https://github.com/NZN/NZGoogleAnalytics/wiki/Change-log).
