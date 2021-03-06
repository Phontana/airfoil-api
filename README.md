# Airfoil API

Wrap Airfoil's Applescript interface with a JSON API. This version is edited to work on Dutch localized machines.

### Setup

1. Install NodeJS
2. Clone this repo
3. `cd` into the application folder
4. To run the application, type:

`npm run start`
    
or:
 
`node /PATH/TO/APPLICATION/FOLDER/app.js`

### Installation

Usage of the Mac's LaunchAgent is recommended to keep the NodeJS server running. Create the following file in a text editor of choice and place it in `~/Library/LaunchAgents` and name it: `com.phontana.airfoilapi.plist`. 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>Label</key>
	<string>com.phontana.airfoilapi</string>
	<key>ProgramArguments</key>
	<array>
		<string>/usr/local/bin/node</string>
		<string>/PATH/TO/APPLICATION/FOLDER/app.js</string>
	</array>
	<key>RunAtLoad</key>
	<true/>
</dict>
</plist>
```

With every reboot or new login the NodeJS server will start the `airfoil-api` application

### Usage

    $ curl http://localhost:8080/speakers
    [{"connected":"false","volume":0.75,"name":"Computer","id":"com.rogueamoeba.airfoil.LocalSpeaker"},{"connected":"false","volume":0.9375,"name":"stream","id":"685B35A4C6BC@stream"},{"connected":"true","volume":0.5,"name":"loft-bathroom","id":"F0D1A90B2769@loft-bathroom"},{"connected":"false","volume":0.75,"name":"magnavox","id":"F0D1A9083B63@magnavox"},{"connected":"false","volume":0.49470898509,"name":"Bedroom ","id":"68D93C804DEA@Bedroom "},{"connected":"false","volume":0.679894208908,"name":"loft","id":"B034953D7649@loft"}]
    $ curl -X POST http://localhost:8080/speakers/F0D1A90B2769@loft-bathroom/connect
    {"id":"F0D1A90B2769@loft-bathroom","connected":"true"}
    $ curl -X POST http://localhost:8080/speakers/F0D1A90B2769@loft-bathroom/disconnect
    {"id":"F0D1A90B2769@loft-bathroom","connected":"false"}
    $ curl -X POST --data '0.75' http://localhost:8080/speakers/F0D1A90B2769@loft-bathroom/volume
    {"id":"F0D1A90B2769@loft-bathroom","volume":0.75}
    $ curl -X POST --data '0.76' http://localhost:8080/speakers/F0D1A90B2769@loft-bathroom/volume
    {"id":"F0D1A90B2769@loft-bathroom","volume":0.759999990463}
