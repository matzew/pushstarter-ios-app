# pushstarter-ios-app 

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

In ```PushStarter/AppDelegate.m``` you register for notification as below:

```
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
  [FH pushRegister:deviceToken andSuccess:^(FHResponse *success) {
    NSNotification *notification = [NSNotification notificationWithName:@"success_registered" object:nil];
    [[NSNotificationCenter defaultCenter] postNotification:notification];
    NSLog(@"Unified Push registration successful");
  } andFailure:^(FHResponse *failed) {
    NSNotification *notification = [NSNotification notificationWithName:@"error_register" object:nil];
    [[NSNotificationCenter defaultCenter] postNotification:notification];
    NSLog(@"Unified Push registration Error: %@", failed.error);
  }];
}
```
Register FH to receive remote push notification with success [1] and failure [2] callbacks.

### FH receives remote push notification

To receive notification, in ```PushStarter/AppDelegate.m```:

```Swift
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
    NSLog(@"UPS message received: %@", userInfo);
}
```
