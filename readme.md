<p align="center"> 
  <img src="https://user-images.githubusercontent.com/49455498/110968228-92031100-8357-11eb-922a-597e6f932c99.png" width=50%>
</p>
# zigbee-switch-deconz-to-homekit-doorbell-with-gate

<img width="913" alt="Snímek obrazovky 2021-03-29 v 20 03 07" src="https://user-images.githubusercontent.com/49455498/112880680-09ac9c00-90cb-11eb-94db-f48a7832aad0.png"># 




my simple node-red flow to have Apple Homekit native doorbell, by Philips Hue Smart Button.
With safety switch to on/off function.

video:<br>
https://youtu.be/CpSQrBIdOHY

node-red flow code
```
[{"id":"b2250e2d.b6bf88","type":"tab","label":"Doorbell","disabled":false,"info":""},{"id":"b464bbaa.5be868","type":"gate","z":"b2250e2d.b6bf88","name":"SAFE Gate Doorbell","controlTopic":"control","defaultState":"open","openCmd":"open","closeCmd":"close","toggleCmd":"toggle","defaultCmd":"default","statusCmd":"status","persist":true,"x":820,"y":160,"wires":[["b3d1c64d.ac1b58"]]},{"id":"9bda3635.6fb588","type":"homekit-service","z":"b2250e2d.b6bf88","isParent":true,"bridge":"b51ae49c.1f963","parentService":"","name":"Doorbell switch","serviceName":"Switch","topic":"","filter":false,"manufacturer":"MADE by  jakubkasparek.cz","model":"1.2.0","serialNo":"Default Serial Number","firmwareRev":"1.2.0","hardwareRev":"1.2.0","softwareRev":"1.2.0","cameraConfigVideoProcessor":"ffmpeg","cameraConfigSource":"","cameraConfigStillImageSource":"","cameraConfigMaxStreams":2,"cameraConfigMaxWidth":1280,"cameraConfigMaxHeight":720,"cameraConfigMaxFPS":10,"cameraConfigMaxBitrate":300,"cameraConfigVideoCodec":"libx264","cameraConfigAudioCodec":"libfdk_aac","cameraConfigAudio":false,"cameraConfigPacketSize":1316,"cameraConfigVerticalFlip":false,"cameraConfigHorizontalFlip":false,"cameraConfigMapVideo":"0:0","cameraConfigMapAudio":"0:1","cameraConfigVideoFilter":"scale=1280:720","cameraConfigAdditionalCommandLine":"-tune zerolatency","cameraConfigDebug":false,"cameraConfigSnapshotOutput":"disabled","cameraConfigInterfaceName":"","characteristicProperties":"{}","waitForSetupMsg":false,"outputs":2,"x":400,"y":100,"wires":[["59a1fbb1.f416f4"],[]]},{"id":"59a1fbb1.f416f4","type":"switch","z":"b2250e2d.b6bf88","name":"","property":"payload.On","propertyType":"msg","rules":[{"t":"cont","v":"true","vt":"str"},{"t":"cont","v":"false","vt":"str"}],"checkall":"true","repair":false,"outputs":2,"x":490,"y":160,"wires":[["b92cd145.81927"],["3fee1e79.68013a"]]},{"id":"b92cd145.81927","type":"change","z":"b2250e2d.b6bf88","name":"Open","rules":[{"t":"set","p":"payload","pt":"msg","to":"open","tot":"str"},{"t":"set","p":"topic","pt":"msg","to":"control","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":610,"y":140,"wires":[["b464bbaa.5be868"]]},{"id":"3fee1e79.68013a","type":"change","z":"b2250e2d.b6bf88","name":"close","rules":[{"t":"set","p":"payload","pt":"msg","to":"close","tot":"str"},{"t":"set","p":"topic","pt":"msg","to":"control","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":610,"y":180,"wires":[["b464bbaa.5be868"]]},{"id":"a8a4a8e4.4ed17","type":"debug","z":"b2250e2d.b6bf88","name":"Doorbell","active":true,"tosidebar":true,"console":false,"tostatus":true,"complete":"payload","targetType":"msg","statusVal":"payload","statusType":"auto","x":880,"y":300,"wires":[]},{"id":"b261f9a0.b695f8","type":"inject","z":"b2250e2d.b6bf88","name":"status","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":true,"onceDelay":0.1,"topic":"control","payload":"status","payloadType":"str","x":610,"y":80,"wires":[["b464bbaa.5be868"]]},{"id":"12d65d88.3a9d02","type":"status","z":"b2250e2d.b6bf88","name":"gate status","scope":["b464bbaa.5be868"],"x":260,"y":220,"wires":[["a52f8528.84eaa"]]},{"id":"a52f8528.84eaa","type":"change","z":"b2250e2d.b6bf88","name":"","rules":[{"t":"move","p":"status.text","pt":"msg","to":"payload.On","tot":"msg"},{"t":"change","p":"payload.On","pt":"msg","from":"open","fromt":"str","to":"true","tot":"bool"},{"t":"change","p":"payload.On","pt":"msg","from":"close","fromt":"str","to":"false","tot":"bool"}],"action":"","property":"","from":"","to":"","reg":false,"x":280,"y":160,"wires":[["9bda3635.6fb588"]]},{"id":"b3d1c64d.ac1b58","type":"homekit-service","z":"b2250e2d.b6bf88","isParent":true,"bridge":"b51ae49c.1f963","parentService":"","name":"Doorbell","serviceName":"Doorbell","topic":"","filter":false,"manufacturer":"MADE by  jakubkasparek.cz","model":"1.0","serialNo":"4815162342","firmwareRev":"1.0","hardwareRev":"1.0","softwareRev":"1.0","cameraConfigVideoProcessor":"","cameraConfigSource":"","cameraConfigStillImageSource":"","cameraConfigMaxStreams":"","cameraConfigMaxWidth":"","cameraConfigMaxHeight":"","cameraConfigMaxFPS":"","cameraConfigMaxBitrate":"","cameraConfigVideoCodec":"","cameraConfigAudioCodec":"","cameraConfigAudio":false,"cameraConfigPacketSize":"","cameraConfigVerticalFlip":false,"cameraConfigHorizontalFlip":false,"cameraConfigMapVideo":"","cameraConfigMapAudio":"","cameraConfigVideoFilter":"","cameraConfigAdditionalCommandLine":"","cameraConfigDebug":false,"cameraConfigSnapshotOutput":"disabled","cameraConfigInterfaceName":"","characteristicProperties":"{ \"Name\" : \"Doorbell on Entry\"}","waitForSetupMsg":false,"outputs":2,"x":880,"y":220,"wires":[["a8a4a8e4.4ed17"],["a8a4a8e4.4ed17"]],"icon":"node-red-contrib-xiaomi-devices/door-icon.png"},{"id":"c696d530.6b3398","type":"deconz-input","z":"b2250e2d.b6bf88","name":"","server":"f365504d.cf235","device":"00:17:88:01:08:03:4a:1b-01-fc00","device_name":"Smart Button : ZHASwitch","topic":"","state":"0","output":"always","outputAtStartup":true,"x":330,"y":300,"wires":[[],["90e34704.ae5188","1f5ccc04.e469ac"]]},{"id":"90e34704.ae5188","type":"change","z":"b2250e2d.b6bf88","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"{\"ProgrammableSwitchEvent\":1}","tot":"json"},{"t":"set","p":"topic","pt":"msg","to":"","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":580,"y":240,"wires":[["b464bbaa.5be868"]]},{"id":"7559cbb2.70679c","type":"deconz-battery","z":"b2250e2d.b6bf88","name":"","server":"f365504d.cf235","device":"00:17:88:01:08:03:4a:1b-01-fc00","device_name":"Smart Button : ZHASwitch","outputAtStartup":true,"x":330,"y":360,"wires":[[],["a03b2840.b4727"]]},{"id":"a03b2840.b4727","type":"homekit-service","z":"b2250e2d.b6bf88","isParent":false,"bridge":"","parentService":"b3d1c64d.ac1b58","name":"Doorbell Battery","serviceName":"BatteryService","topic":"","filter":false,"manufacturer":"NRCHKB","model":"1.2.0","serialNo":"Default Serial Number","firmwareRev":"1.2.0","hardwareRev":"1.2.0","softwareRev":"1.2.0","cameraConfigVideoProcessor":"ffmpeg","cameraConfigSource":"","cameraConfigStillImageSource":"","cameraConfigMaxStreams":2,"cameraConfigMaxWidth":1280,"cameraConfigMaxHeight":720,"cameraConfigMaxFPS":10,"cameraConfigMaxBitrate":300,"cameraConfigVideoCodec":"libx264","cameraConfigAudioCodec":"libfdk_aac","cameraConfigAudio":false,"cameraConfigPacketSize":1316,"cameraConfigVerticalFlip":false,"cameraConfigHorizontalFlip":false,"cameraConfigMapVideo":"0:0","cameraConfigMapAudio":"0:1","cameraConfigVideoFilter":"scale=1280:720","cameraConfigAdditionalCommandLine":"-tune zerolatency","cameraConfigDebug":false,"cameraConfigSnapshotOutput":"disabled","cameraConfigInterfaceName":"","characteristicProperties":"{}","waitForSetupMsg":false,"outputs":2,"x":580,"y":360,"wires":[[],[]]},{"id":"1f5ccc04.e469ac","type":"debug","z":"b2250e2d.b6bf88","name":"","active":true,"tosidebar":true,"console":false,"tostatus":true,"complete":"payload","targetType":"msg","statusVal":"payload","statusType":"auto","x":570,"y":300,"wires":[]},{"id":"b51ae49c.1f963","type":"homekit-bridge","bridgeName":"Node-RED","pinCode":"826-38-554","port":"","allowInsecureRequest":true,"manufacturer":"NRCHKB","model":"1.2.0","serialNo":"Default Serial Number","firmwareRev":"1.2.0","hardwareRev":"1.2.0","softwareRev":"1.2.0","customMdnsConfig":false,"mdnsMulticast":true,"mdnsInterface":"","mdnsPort":"","mdnsIp":"","mdnsTtl":"","mdnsLoopback":true,"mdnsReuseAddr":true,"allowMessagePassthrough":true},{"id":"f365504d.cf235","type":"deconz-server","name":"ConBee","ip":"192.168.XXX.XX","port":"80","ws_port":"443","secure":false,"polling":"15"}]

```
<br><br>
<img width="400px" src="https://user-images.githubusercontent.com/49455498/112881962-a3c11400-90cc-11eb-992a-be6c30792e74.jpg">



requered node-red pallete:<br>
<b>node-red-contrib-deconz</b><br>
https://flows.nodered.org/node/node-red-contrib-deconz
<br><br>
<b>node-red-contrib-homekit-bridged</b><br>
https://flows.nodered.org/node/@plasma2450/node-red-contrib-homekit-bridged
<br><br>
<b>node-red-contrib-simple-gate</b><br>
https://flows.nodered.org/node/node-red-contrib-simple-gate
<br><br>
