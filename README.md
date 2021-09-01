# SelligentM1
Test Project illustrating the build issues for Simulator when running on an M1 Mac, reported in this [issue](https://github.com/SelligentMarketingCloud/MobileSDK-iOS/issues/9).

## Environment Used
* MacBook Pro (13-inch, **M1**, 2020) _[This is crucial to reproduce the issue, it needs to be an M1 based machine]_.
* macOS Big Sur 11.4
* Xcode 12.5.1
* CocoaPods 1.10.2
* Selligent MobileSDK 2.6.2

## Setup
This repo contains a simple iOS App project, no code changed. Cocoapods were added, containing only the Selligent Mobile SDK pod. Usually, it should be possible to simply run this app on device or simulator, on either Intel-based or M1 based Mac.

However, when running on a M1 Mac, on Simulator, an error occurs.

## Steps to reproduce

1. Clone the repo to an M1 Mac.
2. `pod install` to install the Selligent Pod.
3. Open SelligentM1.xcworkspace in Xcode.
4. Select the main SelligentM1 scheme, and any simulator.
5. Run the app.

## Expected Result

The app should compile, be installed and start running on the selected simulator. (This is what happens on an Intel-based Mac.)

## Actual Result

The app fails to compile, and reports:

>ld: in /PROJECT_PARENT/SelligentM1/Pods/SelligentMobileSDK/iOS Lib/libSelligentMobile.a(SMNotifMapViewController.o), building for iOS Simulator, but linking in object file built for iOS, file '/PROJECT_PARENT/SelligentM1/Pods/SelligentMobileSDK/iOS Lib/libSelligentMobile.a' for architecture arm64

Indicating that the binary of this sdk is not suitable to be used on an M1 (ARM) Simulator.

## Consequences

iOS apps using the Selligent Mobile SDK cannot be compiled for simulator on new Apple hardware.

While there is a workaround by only running the app on physical devices, this brings severe limitations, because the simulator is often the easiest way for developing and running unit / UI tests. Especially when testing for different kinds of devices, iOS versions, etc.
