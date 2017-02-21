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
language | string | no |
loc | string | no |
loc_age | int | no |
loc_prec | int | no |
amax_size | string | no |
mcc | int | no |
mnc | int | no |
orientation | string | no |
os | string | no |
pcode | string | no |
psa | string | no |
sha1mac | string | no |
st | string | no |
size | string | no |
tmpl_id | string | no |
tmpl_id | string | no |
ua | string | no |
cat | string | no |
vnd_cat | string | no |
vnd_tag | string | no |


endpoint: `/mob`
