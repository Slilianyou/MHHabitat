# MHHabitat
```MHHabitat``` is an library for used to determine the runtime environment of an iOS library by inspecting the ```embedded.mobileprovision``` file that the XCode toolchain includes during the application packing process.

```MHHabitat``` supports detection of the following runtime environments:
* Development ```MHMobileProvisionTypeDebug```
* AdHoc ```MHMobileProvisionTypeAdHoc```
* Enterprise ```MHMobileProvisionTypeEnterprise```
* AppStore ```MHMobileProvisionTypeAppStore```

In the case ```MHHabitat``` can't find or parse the ```embedded.mobileprovision```, it will default to ```MHMobileProvisionTypeAppStore``` in order to prevent any user-facing issues.  This holds true except when compiled for iOS Simulator (```TARGET_IPHONE_SIMULATOR```), in which case a parsing failure will return ```MHMobileProvisionTypeUndetermined```.

## Usage
```objc
// Logging the current environment
NSLog(@"Current app environment is: %@", [MHHabitat mobileProvisionTypeString]);

// Toggle behavior based on environment
AFHTTPRequestOperationManager *manager;
if ([MHHabitat isAppProduction]) {
  manager = [[AFHTTPRequestOperationManager alloc] initWithBaseURL:@"http://dev.myapi.com"];
}
else {
  manager = [[AFHTTPRequestOperationManager alloc] initWithBaseURL:@"https://myapi.com"];
}
```
