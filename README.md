# unity_in_flutter

Testing out different ways of getting Unity to run in a Flutter app.

## flutter_unity_widget

https://github.com/snowballdigital/flutter-unity-view-widget

Steps to getting Unity project added as a library 

1. add flutter_unity_widget: as a flutter dependency
1. create a new Unity project at `unity/`
1. copy Build.cs and XCodePostBuild.cs to `unity/<Unity Project>/Assets/Scripts/Editor/`
1. select menu item: Flutter -> Export to iOS 
1. open `Runner.xcworkspace`
1. right click in the Navigator and select Add Files to “Runner” -> `UnityExport/Unity-Iphone.xcodeproj`
1. select `Unity-iPhone/Data` folder and change Target Membership to `UnityFramework` 
1. Add to `Runner/Runner/Runner-Bridging-Header.h` ->
```ObjC
#import "UnityUtils.h" 
```
8. add to `AppDelegate.swift` before the `GeneratePluginRegistrant` call:
```Swift
InitArgs(CommandLine.argc, CommandLine.unsafeArgv)
```
9. opt-in to embedded views preview, by adding the key `io.flutter.embedded_views_preview` with value `YES` to `Info.plist`
10. open `ios/UnityExport/Unity-iPhone.xcodeproj` and build 
11. select Runner, Targets -> Runner, then Build Phases -> Embed Frameworks, then hit + and select UnityFramework.framework 
