endpoint: `/mob`

## Reqeust

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
sha1udid | string | no | The SHA1 hash of the ANDROID_ID. This should only be sent for Android devices. This should be URL encoded..
idfa | string | no | The Apple advertising identifier for iOS devices running iOS 6+.
aaid | string | no | The Google advertising identifier for Android devices as retrieved from Google Play services.
ip | string | no | IP address of the device making the ad request, e.g., 207.237.150.246.<br>If not specified, the IP passed via HTTP headers will be used for geo detection instead.
language | string | no | The device's language, specified with an ISO Language Code.
loc | string | no | The user's location expressed in latitude and longitude, in the format: snnn.ddddddddddddd,snnn.ddddddddddddd. Up to 13 decimal places of precision are allowed.
loc_age | int | no | Age of the location data in milliseconds.
loc_prec | int | no | Precision of the location data in meters.
max_size | string | no | The maximum banner size allowed, e.g., "320x250". N/A for Interstitial ads.
mcc | int | no | The Mobile Country Code as specified by the ITU.
mnc | int | no | The Mobile Network Code as specified by the ITU.
orientation | string | no | Device screen orientation during the ad request. Allowed values are "v" or "h".
os | string | no | The operating system of the device. For example, Android 4.0.2. For mobile apps, this is usually provided by the user agent.
pcode | string | no | The postal code of the user requesting an ad. If not specified, postal code will be determined from the IP address.
psa | string | no | If true, PSAs will serve if the auction has no winner. Otherwise, an empty 200 OK HTTP response will be returned. Allowed values: true or false, 1 or 0.
st | string | no | The supply type of the inventory, which indicates the environment in which an ad will be shown. Allowed values: "mobile_app", "mobile_web", or "web". Defaults to"mobile_app".
size | string | no | The requested banner size, e.g., "320x50", or the screen size for Interstitial ads.
ua | string | no | The user agent string associated with the device requesting an ad. If specified, this value will be used rather than the standard user agent sent via HTTP header. This should be URL encoded.
cat | string | no | universal category, e.g., "IAB13,IAB21-1"
vnd_cat | string | no | custom categories (vendor), e.g.: "3,24,55"
vnd_tag | string | no | custom tags (vendor), e.g.: "2,5,10"

## Response

### Banner/Interstitial

```javascript
{
  "status": "ok",
  "ads": [
    {
      "type": "banner",
      "width": 320,
      "height": 50,
      "content": "<script type=\"text/javascript\">document.write('<a href=\"http://example.com/cute/kittens" target=\"_blank\"><img width=\"320\" height=\"50\" style=\"border-style: none\" src=\"http://placekitten.com/g/320/50\"/></a>');</script>"
    }
  ]
}
```

