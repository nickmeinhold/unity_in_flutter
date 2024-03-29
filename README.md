# unity_in_flutter

Testing out different ways of getting Unity to run in a Flutter app.

## flutter_unity_widget

https://github.com/snowballdigital/flutter-unity-view-widget

Steps to get the AR Demo working 
1. in `pubspec.yaml` dependencies, add `flutter_unity_widget:`
1. copy `ARDemoApp` from `flutter-unity-view-widget/example/unity/` to `unity/`
1. open `ARDemoApp` with Unity 
1. ensure at least one scene is selected 
1. select the `Flutter` menu item -> `Export iOS` 
1. open `Runner.xcworkspace` 
1. right click in the Navigator and select Add Files to “Runner” -> `UnityExport/Unity-Iphone.xcodeproj`
1. select `Unity-iPhone/Data` folder and change Target Membership to `UnityFramework`
1. Add to `Runner/Runner/Runner-Bridging-Header.h` ->
```ObjC
#import "UnityUtils.h" 
```
10. add to `AppDelegate.swift` before the `GeneratePluginRegistrant` call:
```Swift
InitArgs(CommandLine.argc, CommandLine.unsafeArgv)
```
11. opt-in to embedded views preview, by adding the key `io.flutter.embedded_views_preview` with value `YES` to `Info.plist`
12. add another entry to `Info.plist` with key: `Privacy - Camera Usage Description` and value: `$(PRODUCT_NAME) uses Cameras`
13. select Runner, Targets -> Runner, then Build Phases -> Embed Frameworks, then hit + and select UnityFramework.framework  