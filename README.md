# Clove OS: Smart UI Sandbox Framework
### Developer Interface & API Reference Guide

---

## 📖 Application Overview

The **Clove Android Application** is a client-side runtime environment engineered for IoT interaction, data visualization, and hardware control. Instead of relying on rigid, pre-built dashboard architectures, Clove provides an open-ended presentation layer sandbox.

### How the Ecosystem Works:
1. **Custom UI Provisioning:** Developers bundle standard web assets (`index.html`, `styles.css`, JS modules, and static graphics) into a `.zip` file and upload it directly to the Clove app.
2. **Native Abstraction Virtualization:** The app renders these assets inside a secure sandbox viewport.
3. **Zero Native Code Required:** The runtime intercepts execution requests via the global window bridge (`window.Clove`), allowing your JavaScript to natively control hardware sensors, Bluetooth, USB serial, and file systems without writing native Android code.

---

## 🔗 Interactive API Reference Index

### Core & Initialization
* [`Clove.ready()`](#cloveready)
* [`Clove.connectIoT(config, callback)`](#cloveconnectiot)

### Device & Network Diagnostics
* [`Clove.device.info()`](#clovedeviceinfo)
* [`Clove.network.status()`](#clovenetworkstatus)

### Persistent State Storage
* [`Clove.storage.get(key)`](#clovestorageget)
* [`Clove.storage.set(key, value)`](#clovestorageset)
* [`Clove.storage.remove(key)`](#clovestorageremove)
* [`Clove.storage.clear()`](#clovestorageclear)

### Sandboxed File System
* [`Clove.file.write(path, data)`](#clovefilewrite)
* [`Clove.file.read(path, options)`](#clovefileread)
* [`Clove.file.exists(path)`](#clovefileexists)
* [`Clove.file.remove(path)`](#clovefileremove)
* [`Clove.file.open(path, mimeType)`](#clovefileopen)
* [`Clove.file.getAssetURL(path)`](#clovefilegetasseturl)

### Enterprise HTTP Networking
* [`Clove.http.request(options)`](#clovehttprequest)
* [`Clove.http.get(url, options)`](#clovehttpget)
* [`Clove.http.post(url, data, options)`](#clovehttppost)
* [`Clove.http.put(url, data, options)`](#clovehttpput)
* [`Clove.http.patch(url, data, options)`](#clovehttppatch)
* [`Clove.http.delete(url, options)`](#clovehttpdelete)
* [`Clove.http.setHeader(host, header, value)`](#clovehttpsetheader)
* [`Clove.http.setDataSerializer(serializer)`](#clovehttpsetdataserializer)

### User Experience & Feedback
* [`Clove.notification.alert(msg, title, btn)`](#clovenotificationalert)
* [`Clove.notification.confirm(msg, title, btns)`](#clovenotificationconfirm)
* [`Clove.notification.prompt(msg, title, btns, defText)`](#clovenotificationprompt)
* [`Clove.notification.beep(times)`](#clovenotificationbeep)
* [`Clove.notification.vibrate(ms)`](#clovenotificationvibrate)

### Bluetooth Classic Serial (SPP)
* [`Clove.bluetooth.list()`](#clovebluetoothlist)
* [`Clove.bluetooth.discoverUnpaired()`](#clovebluetoothdiscoverunpaired)
* [`Clove.bluetooth.connect(address)`](#clovebluetoothconnect)
* [`Clove.bluetooth.disconnect()`](#clovebluetoothdisconnect)
* [`Clove.bluetooth.write(data)`](#clovebluetoothwrite)
* [`Clove.bluetooth.read()`](#clovebluetoothread)
* [`Clove.bluetooth.readUntil(delimiter)`](#clovebluetoothreaduntil)
* [`Clove.bluetooth.subscribe(delimiter, callback)`](#clovebluetoothsubscribe)
* [`Clove.bluetooth.unsubscribe()`](#clovebluetoothunsubscribe)
* [`Clove.bluetooth.isConnected()`](#clovebluetoothisconnected)
* [`Clove.bluetooth.isEnabled()`](#clovebluetoothisenabled)
* [`Clove.bluetooth.enable()`](#clovebluetoothenable)

### Bluetooth Low Energy (GATT)
* [`Clove.ble.scan(services, seconds)`](#cloveblescan)
* [`Clove.ble.stopScan()`](#cloveblestopscan)
* [`Clove.ble.connect(id)`](#clovebleconnect)
* [`Clove.ble.disconnect(id)`](#clovebledisconnect)
* [`Clove.ble.read(id, serviceUuid, characteristicUuid)`](#clovebleread)
* [`Clove.ble.write(id, serviceUuid, characteristicUuid, data)`](#cloveblewrite)
* [`Clove.ble.writeWithoutResponse(id, serviceUuid, characteristicUuid, data)`](#cloveblewritewithoutresponse)
* [`Clove.ble.startNotification(id, serviceUuid, characteristicUuid, callback)`](#cloveblestartnotification)
* [`Clove.ble.stopNotification(id, serviceUuid, characteristicUuid)`](#cloveblestopnotification)
* [`Clove.ble.isEnabled()`](#clovebleisenabled)

### Wi-Fi Adapter Linkages
* [`Clove.wifi.getSSID()`](#clovewifigetssid)
* [`Clove.wifi.getIP()`](#clovewifigetip)
* [`Clove.wifi.list()`](#clovewifilist)
* [`Clove.wifi.connect(ssid, pass, algo, hid)`](#clovewificonnect)
* [`Clove.wifi.disconnect()`](#clovewifidisconnect)
* [`Clove.wifi.isEnabled()`](#clovewifiisenabled)

### Wired Hardware USB Serial
* [`Clove.usb.requestPermission(options)`](#cloveusbrequestpermission)
* [`Clove.usb.open(options)`](#cloveusbopen)
* [`Clove.usb.close()`](#cloveusbclose)
* [`Clove.usb.write(data)`](#cloveusbwrite)
* [`Clove.usb.read(callback)`](#cloveusbread)

### Native Media Capture
* [`Clove.camera.getPicture(options)`](#clovecameragetpicture)

### Spatial Geolocation
* [`Clove.geolocation.getCurrentPosition(options)`](#clovegeolocationgetcurrentposition)
* [`Clove.geolocation.watchPosition(callback, options)`](#clovegeolocationwatchposition)
* [`Clove.geolocation.clearWatch(watchId)`](#clovegeolocationclearwatch)

### MQTT Protocol Engine
* [`Clove.mqtt.connect(options)`](#clovemqttconnect)
* [`Clove.mqtt.disconnect()`](#clovemqttdisconnect)
* [`Clove.mqtt.publish(topic, payload, options)`](#clovemqttpublish)
* [`Clove.mqtt.subscribe(topic, callback)`](#clovemqttsubscribe)
* [`Clove.mqtt.unsubscribe(topic)`](#clovemqttunsubscribe)

---

## 🛠️ API Reference Detail

### Core & Initialization

<a name="cloveready"></a>
#### `Clove.ready()`
Blocks down-stream script execution until the native Android asset hosting environment is fully online and ready.
* **Arguments:** None
* **Returns:** `Promise<void>`
```javascript
document.addEventListener("DOMContentLoaded", async () => {
  try {
    console.log("Initializing webview bridge...");
    await window.Clove.ready();
    console.log("Clove Core API loaded successfully.");
  } catch (error) {
    console.error("Initialization failed:", error);
  }
});
```

---

<a name="cloveconnectiot"></a>
#### `Clove.connectIoT(config, callback)`
A simplified high-level macro method to start automated hardware data pipelines. Handles connection lifecycles and passes parsed text chunks directly to a visual loop interface.
* **Arguments:** * `config` *(Object)*: Configuration descriptor (`{ type: "ble" | "bluetooth" | "usb" | "mqtt" | "http", target: string, serviceUuid?: string, characteristicUuid?: string, delimiter?: string, pollInterval?: number }`)
  * `callback` *(Function)*: Continuous listener logic loop execution function `(data) => void`.
* **Returns:** `Promise<void>`
```javascript
async function launchLiveDashboardStream() {
  await window.Clove.ready();
  
  const pipelineConfig = {
    type: "bluetooth",
    target: "00:11:22:33:44:55",
    delimiter: "\n"
  };

  await window.Clove.connectIoT(pipelineConfig, (incomingPacket) => {
    console.log("Continuous Stream Packet received:", incomingPacket);
    document.getElementById("sensor-readout").innerText = incomingPacket;
  });
}
```

---

### Device & Network Diagnostics

<a name="clovedeviceinfo"></a>
#### `Clove.device.info()`
Queries details about the underlying host Android device operating system hardware layer.
* **Arguments:** None
* **Returns:** `Promise<Object>` containing `{ manufacturer: string, model: string, platform: string, version: string, uuid: string }`
```javascript
async function logSystemSpecs() {
  await window.Clove.ready();
  try {
    const specs = await window.Clove.device.info();
    console.log(`Device hardware verified: ${specs.manufacturer} ${specs.model} running Android OS ${specs.version}`);
  } catch (err) {
    console.error("Unable to query hardware specs:", err);
  }
}
```

---

<a name="clovenetworkstatus"></a>
#### `Clove.network.status()`
Inspects the current internet state and hardware interface route mapping layout.
* **Arguments:** None
* **Returns:** `Promise<Object>` containing `{ online: boolean, type: string }`
```javascript
async function checkNetworkBeforeSync() {
  await window.Clove.ready();
  const net = await window.Clove.network.status();
  
  if (net.online) {
    console.log(`Network status confirmed online via link style: ${net.type}`);
  } else {
    console.warn("Device is running completely offline.");
  }
}
```

---

### Persistent State Storage

<a name="clovestorageget"></a>
#### `Clove.storage.get(key)`
Retrieves a matching key record variable value directly out of secure long-term client sandbox tracking structures.
* **Arguments:** `key` *(String)*
* **Returns:** `Promise<any>`
```javascript
async function loadSavedCredentials() {
  await window.Clove.ready();
  const savedToken = await window.Clove.storage.get("auth_token");
  if (savedToken) {
    console.log("Authorization security token restored successfully.");
  }
}
```

---

<a name="clovestorageset"></a>
#### `Clove.storage.set(key, value)`
Saves key/value variable parameters safely across application reboots. Automatically parses layout arrays or objects to string sets.
* **Arguments:** `key` *(String)*, `value` *(any)*
* **Returns:** `Promise<void>`
```javascript
async function saveDashboardState() {
  await window.Clove.ready();
  const runtimeConfig = { theme: "cyberpunk", telemetryInterval: 250 };
  await window.Clove.storage.set("dashboard_prefs", runtimeConfig);
  console.log("User preferences serialized and saved.");
}
```

---

<a name="clovestorageremove"></a>
#### `Clove.storage.remove(key)`
Clears structural data references containing targeted tracking configuration keywords.
* **Arguments:** `key` *(String)*
* **Returns:** `Promise<void>`
```javascript
async function purgeCachedSession() {
  await window.Clove.ready();
  await window.Clove.storage.remove("dashboard_prefs");
  console.log("Specified storage key mapping has been deleted.");
}
```

---

<a name="clovestorageclear"></a>
#### `Clove.storage.clear()`
Wipes out all records within the local scope data ecosystem space.
* **Arguments:** None
* **Returns:** `Promise<void>`
```javascript
async function factoryResetLocalStorage() {
  await window.Clove.ready();
  await window.Clove.storage.clear();
  console.log("All sandbox key/value maps have been reset.");
}
```

---

### Sandboxed File System

<a name="clovefilewrite"></a>
#### `Clove.file.write(path, data)`
Saves raw string data lines or configuration sheets directly onto internal app-allocated media storage routes.
* **Arguments:** `path` *(String)*, `data` *(String | Object)*
* **Returns:** `Promise<any>`
```javascript
async function writeLogToDisk() {
  await window.Clove.ready();
  const reportPayload = { systemCode: "OK", updates: ["Sensors armed", "Batteries full"] };
  await window.Clove.file.write("diagnostics/daily_report.json", reportPayload);
  console.log("Log write operation completed cleanly.");
}
```

---

<a name="clovefileread"></a>
#### `Clove.file.read(path, options)`
Loads stored layout files. Automatically attempts to parse formatting arrays or string configurations matching `.json` suffixes.
* **Arguments:** `path` *(String)*, `options` *(Object)* *(Optional: `{ mode: "text" | "json" }`)*
* **Returns:** `Promise<any>`
```javascript
async function verifyDiskReport() {
  await window.Clove.ready();
  try {
    const reportData = await window.Clove.file.read("diagnostics/daily_report.json", { mode: "json" });
    console.log("Read complete. System Code details:", reportData.systemCode);
  } catch (err) {
    console.error("Error reading file path targets:", err);
  }
}
```

---

<a name="clovefileexists"></a>
#### `Clove.file.exists(path)`
Verifies specific storage space routing indices before initiating operational system reads.
* **Arguments:** `path` *(String)*
* **Returns:** `Promise<Boolean>`
```javascript
async function safeLoadAsset() {
  await window.Clove.ready();
  const fileFound = await window.Clove.file.exists("diagnostics/daily_report.json");
  if (fileFound) {
    console.log("Target resource paths mapped properly on storage disks.");
  }
}
```

---

<a name="clovefileremove"></a>
#### `Clove.file.remove(path)`
Removes specified sandboxed assets cleanly from local target directories.
* **Arguments:** `path` *(String)*
* **Returns:** `Promise<any>`
```javascript
async function cleanOldTelemetry() {
  await window.Clove.ready();
  await window.Clove.file.remove("diagnostics/daily_report.json");
  console.log("Target disk asset removed permanently.");
}
```

---

<a name="clovefileopen"></a>
#### `Clove.file.open(path, mimeType)`
Launches native system execution handles to open or view local reports outside the sandboxed web dashboard context.
* **Arguments:** `path` *(String)*, `mimeType` *(String)*
* **Returns:** `Promise<any>`
```javascript
async function triggerSystemPdfViewer() {
  await window.Clove.ready();
  await window.Clove.file.open("exports/schematic.pdf", "application/pdf");
  console.log("Native intent document handover triggered.");
}
```

---

<a name="clovefilegetasseturl"></a>
#### `Clove.file.getAssetURL(path)`
Transforms sandboxed file data references into web-safe asset URLs suitable for rendering inside DOM structures.
* **Arguments:** `path` *(String)*
* **Returns:** `Promise<String>`
```javascript
async function displayCapturedFrame() {
  await window.Clove.ready();
  const rawPath = "snapshots/node_view.jpg";
  const webSafeUrl = await window.Clove.file.getAssetURL(rawPath);
  document.getElementById("node-image-view").src = webSafeUrl;
}
```

---

### Enterprise HTTP Networking

<a name="clovehttprequest"></a>
#### `Clove.http.request(options)`
Passes API requests straight through native OS interface modules, bypassing browser CORS protection filters completely.
* **Arguments:** `options` *(Object)* containing `{ method: string, url: string, data?: any, headers?: any }`
* **Returns:** `Promise<Object>` containing `{ ok: boolean, status: number, body: any, headers: any }`
```javascript
async function queryCustomBackend() {
  await window.Clove.ready();
  const networkParams = {
    method: "POST",
    url: "[https://api.external-cloud-node.net/v1/ingest](https://api.external-cloud-node.net/v1/ingest)",
    data: { dataTimestamp: Date.now(), coreReading: 404 }
  };
  const res = await window.Clove.http.request(networkParams);
  console.log(`Response received with status code flag: ${res.status}`);
}
```

---

<a name="clovehttpget"></a>
#### `Clove.http.get(url, options)`
Shorthand alternative implementation to process a targeted HTTP GET request.
* **Arguments:** `url` *(String)*, `options` *(Object)* *(Optional metadata configuration blocks)*
* **Returns:** `Promise<Object>`
```javascript
async function fetchConfigPayload() {
  await window.Clove.ready();
  const res = await window.Clove.http.get("[https://api.clove.io/presets](https://api.clove.io/presets)", {});
  if (res.ok) {
    console.log("Configuration parameters matched:", res.body);
  }
}
```

---

<a name="clovehttppost"></a>
#### `Clove.http.post(url, data, options)`
Shorthand alternative implementation to process a targeted HTTP POST request.
* **Arguments:** `url` *(String)*, `data` *(Object)*, `options` *(Object)*
* **Returns:** `Promise<Object>`
```javascript
async function transmitNodeHeartbeat() {
  await window.Clove.ready();
  const res = await window.Clove.http.post("[https://api.clove.io/heartbeat](https://api.clove.io/heartbeat)", { status: "active" }, {});
  console.log(`Post response matching status flags: ${res.status}`);
}
```

---

<a name="clovehttpput"></a>
#### `Clove.http.put(url, data, options)`
Shorthand alternative implementation to process a targeted HTTP PUT data request.
* **Arguments:** `url` *(String)*, `data` *(Object)*, `options` *(Object)*
* **Returns:** `Promise<Object>`
```javascript
async function updateServerAsset() {
  await window.Clove.ready();
  const res = await window.Clove.http.put("[https://api.clove.io/device/0](https://api.clove.io/device/0)", { name: "Primary Node" }, {});
  console.log(`Put asset operation returned code: ${res.status}`);
}
```

---

<a name="clovehttppatch"></a>
#### `Clove.http.patch(url, data, options)`
Shorthand alternative implementation to process a targeted HTTP PATCH request.
* **Arguments:** `url` *(String)*, `data` *(Object)*, `options` *(Object)*
* **Returns:** `Promise<Object>`
```javascript
async function patchServerParam() {
  await window.Clove.ready();
  const res = await window.Clove.http.patch("[https://api.clove.io/device/0](https://api.clove.io/device/0)", { status: "standby" }, {});
  console.log(`Patch update code verified: ${res.status}`);
}
```

---

<a name="clovehttpdelete"></a>
#### `Clove.http.delete(url, options)`
Shorthand alternative implementation to process a targeted HTTP DELETE verification request.
* **Arguments:** `url` *(String)*, `options` *(Object)*
* **Returns:** `Promise<Object>`
```javascript
async function deleteStaleDevice() {
  await window.Clove.ready();
  const res = await window.Clove.http.delete("[https://api.clove.io/device/old](https://api.clove.io/device/old)", {});
  console.log(`Deletion response confirmed: ${res.status}`);
}
```

---

<a name="clovehttpsetheader"></a>
#### `Clove.http.setHeader(host, header, value)`
Registers default global headers for outgoing remote server pipeline calls.
* **Arguments:** `host` *(String)*, `header` *(String)*, `value` *(String)*
* **Returns:** `Promise<void>`
```javascript
async function injectStickySecurityToken() {
  await window.Clove.ready();
  await window.Clove.http.setHeader("api.clove.io", "X-Custom-Client-Auth", "SecureKey_99182");
  console.log("Global authentication header bound to target host layer.");
}
```

---

<a name="clovehttpsetdataserializer"></a>
#### `Clove.http.setDataSerializer(serializer)`
Updates underlying framework encoding rules for outgoing web requests.
* **Arguments:** `serializer` *(String)* — `"json" | "urlencoded" | "utf8" | "multipart"`
* **Returns:** `Promise<void>`
```javascript
async function changeSerializerFormatting() {
  await window.Clove.ready();
  await window.Clove.http.setDataSerializer("urlencoded");
  console.log("Outgoing transmission encoding rules changed to urlencoded standard formatting.");
}
```

---

### User Experience & Feedback

<a name="clovenotificationalert"></a>
#### `Clove.notification.alert(msg, title, btn)`
Launches native hardware-styled workspace warning popups with built-in runtime fallback loops.
* **Arguments:** `msg` *(String)*, `title` *(String)*, `btn` *(String)*
* **Returns:** `Promise<void>`
```javascript
async function notifySystemOverload() {
  await window.Clove.ready();
  await window.Clove.notification.alert(
    "Critical core temperature threshold exceeded!", 
    "Hardware Alarm", 
    "Acknowledge Danger"
  );
  console.log("User verified reading data warning alert wrapper popup layout.");
}
```

---

<a name="clovenotificationconfirm"></a>
#### `Clove.notification.confirm(msg, title, btns)`
Displays operational validation request paths with up to three distinct button selection markers.
* **Arguments:** `msg` *(String)*, `title` *(String)*, `btns` *(Array<String>)*
* **Returns:** `Promise<Number>` *(Returns 1-based index matching selected button position element arrays)*
```javascript
async function queryFirmwareFlash() {
  await window.Clove.ready();
  const responseIndex = await window.Clove.notification.confirm(
    "Proceed with updating the target controller firmware stack configuration?",
    "System Update",
    ["Begin Flash", "Abort Process"]
  );
  if (responseIndex === 1) {
    console.log("User authorized process path execution initialization routines.");
  }
}
```

---

<a name="clovenotificationprompt"></a>
#### `Clove.notification.prompt(msg, title, btns, defText)`
Launches native textual input capturing dialog panels.
* **Arguments:** `msg` *(String)*, `title` *(String)*, `btns` *(Array<String>)*, `defText` *(String)*
* **Returns:** `Promise<Object>` containing `{ buttonIndex: number, input1: string }`
```javascript
async function captureDeviceAlias() {
  await window.Clove.ready();
  const inputResult = await window.Clove.notification.prompt(
    "Please specify a localized deployment label index for this node asset:",
    "Device Setup",
    ["Assign", "Keep Default"],
    "Node-Alpha"
  );
  if (inputResult.buttonIndex === 1) {
    console.log(`User mapped configuration target label to entry: ${inputResult.input1}`);
  }
}
```

---

<a name="clovenotificationbeep"></a>
#### `Clove.notification.beep(times)`
Triggers physical audio diagnostic alerting chirps directly via native system speakers.
* **Arguments:** `times` *(Number)*
* **Returns:** `Promise<void>`
```javascript
async function chirpOnCompletion() {
  await window.Clove.ready();
  console.log("Sound alert triggered.");
  await window.Clove.notification.beep(2);
}
```

---

<a name="clovenotificationvibrate"></a>
#### `Clove.notification.vibrate(ms)`
Triggers physical haptic vibration pulses via device motor configurations.
* **Arguments:** `ms` *(Number)*
* **Returns:** `Promise<void>`
```javascript
async function pulseHapticWarning() {
  await window.Clove.ready();
  console.log("Pulsing hardware haptic motor array layers.");
  await window.Clove.notification.vibrate(450);
}
```

---

### Bluetooth Classic Serial (SPP)

<a name="clovebluetoothlist"></a>
#### `Clove.bluetooth.list()`
Maps established system-paired hardware peripheral devices matching standard legacy RFCOMM signatures.
* **Arguments:** None
* **Returns:** `Promise<Array<Object>>` containing list entries with `{ name: string, address: string, id: string, class: number }`
```javascript
async function scanPairedHardware() {
  await window.Clove.ready();
  const pairings = await window.Clove.bluetooth.list();
  pairings.forEach(dev => {
    console.log(`Paired connection entry target found: ${dev.name} [MAC: ${dev.address}]`);
  });
}
```

---

<a name="clovebluetoothdiscoverunpaired"></a>
#### `Clove.bluetooth.discoverUnpaired()`
Initiates an environmental radio discoverability scan for unbonded legacy endpoints.
* **Arguments:** None
* **Returns:** `Promise<Array<Object>>`
```javascript
async function searchForNewLegacyDevices() {
  await window.Clove.ready();
  console.log("Starting 10-second classic environmental discovery scan...");
  const newDevices = await window.Clove.bluetooth.discoverUnpaired();
  console.log(`Discovered ${newDevices.length} unbonded classic endpoints nearby.`);
}
```

---

<a name="clovebluetoothconnect"></a>
#### `Clove.bluetooth.connect(address)`
Establishes an active RFCOMM transmission line channel to a target legacy module.
* **Arguments:** `address` *(String)* (Target hardware MAC identifier)
* **Returns:** `Promise<void>`
```javascript
async function connectToSerialModule() {
  await window.Clove.ready();
  const targetMac = "00:11:22:33:44:55";
  try {
    await window.Clove.bluetooth.connect(targetMac);
    console.log(`Persistent RFCOMM serial stream link set up cleanly to target: ${targetMac}`);
  } catch (err) {
    console.error("Link assembly parameters failed to complete properly:", err);
  }
}
```

---

<a name="clovebluetoothdisconnect"></a>
#### `Clove.bluetooth.disconnect()`
Tears down active serial device pipeline tunnels.
* **Arguments:** None
* **Returns:** `Promise<void>`
```javascript
async function closeSerialConnection() {
  await window.Clove.ready();
  await window.Clove.bluetooth.disconnect();
  console.log("RFCOMM data channel closed.");
}
```

---

<a name="clovebluetoothwrite"></a>
#### `Clove.bluetooth.write(data)`
Transmits raw operational strings down active classic serialization pathways.
* **Arguments:** `data` *(String | ArrayBuffer | Uint8Array)*
* **Returns:** `Promise<void>`
```javascript
async function sendSerialCommand() {
  await window.Clove.ready();
  const commandText = "SYS_VAL_SET_MOTOR_RPM=4500\n";
  await window.Clove.bluetooth.write(commandText);
  console.log("String sequence dispatched across serial link channels.");
}
```

---

<a name="clovebluetoothread"></a>
#### `Clove.bluetooth.read()`
Pulls the current raw buffer string contents out of memory queues manually **(One-Time Read)**.
* **Arguments:** None
* **Returns:** `Promise<String>`
```javascript
async function readCurrentBufferSnapshot() {
  await window.Clove.ready();
  const immediateDataString = await window.Clove.bluetooth.read();
  console.log("Immediate unformatted queue buffer dump data snapshot:", immediateDataString);
}
```

---

<a name="clovebluetoothreaduntil"></a>
#### `Clove.bluetooth.readUntil(delimiter)`
Pulls data from memory buffer queues manually, blocking until a specific validation sequence or line break is met **(One-Time Read)**.
* **Arguments:** `delimiter` *(String)*
* **Returns:** `Promise<String>`
```javascript
async function fetchSingleTelemetryPacket() {
  await window.Clove.ready();
  console.log("Waiting for single transmission line verification wrapper...");
  const rawLineString = await window.Clove.bluetooth.readUntil("\n");
  console.log("One-time parsed data row confirmed:", rawLineString.trim());
}
```

---

<a name="clovebluetoothsubscribe"></a>
#### `Clove.bluetooth.subscribe(delimiter, callback)`
Attaches an ongoing automated observation loop listener to incoming stream data blocks **(Continuous Stream)**.
* **Arguments:** `delimiter` *(String)*, `callback` *(Function)* processing raw strings `(data) => void`
* **Returns:** `Promise<void>`
```javascript
async function monitorContinuousSerialStream() {
  await window.Clove.ready();
  console.log("Registering continuous event stream listener block...");
  await window.Clove.bluetooth.subscribe("\n", (incomingLine) => {
    const dataString = incomingLine.trim();
    console.log("Stream notification received:", dataString);
    document.getElementById("live-spp-readout").innerText = dataString;
  });
}
```

---

<a name="clovebluetoothunsubscribe"></a>
#### `Clove.bluetooth.unsubscribe()`
Detaches automated stream parsing callback observation frameworks.
* **Arguments:** None
* **Returns:** `Promise<void>`
```javascript
async function stopContinuousSerialMonitoring() {
  await window.Clove.ready();
  await window.Clove.bluetooth.unsubscribe();
  console.log("Continuous stream observer unlinked successfully.");
}
```

---

<a name="clovebluetoothisconnected"></a>
#### `Clove.bluetooth.isConnected()`
Assesses if an active operational link is maintained to a classic client accessory endpoint.
* **Arguments:** None
* **Returns:** `Promise<Boolean>`
```javascript
async function verifyConnectionState() {
  await window.Clove.ready();
  const linked = await window.Clove.bluetooth.isConnected();
  console.log(`Active legacy target connection integrity verified: ${linked}`);
}
```

---

<a name="clovebluetoothisenabled"></a>
#### `Clove.bluetooth.isEnabled()`
Queries if the device's physical legacy Bluetooth adapter engine radio is turned on.
* **Arguments:** None
* **Returns:** `Promise<Boolean>`
```javascript
async function checkRadioAdapterState() {
  await window.Clove.ready();
  const adapterActive = await window.Clove.bluetooth.isEnabled();
  if (!adapterActive) {
    console.log("Device adapter radio requires state modifications.");
  }
}
```

---

<a name="clovebluetoothenable"></a>
#### `Clove.bluetooth.enable()`
Triggers direct native host hardware adapter power state modification requests to activate the radio interface.
* **Arguments:** None
* **Returns:** `Promise<any>`
```javascript
async function demandRadioActivation() {
  await window.Clove.ready();
  console.log("Requesting platform adapter activation sequence guidelines...");
  await window.Clove.bluetooth.enable();
}
```

---

### Bluetooth Low Energy (GATT)

<a name="cloveblescan"></a>
#### `Clove.ble.scan(services, seconds)`
Scans the local environment for advertising BLE peripherals.
* **Arguments:** `services` *(Array<String>)* (Filter by service UUIDs, pass empty array `[]` for all), `seconds` *(Number)* (Scan duration)
* **Returns:** `Promise<Array<Object>>` containing targets with `{ name: string, id: string, rssi: number, advertising: any }`
```javascript
async function discoveryLowEnergyNodes() {
  await window.Clove.ready();
  console.log("Scanning for Bluetooth Low Energy advertisement markers...");
  const discoveredGattNodes = await window.Clove.ble.scan([], 5);
  discoveredGattNodes.forEach(node => {
    console.log(`Discovered BLE peripheral node: ${node.name || 'Unknown'} ID: ${node.id} Signal: ${node.rssi}dBm`);
  });
}
```

---

<a name="cloveblestopscan"></a>
#### `Clove.ble.stopScan()`
Halts active environmental BLE radio scanning execution before the countdown timer finishes.
* **Arguments:** None
* **Returns:** `Promise<void>`
```javascript
async function emergencyHaltBleScan() {
  await window.Clove.ready();
  await window.Clove.ble.stopScan();
  console.log("Active radio scanning sequence terminated.");
}
```

---

<a name="clovebleconnect"></a>
#### `Clove.ble.connect(id)`
Establishes a persistent connection route configuration pointing directly to a remote GATT server.
* **Arguments:** `id` *(String)* (Target system identifier or MAC index)
* **Returns:** `Promise<Object>` returning deep structural map objects listing discoverable services and characteristics descriptors.
```javascript
async function connectToGattServer() {
  await window.Clove.ready();
  const targetId = "F3:D2:C1:00:AA:BB";
  try {
    const topologyMap = await window.Clove.ble.connect(targetId);
    console.log("GATT handshake successful. Structural services verified:", topologyMap.services);
  } catch (err) {
    console.error("GATT handshake routine failure:", err);
  }
}
```

---

<a name="clovebledisconnect"></a>
#### `Clove.ble.disconnect(id)`
Tears down active persistent communication pathways linked to low energy GATT nodes.
* **Arguments:** `id` *(String)*
* **Returns:** `Promise<void>`
```javascript
async function terminateGattLink() {
  await window.Clove.ready();
  const targetId = "F3:D2:C1:00:AA:BB";
  await window.Clove.ble.disconnect(targetId);
  console.log("GATT pipeline disconnected cleanly.");
}
```

---

<a name="clovebleread"></a>
#### `Clove.ble.read(id, serviceUuid, characteristicUuid)`
Queries a specific characteristic descriptor value directly from a GATT server **(One-Time Read)**.
* **Arguments:** `id` *(String)*, `serviceUuid` *(String)*, `characteristicUuid` *(String)*
* **Returns:** `Promise<ArrayBuffer>` containing raw unformatted data chunks.
```javascript
async function fetchGattBatteryLevel() {
  await window.Clove.ready();
  const devId = "F3:D2:C1:00:AA:BB";
  
  const rawBytes = await window.Clove.ble.read(devId, "180F", "2A19");
  const view = new DataView(rawBytes);
  const batteryPct = view.getUint8(0);
  console.log(`Snapshot read matching Battery Characteristic data metrics: ${batteryPct}%`);
}
```

---

<a name="cloveblewrite"></a>
#### `Clove.ble.write(id, serviceUuid, characteristicUuid, data)`
Transmits configuration data blocks downstream to specific characteristic profiles, expecting an confirmation response code back.
* **Arguments:** `id` *(String)*, `serviceUuid` *(String)*, `characteristicUuid` *(String)*, `data` *(ArrayBuffer | Uint8Array)*
* **Returns:** `Promise<void>`
```javascript
async function writeGattControlState() {
  await window.Clove.ready();
  const devId = "F3:D2:C1:00:AA:BB";
  
  const commandBytes = new Uint8Array([0x01, 0xFF]); // Custom control logic codes
  await window.Clove.ble.write(devId, "180A", "2A57", commandBytes.buffer);
  console.log("GATT command array package processed with server acknowledgment.");
}
```

---

<a name="cloveblewritewithoutresponse"></a>
#### `Clove.ble.writeWithoutResponse(id, serviceUuid, characteristicUuid, data)`
Transmits high-speed commands downstream to specific target parameters without requesting acknowledgment loops back from the client.
* **Arguments:** `id` *(String)*, `serviceUuid` *(String)*, `characteristicUuid` *(String)*, `data` *(ArrayBuffer | Uint8Array)*
* **Returns:** `Promise<void>`
```javascript
async function pushFastBleStreamUpdate() {
  await window.Clove.ready();
  const devId = "F3:D2:C1:00:AA:BB";
  
  const fastBytes = new Uint8Array([0x42, 0x00]);
  await window.Clove.ble.writeWithoutResponse(devId, "180A", "2A57", fastBytes.buffer);
  console.log("High-frequency pipeline burst sent unchecked.");
}
```

---

<a name="cloveblestartnotification"></a>
#### `Clove.ble.startNotification(id, serviceUuid, characteristicUuid, callback)`
Subscribes to characteristic value notifications for real-time GATT descriptor updates **(Continuous Stream)**.
* **Arguments:** `id` *(String)*, `serviceUuid` *(String)*, `characteristicUuid` *(String)*, `callback` *(Function)* running data transformations structural routines via parameters `(rawBuffer) => void`
* **Returns:** `Promise<void>`
```javascript
async function subscribeToLivePulseRate() {
  await window.Clove.ready();
  const devId = "F3:D2:C1:00:AA:BB";
  
  await window.Clove.ble.startNotification(devId, "180D", "2A37", (incomingBuffer) => {
    const dataView = new DataView(incomingBuffer);
    const pulseCount = dataView.getUint8(1); // Custom offset map
    console.log(`Live telemetry pulse caught via continuous stream notification: ${pulseCount} BPM`);
    document.getElementById("live-pulse-ui").innerText = `${pulseCount} BPM`;
  });
}
```

---

<a name="cloveblestopnotification"></a>
#### `Clove.ble.stopNotification(id, serviceUuid, characteristicUuid)`
Tears down subscription routes listening to localized character modifications profiles.
* **Arguments:** `id` *(String)*, `serviceUuid` *(String)*, `characteristicUuid` *(String)*
* **Returns:** `Promise<void>`
```javascript
async function haltGattNotifications() {
  await window.Clove.ready();
  const devId = "F3:D2:C1:00:AA:BB";
  await window.Clove.ble.stopNotification(devId, "180D", "2A37");
  console.log("GATT modification update subscription routes disconnected cleanly.");
}
```

---

<a name="clovebleisenabled"></a>
#### `Clove.ble.isEnabled()`
Queries if the device's physical Bluetooth Low Energy adapter radio is turned on.
* **Arguments:** None
* **Returns:** `Promise<Boolean>`
```javascript
async function checkBleAdapterAvailability() {
  await window.Clove.ready();
  const bleActive = await window.Clove.ble.isEnabled();
  console.log(`Hardware platform BLE engine active validation parameter: ${bleActive}`);
}
```

---

### Wi-Fi Adapter Linkages

<a name="clovewifigetssid"></a>
#### `Clove.wifi.getSSID()`
Queries the naming assignment identifier of the local access point network link.
* **Arguments:** None
* **Returns:** `Promise<String>`
```javascript
async function readCurrentSsidSnapshot() {
  await window.Clove.ready();
  const activeSsid = await window.Clove.wifi.getSSID();
  console.log(`Current established network SSID name trace configuration: ${activeSsid}`);
}
```

---

<a name="clovewifigetip"></a>
#### `Clove.wifi.getIP()`
Queries the device's assigned local IPv4 address.
* **Arguments:** None
* **Returns:** `Promise<String>`
```javascript
async function readLocalIP() {
  await window.Clove.ready();
  const assignedIp = await window.Clove.wifi.getIP();
  console.log(`Local link transport IP address trace: ${assignedIp}`);
}
```

---

<a name="clovewifilist"></a>
#### `Clove.wifi.list()`
Scans surrounding airspace to map visible wireless access points **(One-Time Fetch)**.
* **Arguments:** None
* **Returns:** `Promise<Array<Object>>` listing elements containing `{ SSID: string, BSSID: string, level: number, capabilities: string }`
```javascript
async function scanLocalAps() {
  await window.Clove.ready();
  console.log("Scanning local airspace for wireless access networks...");
  const structuralNetworksList = await window.Clove.wifi.list();
  structuralNetworksList.forEach(net => {
    console.log(`Discovered Network: ${net.SSID} Signal Level: ${net.level}dBm`);
  });
}
```

---

<a name="clovewificonnect"></a>
#### `Clove.wifi.connect(ssid, pass, algo, hid)`
Forces network roaming handovers to connect the Android hardware to an external localized access point network.
* **Arguments:** `ssid` *(String)*, `pass` *(String)*, `algo` *(String — e.g. "WPA" | "WEP")*, `hid` *(Boolean — Hidden tracking settings flag)*
* **Returns:** `Promise<any>`
```javascript
async function bindToNodeHotspot() {
  await window.Clove.ready();
  try {
    console.log("Attempting hardware Wi-Fi handover to target hotspot...");
    await window.Clove.wifi.connect("Field_Node_AP_E9", "FactoryPass882", "WPA", false);
    console.log("Subnet network configuration handshake complete.");
  } catch (err) {
    console.error("Handover request parameters rejected by adapter hardware layer:", err);
  }
}
```

---

<a name="clovewifidisconnect"></a>
#### `Clove.wifi.disconnect()`
Termitances current interface link configurations safely from local target router gateways.
* **Arguments:** None
* **Returns:** `Promise<void>`
```javascript
async function severWifiConnection() {
  await window.Clove.ready();
  await window.Clove.wifi.disconnect();
  console.log("Wireless station link interface dropped manually.");
}
```

---

<a name="clovewifiisenabled"></a>
#### `Clove.wifi.isEnabled()`
Queries if the device's physical Wi-Fi network interface card module is active.
* **Arguments:** None
* **Returns:** `Promise<Boolean>`
```javascript
async function checkWifiAdapterState() {
  await window.Clove.ready();
  const wifiHardwareActive = await window.Clove.wifi.isEnabled();
  console.log(`Wi-Fi card activation confirmation verification flag: ${wifiHardwareActive}`);
}
```

---

### Wired Hardware USB Serial

<a name="cloveusbrequestpermission"></a>
#### `Clove.usb.requestPermission(options)`
Requests explicit system device handling access codes targeting hardware accessories attached via USB OTG lines.
* **Arguments:** `options` *(Object)* detailing interface configurations `{ baudRate: number, dataBits: number, stopBits: number, parity: number }`
* **Returns:** `Promise<any>`
```javascript
async function authorizeUsbAccess() {
  await window.Clove.ready();
  const serialParameters = { baudRate: 9600, dataBits: 8, stopBits: 1, parity: 0 };
  console.log("Requesting system permission handover flags for USB accessories...");
  await window.Clove.usb.requestPermission(serialParameters);
  console.log("USB accessory device permissions confirmed.");
}
```

---

<a name="cloveusbopen"></a>
#### `Clove.usb.open(options)`
Opens direct execution tunnels tracking standard hardware setups linked to physical USB serial interface boards.
* **Arguments:** `options` *(Object)* detailing interface configurations `{ baudRate: number, dataBits: number, stopBits: number, parity: number }`
* **Returns:** `Promise<any>`
```javascript
async function initializeUsbLink() {
  await window.Clove.ready();
  const serialParameters = { baudRate: 9600, dataBits: 8, stopBits: 1, parity: 0 };
  await window.Clove.usb.open(serialParameters);
  console.log("Wired OTG communication pathways mounted and initialized.");
}
```

---

<a name="cloveusbclose"></a>
#### `Clove.usb.close()`
Tears down active persistent communication pathways linked to physical USB interfaces.
* **Arguments:** None
* **Returns:** `Promise<void>`
```javascript
async function shutdownUsbPort() {
  await window.Clove.ready();
  await window.Clove.usb.close();
  console.log("Wired OTG asset link deactivated cleanly.");
}
```

---

<a name="cloveusbwrite"></a>
#### `Clove.usb.write(data)`
Transmits raw operational strings straight across physical hardware lines.
* **Arguments:** `data` *(String)*
* **Returns:** `Promise<void>`
```javascript
async function pushUsbCommand() {
  await window.Clove.ready();
  const hardwareInstruction = "SYS_REBOOT_CONTROLLER_CHIP_NOW\n";
  await window.Clove.usb.write(hardwareInstruction);
  console.log("Instruction bytes processed by native USB port controllers.");
}
```

---

<a name="cloveusbread"></a>
#### `Clove.usb.read(callback)`
Attaches an execution handle loop listener to read characters arriving across physical hardware connections **(Continuous Stream)**.
* **Arguments:** `callback` *(Function)* running payload transformations data structures `(rawBufferArray) => void`
* **Returns:** `Promise<any>`
```javascript
async function readContinuousUsbStream() {
  await window.Clove.ready();
  console.log("Binding continuous event streaming callback logic to active USB interface port elements...");
  await window.Clove.usb.read((incomingChunk) => {
    const stringDecoder = new TextDecoder("utf-8");
    const readableText = stringDecoder.decode(incomingChunk);
    console.log("Wired USB character segment caught:", readableText);
    document.getElementById("usb-console").value += readableText;
  });
}
```

---

### Native Media Capture

<a name="clovecameragetpicture"></a>
#### `Clove.camera.getPicture(options)`
Launches the device's native camera viewfinder frame layout to capture raw images.
* **Arguments:** `options` *(Object)* containing `{ quality: number, destinationType: number, sourceType: number }`
* **Returns:** `Promise<String>` containing base64 string lines data sets or local system file locations.
```javascript
async function runCameraCapture() {
  await window.Clove.ready();
  const photoConfig = { quality: 75, destinationType: 0, sourceType: 1 };
  
  try {
    const capturedStringData = await window.Clove.camera.getPicture(photoConfig);
    document.getElementById("node-preview-pane").src = `data:image/jpeg;base64,${capturedStringData}`;
    console.log("Image data rendering updated accurately.");
  } catch (err) {
    console.log("User terminated camera layout context view sequence early.", err);
  }
}
```

---

### Spatial Geolocation

<a name="clovegeolocationgetcurrentposition"></a>
#### `Clove.geolocation.getCurrentPosition(options)`
Queries satellite position tracking engines for a single coordinate fix **(One-Time Snapshot)**.
* **Arguments:** `options` *(Object)* matching standard specifications configuration patterns `{ enableHighAccuracy: boolean, timeout: number }`
* **Returns:** `Promise<Object>` detailing position attributes containing `{ coords: { latitude: number, longitude: number, accuracy: number, altitude: number } }`
```javascript
async function sampleCurrentLocation() {
  await window.Clove.ready();
  const positioningParams = { enableHighAccuracy: true, timeout: 6000 };
  
  try {
    const geographicFix = await window.Clove.geolocation.getCurrentPosition(positioningParams);
    console.log(`GPS Location confirmation: Lat ${geographicFix.coords.latitude} Long ${geographicFix.coords.longitude}`);
  } catch (err) {
    console.error("GPS hardware timed out or turned off:", err);
  }
}
```

---

<a name="clovegeolocationwatchposition"></a>
#### `Clove.geolocation.watchPosition(callback, options)`
Binds monitoring tracking handles to log spatial relocation vectors continuously as the device moves **(Continuous Stream)**.
* **Arguments:** `callback` *(Function)* running spatial transformations routines `(positionData) => void`, `options` *(Object)*
* **Returns:** `Promise<Number>` returning tracking identification tokens used for unlinking listeners later.
```javascript
let localTrackingToken = null;

async function trackMovementContinuously() {
  await window.Clove.ready();
  console.log("Activating continuous geolocation tracking pipeline...");
  
  localTrackingToken = await window.Clove.geolocation.watchPosition((liveLocationPacket) => {
    const lat = liveLocationPacket.coords.latitude;
    const lon = liveLocationPacket.coords.longitude;
    console.log(`Continuous tracking update: Lat ${lat} | Lon ${lon}`);
    document.getElementById("live-coordinates-ui").innerText = `${lat.toFixed(4)}, ${lon.toFixed(4)}`;
  }, { enableHighAccuracy: true });
}
```

---

<a name="clovegeolocationclearwatch"></a>
#### `Clove.geolocation.clearWatch(watchId)`
Unlinks active stream observation frameworks listening to physical location variations parameters.
* **Arguments:** `watchId` *(Number)* (Tracking confirmation token code)
* **Returns:** `Promise<void>`
```javascript
async function haltAssetTracking() {
  await window.Clove.ready();
  if (localTrackingToken !== null) {
    await window.Clove.geolocation.clearWatch(localTrackingToken);
    localTrackingToken = null;
    console.log("Continuous tracking loop stopped.");
  }
}
```

---

### MQTT Protocol Engine

<a name="clovemqttconnect"></a>
#### `Clove.mqtt.connect(options)`
Establishes data transmission tunnels targeting remote server message distribution hubs.
* **Arguments:** `options` *(Object)* containing parameter keys like `{ host: string, port: number, clientId: string, username?: string, password?: string }`
* **Returns:** `Promise<any>`
```javascript
async function linkToMqttBroker() {
  await window.Clove.ready();
  const brokerSettings = {
    host: "broker.hivemq.com",
    port: 1883,
    clientId: "clove_dashboard_client_0x991"
  };
  
  try {
    console.log("Initiating native MQTT link handshake parameters...");
    await window.Clove.mqtt.connect(brokerSettings);
    console.log("MQTT network tracking links constructed successfully.");
  } catch (err) {
    console.error("MQTT broker connection failure:", err);
  }
}
```

---

<a name="clovemqttdisconnect"></a>
#### `Clove.mqtt.disconnect()`
Tears down persistent message delivery setups safely from target distribution tracking platforms.
* **Arguments:** None
* **Returns:** `Promise<void>`
```javascript
async function severMqttBrokerLink() {
  await window.Clove.ready();
  await window.Clove.mqtt.disconnect();
  console.log("MQTT network transmission pipes deactivated cleanly.");
}
```

---

<a name="clovemqttpublish"></a>
#### `Clove.mqtt.publish(topic, payload, options)`
Publishes data records downstream onto explicit tracking topic parameters.
* **Arguments:** `topic` *(String)*, `payload` *(String)*, `options` *(Object — Optional settings block e.g., `{ qos: number, retain: boolean }`)*
* **Returns:** `Promise<any>`
```javascript
async function broadcastSensorMetrics() {
  await window.Clove.ready();
  const alertTopic = "factory/assembly/line_1";
  const monitoringData = JSON.stringify({ state: "operational", conveyorSpeed: "nominal" });
  
  await window.Clove.mqtt.publish(alertTopic, monitoringData, { qos: 1 });
  console.log("Payload data set dispatched across MQTT network topic targets.");
}
```

---

<a name="clovemqttsubscribe"></a>
#### `Clove.mqtt.subscribe(topic, callback)`
Attaches event observation listeners to specific incoming communication channels **(Continuous Stream)**.
* **Arguments:** `topic` *(String)*, `callback` *(Function)* running incoming data string actions mapping loops `(topic, payload) => void`
* **Returns:** `Promise<any>`
```javascript
async function listenToGlobalAlerts() {
  await window.Clove.ready();
  const targetChannel = "factory/alarms/+/critical";
  
  console.log(`Subscribing to continuous channel messages stream on: ${targetChannel}`);
  await window.Clove.mqtt.subscribe(targetChannel, (topicName, incomingMessageText) => {
    console.log(`Continuous message caught on [${topicName}]:`, incomingMessageText);
    document.getElementById("live-mqtt-alert").innerText = incomingMessageText;
  });
}
```

---

<a name="clovemqttunsubscribe"></a>
#### `Clove.mqtt.unsubscribe(topic)`
Removes subscription tracking profiles from designated broker paths.
* **Arguments:** `topic` *(String)*
* **Returns:** `Promise<any>`
```javascript
async function dropChannelSubscription() {
  await window.Clove.ready();
  const staleChannel = "factory/alarms/+/critical";
  await window.Clove.mqtt.unsubscribe(staleChannel);
  console.log("MQTT topic observation framework unlinked successfully.");
}
```

---

## 🤖 AI Developer Prompt Template

Copy and paste the prompt block below into any Large Language Model (ChatGPT, Claude, Gemini) along with your dashboard UI idea. This sets up the AI with the complete context required to generate flawless vanilla HTML/CSS/JS code that integrates directly with the Clove framework.

```text
You are an expert frontend software engineer specialized in building custom user interface templates for the Clove OS runtime framework. Clove is an Android application acting as a native IoT client sandbox. It lets developers upload bundled frontend assets (HTML, CSS, JS) and runs them inside an optimized container.

The runtime eliminates standard browser CORS restrictions by routing network requests via native proxy layers, and abstracts native Android capabilities (Bluetooth, BLE, USB Serial, Wi-Fi, Filesystem) into an asynchronous JavaScript API bridge (`window.Clove`).

### CRITICAL RULES:
1. DO NOT assume the presence of packaging tools, module bundlers, or package managers (No Webpack, Vite, npm, React, or Vue). Write clean, standalone ES6+ JavaScript, CSS3, and HTML5.
2. Every hardware interaction must use `async/await` syntax wrapped in robust `try/catch` blocks.
3. Always await framework initialization before running native functions: `await window.Clove.ready();`.
4. Distinguish clearly between ONE-TIME DATA READS (e.g., `device.info()`, `ble.read()`, `bluetooth.readUntil()`, `geolocation.getCurrentPosition()`) and CONTINUOUS DATA STREAMS (e.g., `connectIoT()`, `bluetooth.subscribe()`, `ble.startNotification()`, `geolocation.watchPosition()`).
5. NEVER mention or reference "Cordova" or any third-party wrapper plugins.

### COMPLETE GLOBAL API REFERENCE & METHOD SIGNATURES:

#### 1. Core & Initialization
* `Clove.ready(): Promise<void>` -> Blocks script execution until the native bridge is fully active.
* `Clove.connectIoT(config: {type: 'ble'|'bluetooth'|'usb'|'mqtt'|'http', target: string, serviceUuid?: string, characteristicUuid?: string, delimiter?: string, pollInterval?: number}, callback: (data: string) => void): Promise<void>` -> Initiates high-level micro-pipelines. Callback handles data updates continuously.

#### 2. Device & Network Diagnostics
* `Clove.device.info(): Promise<{ manufacturer: string, model: string, platform: string, version: string, uuid: string }>`
* `Clove.network.status(): Promise<{ online: boolean, type: string }>`

#### 3. Persistent State Storage
* `Clove.storage.get(key: string): Promise<any>`
* `Clove.storage.set(key: string, value: any): Promise<void>` -> Automatically serializes arrays and objects to JSON.
* `Clove.storage.remove(key: string): Promise<void>`
* `Clove.storage.clear(): Promise<void>`

#### 4. Sandboxed File System
* `Clove.file.write(path: string, data: string | Object): Promise<any>`
* `Clove.file.read(path: string, options?: { mode: 'text' | 'json' }): Promise<any>`
* `Clove.file.exists(path: string): Promise<boolean>`
* `Clove.file.remove(path: string): Promise<any>`
* `Clove.file.open(path: string, mimeType: string): Promise<any>` -> Triggers native system intent viewing window handler.
* `Clove.file.getAssetURL(path: string): Promise<string>` -> Converts sandboxed file paths into a web-safe URL string for visual element binding.

#### 5. Enterprise Proxy HTTP Networking
* `Clove.http.request(options: { method: 'GET'|'POST'|'PUT'|'PATCH'|'DELETE', url: string, data?: any, headers?: any }): Promise<{ ok: boolean, status: number, body: any, headers: any }>`
* `Clove.http.get(url: string, options?: any): Promise<{ ok: boolean, status: number, body: any, headers: any }>`
* `Clove.http.post(url: string, data: any, options?: any): Promise<{ ok: boolean, status: number, body: any, headers: any }>`
* `Clove.http.put(url: string, data: any, options?: any): Promise<{ ok: boolean, status: number, body: any, headers: any }>`
* `Clove.http.patch(url: string, data: any, options?: any): Promise<{ ok: boolean, status: number, body: any, headers: any }>`
* `Clove.http.delete(url: string, options?: any): Promise<{ ok: boolean, status: number, body: any, headers: any }>`
* `Clove.http.setHeader(host: string, headerName: string, value: string): Promise<void>` -> Maps default header parameters to a specified host context.
* `Clove.http.setDataSerializer(serializer: 'json' | 'urlencoded' | 'utf8' | 'multipart'): Promise<void>`

#### 6. User Experience & Native Feedback
* `Clove.notification.alert(msg: string, title: string, buttonLabel: string): Promise<void>`
* `Clove.notification.confirm(msg: string, title: string, buttonLabels: string[]): Promise<number>` -> Returns 1-based index matching selected button layout mapping.
* `Clove.notification.prompt(msg: string, title: string, buttonLabels: string[], defaultText: string): Promise<{ buttonIndex: number, input1: string }>` -> Maps button triggers alongside string configurations text input fields parameters.
* `Clove.notification.beep(times: number): Promise<void>`
* `Clove.notification.vibrate(ms: number): Promise<void>`

#### 7. Bluetooth Classic Serial (SPP)
* `Clove.bluetooth.list(): Promise<Array<{ name: string, address: string, id: string, class: number }>>` -> Lists paired legacy classic device profiles.
* `Clove.bluetooth.discoverUnpaired(): Promise<Array<{ name: string, address: string }>>`
* `Clove.bluetooth.connect(address: string): Promise<void>` -> Initiates communication link mapping over standard RFCOMM channels.
* `Clove.bluetooth.write(data: string | ArrayBuffer | Uint8Array): Promise<void>`
* `Clove.bluetooth.read(): Promise<string>` -> One-time request reading whatever unformatted queue text is present in the buffer at that millisecond.
* `Clove.bluetooth.readUntil(delimiter: string): Promise<string>` -> One-time request reading data blocking execution loops until delimiter configuration matches.
* `Clove.bluetooth.subscribe(delimiter: string, callback: (data: string) => void): Promise<void>` -> CONTINUOUS DATA STREAM. Fires automatically on matching delimiter tokens.
* `Clove.bluetooth.unsubscribe(): Promise<void>`
* `Clove.bluetooth.isConnected(): Promise<boolean>`
* `Clove.bluetooth.isEnabled(): Promise<boolean>`
* `Clove.bluetooth.enable(): Promise<any>` -> Prompts native OS platform dialog handling requests to turn on system adapter radio elements.
* `Clove.bluetooth.disconnect(): Promise<void>`

#### 8. Bluetooth Low-Energy (GATT)
* `Clove.ble.scan(services: string[], durationSeconds: number): Promise<Array<{ name: string, id: string, rssi: number, advertising: any }>>`
* `Clove.ble.stopScan(): Promise<void>`
* `Clove.ble.connect(id: string): Promise<{ services: string[], characteristics: Array<{ service: string, characteristic: string, properties: string[] }> }>`
* `Clove.ble.disconnect(id: string): Promise<void>`
* `Clove.ble.read(id: string, serviceUuid: string, characteristicUuid: string): Promise<ArrayBuffer>` -> One-time request parameters read.
* `Clove.ble.write(id: string, serviceUuid: string, characteristicUuid: string, data: ArrayBuffer): Promise<void>` -> Expects device acknowledgment feedback.
* `Clove.ble.writeWithoutResponse(id: string, serviceUuid: string, characteristicUuid: string, data: ArrayBuffer): Promise<void>` -> High speed write, skips verification tracking loop states.
* `Clove.ble.startNotification(id: string, serviceUuid: string, characteristicUuid: string, callback: (data: ArrayBuffer) => void): Promise<void>` -> CONTINUOUS DATA STREAM.
* `Clove.ble.stopNotification(id: string, serviceUuid: string, characteristicUuid: string): Promise<void>`
* `Clove.ble.isEnabled(): Promise<boolean>`

#### 9. Wi-Fi Adapter Linkages
* `Clove.wifi.getSSID(): Promise<string>`
* `Clove.wifi.getIP(): Promise<string>`
* `Clove.wifi.list(): Promise<Array<{ SSID: string, BSSID: string, level: number, capabilities: string }>>` -> Returns list layout details surrounding current area airspace hotspots maps.
* `Clove.wifi.connect(ssid: string, password: string, algorithm: 'WPA'|'WEP'|'NONE', isHidden: boolean): Promise<any>`
* `Clove.wifi.disconnect(): Promise<void>`
* `Clove.wifi.isEnabled(): Promise<boolean>`

#### 10. Wired OTG USB Serial
* `Clove.usb.requestPermission(options: { baudRate: number, dataBits: number, stopBits: number, parity: number }): Promise<any>`
* `Clove.usb.open(options: { baudRate: number, dataBits: number, stopBits: number, parity: number }): Promise<any>`
* `Clove.usb.write(data: string): Promise<void>`
* `Clove.usb.read(callback: (data: Uint8Array) => void): Promise<any>` -> CONTINUOUS DATA STREAM. Loop handler reading incoming wired hardware buffer states.
* `Clove.usb.close(): Promise<void>`

#### 11. Native Media Capture
* `Clove.camera.getPicture(options: { quality: number, destinationType: 0 | 1, sourceType: 1 }): Promise<string>` -> destinationType 0 returns raw base64 string, 1 returns system storage local file path.

#### 12. Spatial Geolocation
* `Clove.geolocation.getCurrentPosition(options?: { enableHighAccuracy?: boolean, timeout?: number }): Promise<{ coords: { latitude: number, longitude: number, accuracy: number, altitude: number, speed: number | null } }>` -> One-time fix snapshot tracking mapping logic.
* `Clove.geolocation.watchPosition(callback: (position: { coords: { latitude: number, longitude: number, accuracy: number, speed: number | null } }) => void, options?: { enableHighAccuracy?: boolean }): Promise<number>` -> CONTINUOUS DATA STREAM. Returns watchId token metrics.
* `Clove.geolocation.clearWatch(watchId: number): Promise<void>`

#### 13. MQTT Protocol Messaging Engine
* `Clove.mqtt.connect(options: { host: string, port: number, clientId: string, username?: string, password?: string }): Promise<any>`
* `Clove.mqtt.publish(topic: string, message: string, options?: { qos?: 0 | 1 | 2, retain?: boolean }): Promise<any>`
* `Clove.mqtt.subscribe(topic: string, callback: (topic: string, payload: string) => void): Promise<any>` -> CONTINUOUS DATA STREAM. Incoming message listener block.
* `Clove.mqtt.unsubscribe(topic: string): Promise<any>`
* `Clove.mqtt.disconnect(): Promise<void>`

Acknowledge these exact API definitions, parameters, and return type definitions, and generate the complete code suite (HTML/CSS/JS) for my specific dashboard request described below.
```
