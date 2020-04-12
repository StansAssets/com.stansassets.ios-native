# iOS Native Pro
Plugin gives you an ability to directly use **iOS** and **watchOS** API, in order to make your application feel more natural and friendly for the iOS users. Almost any App Store game has to implement **In-App Purchases, Game Center, Social sharing, Local Notifications etc**. And this is only small part of useful API and features we have in our plugin.

We’ve put all our experience of how to properly build a plugin for Unity developers community, that we gained from being an [Asset Store Publisher](https://assetstore.unity.com/publishers/2256) and making [Games & Applications](https://stansassets.com/#portfolio) for more than 8 years.

**Note:** The plugin source code is only avaliable after the purchase on the [Unity Asset Store](https://assetstore.unity.com/packages/tools/integration/ios-native-pro-119175)

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
