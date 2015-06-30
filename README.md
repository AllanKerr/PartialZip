# PartialZip
This framework is designed to extract resources from zip files without the need to download the entire zip file. The intended use was for jailbroken iDevice projects to extract assets from the various zip files found here:
http://mesu.apple.com/assets/com_apple_MobileAsset_SoftwareUpdate/com_apple_MobileAsset_SoftwareUpdate.xml

The easiest way to use it is to drop **PZFileBrowser.h** and **PZFileBrowser.m** into your project. It is important to link to **libz.dylib** as this is required to decompress assets. **libz.dylib** can be included in a Theos make file by adding:

```
ProjectName_LIBRARIES = z
```

Usage:
``` objective-c
NSString *zipPath = @"http://appldnld.apple.com/iOS7.1/031-5051.20140630.1zyJC/com_apple_MobileAsset_SoftwareUpdate/be2f8a9534473bd41453e61169b860638d33c8e3.zip";

// Loads the zip files central directory
PZFileBrowser *browser = [PZFileBrowser browserWithPath:zipPath];

// Gets an array containing the paths to all files found in the central directory
NSArray *allPaths = [browser getAllPaths];

// If you find the path for the asset you want in allPaths you can use the path to fetch it
NSString *path = @"AssetData/payload/replace/System/Library/PrivateFrameworks/PhotoLibrary.framework/PLRedEye@2x.png";

// Fetches the data using the file path from the remote zip file
NSData *data = [browser getDataForPath:path];
```
The previous example works for well checking if an asset is present during development but can be extremely slow with large zip files due to the need to download the entire zip file's central directory.

In order to get around that it is possible to determine the byte range for a group of assets:
```

```
