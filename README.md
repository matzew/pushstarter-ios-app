# pushstarter-ios-app 
> Swift version of PushStarter iOS app is available [here](https://github.com/feedhenry-templates/pushstarter-ios-app/tree/swift).

> ObjC/Cocoapods of PushStarter iOS app is available [here](https://github.com/feedhenry-templates/pushstarter-ios-app/tree/cocoapods).

The ```PushStarter``` project demonstrates how to include basic push functionality using [fh-ios-sdk](https://github.com/feedhenry/fh-ios-sdk) and Red Hat Mobile Application Platform.

|                 | Project Info  |
| --------------- | ------------- |
| License:        | Apache License, Version 2.0  |
| Build:          | Embedded FH.framework  |
| Documentation:  | http://docs.feedhenry.com/v3/dev_tools/sdks/ios.html|

## Build

1. Clone this project

2. Populate ```PushStarter/fhconfig.plist``` with your values as explained [here](http://docs.feedhenry.com/v3/dev_tools/sdks/ios.html#ios-configure).

3. open PushStarter.xcodeproj

## Example Usage

### FH registers for remote push notification

In ```PushStarter/AppDelegate.swift``` you register for notification as below:

```Swift
func application(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
  FH.pushRegister(deviceToken, andSuccess: { res in // [1]
    let notification = NSNotification(name: "sucess_registered", object: nil)
    NSNotificationCenter.defaultCenter().postNotification(notification)
    print("Unified Push registration successful")
  }, andFailure: {failed in                         // [2]
    let notification = NSNotification(name: "error_register", object: nil)
    NSNotificationCenter.defaultCenter().postNotification(notification)
    print("Unified Push registration Error \(failed.error)")
  })
}
```
Register FH to receive remote push notification with success [1] and failure [2] callbacks.

### FH receives remote push notification

To receive notification, in ```PushStarter/AppDelegate.swift```:

```Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject: AnyObject]) {
  print("UPS message received: \(userInfo)")
}
```

