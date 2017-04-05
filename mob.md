# Ad Call Reference

This document describes our ad calls, the `/mob` calls, which are used to request ads for all apps. These calls include information about the client device as query string parameters.
For definitions of all the supported parameters, see [Request parameters](#request-parameters).



## Request parameters

The ad call accepts the query string parameters shown below.
Note that device ID fields are case sensitive.
Several of these parameters need to be URL encoded. For more information about URL encoding, see this [Wikipedia article](https://en.wikipedia.org/wiki/Percent-encoding).

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
id | string | yes | The unique ID of the placement where the ad will serve
appid | stirng | recommended | This string is used to identify a mobile app running on Android or iOS devices.<br>On Android, this is the app's package name. It's formatted as follows:com.example.helloworld.<br>On iOS, this is the app's iTunes ID. It's formatted as follows: 123456789.<br>Many buyers set campaign targeting and reporting based on appid. Failing to supply a correct appid will make your inventory unattractive to these buyers. Therefore, passing this field is strongly recommended when supply_type is set to "mobile_app". Note that this is what our Mobile SDKs do when they request an ad.
carrier | string | no | Name of the mobile carrier. This is optional because our system can usually deduce the carrier from the device's IP address.
connection_type | string | no | The type of network used by the device. Allowed values are "wifi" or "wan".
devmake | string | no | Manufacturer of the device requesting an ad.
devmodel | string | no | Model of the device requesting an ad
LimitAdTrackingEnabled | boolean | no | If true, the user has set the system-level preference to not receive behaviorally targeted ads. Allowed values: true, false, 1, or 0.
devtime | int | no | The time on the device, measured in seconds since the epoch, or UNIX Time.
devtz | string | no | The device's timezone.
md5udid | string | no | The MD5 hash of the ANDROID_ID. This should only be sent for Android devices. This should be URL encoded.
sha1udid | string | no | The SHA1 hash of the ANDROID_ID. This should only be sent for Android devices. This should be URL encoded.
idfa | string | no | The Apple advertising identifier for iOS devices running iOS 6+.
aaid | string | no | The Google advertising identifier for Android devices as retrieved from Google Play services.
ip | string | no | IP address of the device making the ad request, e.g., 207.237.150.246.<br>If not specified, the IP passed via HTTP headers will be used for geo detection instead.
url | string | no | The URL of the web page which the ad will be placed. This should only be sent for a web browser. This should be URL encoded.<br>If not specified, the url passed via HTTP headers will be used.
language | string | no | The device's language, specified with an ISO Language Code.
loc | string | no | The user's location expressed in latitude and longitude, in the format: snnn.ddddddddddddd,snnn.ddddddddddddd. Up to 13 decimal places of precision are allowed.
loc_age | int | no | Age of the location data in milliseconds.
loc_prec | int | no | Precision of the location data in meters.
max_size | string | no | The maximum banner size allowed, e.g., "320x250". N/A for Interstitial ads.
mcc | int | no | The Mobile Country Code as specified by the ITU.
mnc | int | no | The Mobile Network Code as specified by the ITU.
orientation | string | no | Device screen orientation during the ad request. Allowed values are "v" or "h".
os | string | no | The operating system of the device. For example, Android 4.0.2. For mobile apps, this is usually provided by the user agent.
st | string | no | The supply type of the inventory, which indicates the environment in which an ad will be shown. Allowed values: "mobile_app", "mobile_web", or "web". Defaults to "mobile_app".
size | string | no | The requested banner size, e.g., "320x50", or the screen size for Interstitial ads.
ua | string | no | The user agent string associated with the device requesting an ad. If specified, this value will be used rather than the standard user agent sent via HTTP header. This should be URL encoded.
cat | string | no | universal category, e.g., "IAB13,IAB21-1"
vnd_cat | string | no | custom categories (vendor), e.g.: "3,24,55"
vnd_tag | string | no | custom tags (vendor), e.g.: "2,5,10"
format | string | no | response format, supported values: `json` (default), `xml` (only for vast 3.0 video placement)

## Response

banner/interstitial example

```javascript
{
  "status": "ok", // `no_bid`, `error`
  "ads": [
    {
      "type": "banner", // `interstitial`, `vast30`
      "width": 320,
      "height": 50,
      "content": "<script type=\"text/javascript\">document.write('<a href=\"http://example.com/cute/kittens" target=\"_blank\"><img width=\"320\" height=\"50\" style=\"border-style: none\" src=\"http://placekitten.com/g/320/50\"/></a>');</script>"
    }
  ]
}
```

VAST example

```javascript
{
  "status": "ok",
  "ads": [
    {
      "type": "vast30",
      "width": 320,
      "height": 120,
      "content": "<VAST version="3.0">...vast30 xml here ...</VAST>"
    }
  ]
}
```

### response object

Field | Type | Description
----- | ---- | -----------
status | string | one of `ok`, `no_bid` or `error`; `ok` indicates there're ads in the response, `no_bid` indicates no one has bid on this opertunity
ads | array | array of ad object
errorMessage | string | error message of `status` is `error`
native | array | list of native objects, see [native](#native)

### ad object

Field | Type | Description
----- | ---- | -----------
type | string | one of `banner`, `interstitial` or `vast30`
width | int | widht of the creative
height | int | height of the creative
content | string | html snippet for `banner` and `interstitial`, vast 3.0 xml for `vast30`

### Native

```javascript
{
  "status": "ok",
  "version": 1,
  "native": [
    {
      "type": "in-feed-standard",
      "title": "Cute kittens",
      "description": "Have some cute kittens",
      "full_text": "Really long text",
      "icon_img_url": "https://dummyimage.com/100x100?text=ICON",
      "main_media": [
        {
          "label": "default",
          "width": 800,
          "height": 500,
          "url": "https://dummyimage.com/800x500?text=MAIN_IMAGE"
        }
      ],
      "cta": "download",
      "click_trackers": [
        "http://dummyimage.com/1x1?text=CLICK-TRACKER",
        "http://dummyimage.com/1x1?text=CLICK-TRACKER2"
      ],
      "impression_trackers": [
        "https://dummyimage.com/1x1?text=IMP-TRACKER",
        "https://dummyimage.com/1x1?text=IMP-TRACKER2"
      ],
      "click_url": "http://example.com/cute/kittens"
    }
  ]
}
```

#### Native Object


Field | Type | Description
----- | ---- | -----------
title | text | The title displayed with the native ad.
description | text | A short description of the ad's offer to the user.
full_text | text | The full text of the native ad. Much longer than descrip tion.
context | string | The social context where the native ad will appear in the application. This varies depending on the media subtype of the native ad. For example, it may be a string such as "newsfeed".
icon_img_url | string | The URL of the icon image for the native ad. We don't validate this; you must ensure that the URL resolves to the proper icon image for your native ad type. Will contain a secure URL (HTTPS/SSL) if the auction is secure.
main_media | array | The main content that will appear in the body of the of native ad. For now, we only support images. For more objects information, see Main Media below.
sponsored | string | The brand name that the user should associate with this creative.
cta | string | The "call to action" text of the ad, e.g., "Download now".
rating | object | If the advertisement is for an app, this will display the app's rating in the relevant app store. Note that the rating is provided by the advertiser. We do not directly pull ratings from app stores.
click_url | string | The destination URL that will open if the user clicks the ad. Note that this URL could launch an app on a device.
click_fallback_url | string | A fallback web URL to be used if the deep link provided in the click_url is not supported on the device. For mobile inventory only.
custom_key_values | array | Some sellers allow the buyer to pass a list of custom of key/value pairs. For more information, see Custom Key objects Values below.
click_trackers | array | A list of third-party click tracking URLs intended to be of used with native creatives. For more information, see Cli objects ck Trackers below.
impression_trackers | array | A list of third-party impression tracking URLs intended to of be used with native creatives. For more information, see objects Impression Trackers below.

##### Main Media

Field | Type | Description
----- | ---- | -----------
width | int | The width of the main native ad media.
height | int | The height of the main native ad media.
media_url | string | The URL from which the media can be downloaded.
media_url_secure | string | Like media_url, but with SSL.

##### Custom Key Values

Field | Type | Description
----- | ---- | -----------
custom_key | string | A seller-defined key string.
custom_value | string | A seller-defined value string.

##### Click Trackers

Field | Type | Description
----- | ---- | -----------
click_tracker_url | string | A third-party click tracking URL.

##### Impression Trackers

Field | Type | Description
----- | ---- | -----------
impression_tracker_url | string | A third-party impression tracking URL.
impression_tracker_url_secure | string | A third-party impression tracking URL (that uses SSL).
