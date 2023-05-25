# Set Build Number in Xcode

> NOTICE: This method might make your project unable to upload to App Store Connect.

> Author: [Yang-Xijie](https://github.com/Yang-Xijie)
> 
> Updated in 220208 for Xcode 13.
> 
> [Bilibili |【Xcode】Version & Build Number](https://www.bilibili.com/video/BV1bL4y1375M)

```sh
#!/bin/sh

# [Functions]
# Automatically sets version of target based on most recent tag in git
# Automatically sets build number to number of commits

# [Usage]
# Add the script to project
#     Menu `Xcode > File > New > File...` (⌘N)
#     Search for `sh` and select `Shell Script`, name it `set_build_number.sh`
#     Put this script (`set_build_number.sh`) in the root of the Xcode project in a directory called `Scripts`
# Set build phase
#     In `Project > Target > Build Phase`, click plus at left and click `New Run Script Phase`. Name it `Set Build Number`.
#     Drag the newly created phase to **the top** of the build phase chain
#     Call `set_build_number.sh` as `$SRCROOT/Scripts/set_build_number.sh` in the newly created phase.
# For Xcode 13 and later, create the `Info.plist` in the root of your project.
#     Menu `Xcode > File > New > File...` (⌘N)
#     Search for `pro` and select `Property List`, name it `Info.plist`
#     In `Project > Target > Info`, copy all items to newly created `Info.plist`
#     In `Project > Target > Build Phases`, delete `set_build_number.sh` and `Info.plist` in `Copy Bundle Resources`
#     In `Project > Target > Build Settings`, search for `info.plist file`
#         Set `Generate Info.plist File` to `No`
#         Set `Info.plist File` to `$SRCROOT/Info.plist`
# Add the first tag in main branch of your git repository: `git tag -a 0.1 -m "init"`
# Switch to main branch and build the project. Version and build number will be automatically set.
# Use the biuld number and version in a Swift project as follows:
#     ```swift
#     let appVersionString: String = Bundle.main.object(forInfoDictionaryKey: "CFBundleShortVersionString") as! String
#     let buildNumber: String = Bundle.main.object(forInfoDictionaryKey: "CFBundleVersion") as! String
#     ```

# [Notes]
# This script is for Xcode 13 and later, check [Xcode 13 Missing Info.plist](https://useyourloaf.com/blog/xcode-13-missing-info.plist/) and [Xcode 13 release notes](https://developer.apple.com/documentation/xcode-release-notes/xcode-13-release-notes) for more information.
# Projects created from several templates no longer require configuration files such as entitlements and Info.plist files. Configure common fields in the target’s Info tab, and build settings in the project editor. These files are added to the project when additional fields are used. (68254857)

# [References]
# [Automated Xcode version and build numbering via Git](http://www.mokacoding.com/blog/automatic-xcode-versioning-with-git/)
# [Auto-Incrementing Build Numbers in Xcode](https://crunchybagel.com/auto-incrementing-build-numbers-in-xcode/)
# [Xcode 13 Missing Info.plist](https://useyourloaf.com/blog/xcode-13-missing-info.plist/)
# [Info.plist Is Missing in Xcode 13 — Here’s How To Get It Back](https://betterprogramming.pub/info-plist-is-missing-in-xcode-13-heres-how-to-get-it-back-1a7abf3e2514)

# [Author]
# [Yang-Xijie](https://github.com/Yang-Xijie)

git=$(sh /etc/profile; which git)
number_of_commits=$("$git" rev-list HEAD --count)
git_release_version=$("$git" describe --tags --always --abbrev=0)\

# For Xcode 12 and earlier, change `"${INFOPLIST_FILE}"` to `"${PROJECT_DIR}/${INFOPLIST_FILE}"`.
/usr/libexec/PlistBuddy -c "Set :CFBundleVersion $number_of_commits" "${INFOPLIST_FILE}"
/usr/libexec/PlistBuddy -c "Set :CFBundleShortVersionString $git_release_version" "${INFOPLIST_FILE}"
```
