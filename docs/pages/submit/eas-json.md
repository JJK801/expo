---
title: Configuring EAS Submit with eas.json
sidebar_title: Configuration with eas.json
---

import EasJsonPropertiesTable from '~/components/plugins/EasJsonPropertiesTable';

import submitAndroidSchema from '~/scripts/schemas/unversioned/eas-json-submit-android-schema.js';
import submitIosSchema from '~/scripts/schemas/unversioned/eas-json-submit-ios-schema.js';

`eas.json` is your go-to place for configuring EAS Submit (and [EAS Build](/build/eas-json.md)). It is located at the root of your project next to your `package.json`. Even though `eas.json` is not mandatory for using EAS Submit, it makes your life easier if you'll need to switch between different configurations.

`eas.json` looks something like this:

```json
{
  "submit": {
    "production": {
      "android": {
        "serviceAccountKeyPath": "../path/to/api-xxx-yyy-zzz.json",
        "track": "internal"
      },
      "ios": {
        "appleId": "john@turtle.com",
        "ascAppId": "1234567890",
        "appleTeamId": "AB12XYZ34S"
      }
    }
  }
}
```

The JSON object under the `submit` key can contain multiple submit profiles. Every submit profile can have an arbitrary name. If you run `eas submit` without a profile name specified and you have the `production` profile defined in `eas.json`, it'll be used to configure your submission. If you'd like EAS CLI to pick up another submit profile, you need to specify it with a parameter, e.g. `eas submit --platform ios --profile foobar`.

The schema of this file looks like this:

<!-- prettier-ignore -->
```json
{
  "build": {
    // EAS Build configuration
    ...
  }
  "submit": {
    /* @info any arbitrary name - used as an identifier */"SUBMIT_PROFILE_NAME_1"/* @end */: {
      android: {
        /* @info Android-specific configuration */...ANDROID_OPTIONS/* @end */

      }
      ios: {
        /* @info iOS-specific configuration */...IOS_OPTIONS/* @end */

      }
    },
    /* @info any arbitrary name - used as an identifier */"SUBMIT_PROFILE_NAME_2"/* @end */: {

    },
    ...
  }
}
```

If you're also using EAS Build, [see how to use `eas.json` to configure your builds](/build/eas-json.md).

## Android-specific options

<EasJsonPropertiesTable schema={submitAndroidSchema}/>

## iOS-specific options

<EasJsonPropertiesTable schema={submitIosSchema}/>
