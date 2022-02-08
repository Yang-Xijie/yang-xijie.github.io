# Set Build Number in Xcode

> Author: [Yang-Xijie](https://github.com/Yang-Xijie)
> 
> 220125

For `Xcode 13` or later:

<https://useyourloaf.com/blog/xcode-13-missing-info.plist/>

```shell
#!/bin/sh

# [References]
# http://www.mokacoding.com/blog/automatic-xcode-versioning-with-git/
# https://crunchybagel.com/auto-incrementing-build-numbers-in-xcode/

# [Functions]
# Automatically sets version of target based on most recent tag in git
# Automatically sets build number to number of commits

# [Usage]
# Add a script to build phase in Xcode at the top of the chain named `Set Build Number`
# Put this script (`set_build_number.sh`) in the root of the xcode project in a directory called `Scripts`
# Call the script as `$SRCROOT/Scripts/set_build_number.sh` in Xcode build phase

git=$(sh /etc/profile; which git)

number_of_commits=$("$git" rev-list HEAD --count)
git_release_version=$("$git" describe --tags --always --abbrev=0)

/usr/libexec/PlistBuddy -c "Set :CFBundleVersion $number_of_commits" "${PROJECT_DIR}/${INFOPLIST_FILE}"
/usr/libexec/PlistBuddy -c "Set :CFBundleShortVersionString $git_release_version" "${PROJECT_DIR}/${INFOPLIST_FILE}"
```