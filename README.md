# iOS Native Pro
Plugin gives you an ability to directly use **iOS** and **watchOS** API, in order to make your application feel more natural and friendly for the iOS users. Almost any App Store game has to implement **In-App Purchases, Game Center, Social sharing, Local Notifications etc**. And this is only small part of useful API and features we have in our plugin.

We’ve put all our experience of how to properly build a plugin for Unity developers community, that we gained from being an [Asset Store Publisher](https://assetstore.unity.com/publishers/2256) and making [Games & Applications](https://stansassets.com/#portfolio) for more than 8 years.

#### [Get from The Asset Store](https://assetstore.unity.com/packages/tools/integration/ios-native-pro-119175) |  [Wiki Guides & Tutorials](https://github.com/StansAssets/com.stansassets.ios-native/wiki) | [Scripting Reference](https://api.stansassets.com/ios-native/) | [Forum](https://forum.unity.com/threads/introducing-ios-native-pro.535120/)

**Note:** The plugin source code is only avaliable after the purchase on the [Unity Asset Store](https://assetstore.unity.com/packages/tools/integration/ios-native-pro-119175)

Plugin Build principles
-------------------

Apart from all the statements above, the Ultimate Mobile will inherit all the pro-line plugins development principles:

-  **Full Open source.** I believe only open-source products can work for the developer community. If you are a junior developer, we will be happy if you learn something with our code. If you are a senior developer, we do not want you to have a “backbox” in your project, and we are always open to critics and suggestions.
- **Strict code convention.**  We mostly use default the default [C# Coding Conventions](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions), but with few adjustments, we believe would help our users.
   - Filename / Class will contain plugin code prefix, so you will always know where it belongs.
   - Every public API is documented. Check our the [Scripting References](https://api.stansassets.com/ios-native/).
-   **Nice looking and user-friendly settings editor.** This one is pretty simple with any third-party plugin you are adding to your cool project, you want to have a centralized,  good-looking, and intuitive settings editor for it.
 - **Nice looking and user-friendly settings editor.** Every plugin we make will have one centralized, good-looking, and intuitive settings editor.
 - **Ability to enable/disable modules.** We understand you want to keep your project as clean as possible and application build size as small as possible. With our plugin only feature you use will be included in the project. You also have to enable explicitly enable the module, so you always aware of what exactly included in the build. 
 - **Automatic project configuration.** You do not have to make any additional configuration for your build. If something is missing, the plugin will fix this with the build pre-processing stage. The main goal is to be able to support cloud build services out of the box.

### API Convention
We do not want you to learn "another 3rd party plugin" API, that's why iOS Native plugin API is mirroring the Apple official `Objective-C` API in a `CSharp-ish` manner.  As an example see the sample how to share the first image from the photo gallery to Instagram

With the `Objective-C`
```objective-c.
PHFetchOptions *fetchOptions = [PHFetchOptions new];
fetchOptions.sortDescriptors = @[[NSSortDescriptor sortDescriptorWithKey:@"creationDate" ascending:false]];
PHFetchResult *result = [PHAsset fetchAssetsWithMediaType:PHAssetMediaTypeImage options:fetchOptions];

 NSString *localIdentifier = assetToShare.localIdentifier;
NSString *urlString = [NSString stringWithFormat:@"instagram://library?LocalIdentifier=%@",localIdentifier];
NSURL *instagramURL = [NSURL URLWithString:urlString];
if ([[UIApplication sharedApplication] canOpenURL: instagramURL])
{
    [[UIApplication sharedApplication] openURL:instagramURL options:@{} completionHandler:nil];
} else
{
	NSLog(@"Instagram application is not installed!");
}
```

With IOS Native plugin (`C#`)
```csharp
using SA.iOS.Photos;
using SA.iOS.UIKit;
...

var fetchOptions = new ISN_PHFetchOptions();
fetchOptions.SortDescriptor = new ISN_NSSortDescriptor("creationDate", false);
fetchOptions.FetchLimit = 1;

var fetchResult = ISN_PHAsset.FetchAssetsWithOptions(fetchOptions);

var lastAsset = fetchResult.FirstObject;
var url = "instagram://library?LocalIdentifier=" + lastAsset.LocalIdentifier;

if (ISN_UIApplication.CanOpenURL(url))
   ISN_UIApplication.OpenURL(url);
else
   Debug.LogError("Instagram application is not installed!");
```
