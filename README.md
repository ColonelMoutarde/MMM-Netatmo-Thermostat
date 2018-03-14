# MMM-Netatmo-Thermostat

The MMM-Netatmo-Thermostat module is a module for the [MagicMirror²](https://github.com/MichMich/MagicMirror/).

This module displays your Netatmo thermostat information. It is a very basic module that displays the current temperature of the room and indicates whether the thermostat is heating up or not (thanks to the color displayed by the module).

| Heating | Cooling | Off
|----------------- |-----------|--------------
| ![netatmo-heating](https://user-images.githubusercontent.com/8746134/32518926-5ccb2162-c40b-11e7-8a5d-2da147049e4b.png) | ![netatmo-cooling](https://user-images.githubusercontent.com/8746134/32520309-cd8f37a4-c40f-11e7-89b4-aba68b9f6f1f.png) | ![netatmo-off](https://user-images.githubusercontent.com/8746134/32520450-5a2182bc-c410-11e7-9e84-9a339aa2a536.png)

## Installing the module

Run `git clone https://github.com/overflOw11/MMM-Netatmo-Thermostat` from inside your `MagicMirror/modules` folder.

## Getting the Netatmo developper id

Connect to the Netatmo connect website `https://dev.netatmo.com/myaccount/` and create an app.
Save the clientId and clientSecret automatically generated by Netatmo.

To get the refreshToken, you have to launch the following command. Don't forget to replace parameters by your account information :

`curl --data "grant_type=password&client_id=<YOUR_CLIENT_ID>&client_secret=<YOUR_CLIENT_SECRET>&username=<YOUR_NETATMO_LOGIN>&password=<YOUR_NETATMO_PASSWORD>&scope=read_thermostat" "https://api.netatmo.com/oauth2/token"`

In the response, you can find the refresh token. Save it for later.

## Using the module

To use this module, add the following configuration block to the modules array in the `config/config.js` file:
```js
var config = {
    modules: [
        {
            module: 'MMM-Netatmo-Thermostat',
            config: {
		clientId: "<YOUR_CLIENT_ID>",
		clientSecret: "<YOUR_CLIENT_SECRET>",
		refreshToken: "<REFRESH_TOKEN>",
		updateInterval: 60000,
		color: {
			heating: "orange",
			cooling: "blue",
			off: "grey"
		}
            }
        }
    ]
}
```

## Configuration options

| Option           | Description
|----------------- |-----------
| `clientId`       | *Required* Your client id from https://dec.netatmo.com/myaccount/. <br><br>**Type:** `String` <br>This value is **REQUIRED**.
| `clientSecret`   | *Required* Your client secret from https://dev.netatmo.com/myaccount/. <br><br>**Type:** `String` <br>This value is **REQUIRED**.
| `refreshToken`   | *Required* Your refresh token from the curl command previously describe. <br><br>**Type:** `String` <br> This value is **REQUIRED**.
| `updateInterval` | *Optional* Update interval of your Netatmo module. <br><br>**Type:** `int`(milliseconds) <br>Default 60000 milliseconds (1 minute).
| `color`	   | *Optional* Tab which define color for 'heating', 'cooling' and 'off' state. <br><br>**Type:** `String[]`<br>Default : heating: orange, cooling: blue, off: grey.<br>Possible values are 'blue', 'orange', 'red', 'green', 'purple', 'yellow', 'grey'.
