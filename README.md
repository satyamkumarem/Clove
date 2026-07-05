<div align="center">
  <p>
    <!-- <img alt="clovebanner" src="https://github.com/user-attachments/assets/9678a955-59b1-464d-81c3-beda0f01dd13"  width="546"/> -->
    <img alt="clovebanner" src="https://github.com/user-attachments/assets/578766fe-3987-4d89-aa7b-800bc44e8e0f" width="546"/>

  </p>
  <br />
	<p>
		<a href="https://github.com/satyamkumarem/Clove/releases"><img src="https://img.shields.io/github/v/release/satyamkumarem/Clove?color=5865F2&label=version" alt="version" /></a>
        <a href="https://github.com/satyamkumarem/Clove/releases"><img src="https://img.shields.io/badge/downloads-0_total-2ea44f?color=5865F2"/></a>
	    <a href="https://github.com/satyamkumarem/Clove"><img src="https://img.shields.io/badge/tests-passing-2ea44f?logo=github&logoColor=ffffff" alt="tests" /></a>
	    <a href="https://github.com/satyamkumarem/Clove/commits/main"><img alt="Last commit" src="https://img.shields.io/github/last-commit/satyamkumarem/Clove?logo=github&logoColor=ffffff" /></a>
      <img src="https://img.shields.io/badge/Platform-Android-3DDC84?logo=android&logoColor=white" alt="Platform: Android" />
	</p>
	<p>
		<a href="https://www.android.com"><img src="https://github.com/user-attachments/assets/07a7ddc7-5ab8-46b4-b472-ec344b0d44b6" alt="Powered by Android" height="40" /></a>
		<a href="https://euome.com"><img src="https://github.com/user-attachments/assets/0fcfb862-98a8-4680-aaf2-4b191719c54d" alt="Powered by Euome" height="40" /></a>
	</p>
	<br/>
</div>

## About

Clove is an Android framework that lets you build native mobile apps using simple web code just HTML, CSS, and JavaScript. Instead of spending months learning complex Android development with Java or Kotlin, you just build your custom interface like a basic website, load it into Clove, and the framework automatically sets up the backend and runs it like a native application. It even handles native networking by removing annoying browser blocks like CORS (which usually stop web code from talking directly to external hardware or local servers). It's an ideal environment for testing user interfaces and controlling embedded systems, with an upcoming feature that will let you bundle your final project into a standalone `.apk` file you can distribute.

### Core Features
- **AI-Assisted Dashboard Building:** You don't need to be an expert developer to get started. Clove provides a pre-configured prompt template that you can copy and paste into an AI assistant, allowing absolute beginners to generate fully functional dashboards just by describing what they need in plain English.
- **Plug-and-Play Hardware Connectivity:** Connecting your app interface to embedded systems is incredibly easy. Clove includes ready-to-use modules that handle the low-level communication logic for Bluetooth Classic, BLE, Wi-Fi, and USB serial devices, so you can safely send and stream data with a few lines of clean JavaScript.


## Installation & Setup

Steps to install Clove application on your device and launch your custom dashboard using these steps:

> 1. **Download the APK:** Go to the [Latest Releases](../../releases/latest) page and download the most recent `.apk` file directly to your Android device.
> 2. **Install the App:** Open the downloaded file to begin installation. If prompted by Android, you will need to allow installations from **"Unknown Sources"** in your system security settings.
> 3. **Grant Permissions:** Launch Clove for the first time and grant the requested system permissions so the application can properly perform its functions.
> 4. **Deploy Your Dashboard:** Compress your frontend assets into a standard `.zip` file (make sure your main HTML entry point file is named `index.html`). Upload this zip file inside the Clove application to load your dashboard permanently.

**Updating or Swapping Dashboards:** Because Clove adopts your dashboard permanently, you can clear it out to upload a new design by either clearing the app's data (`Settings > Apps > Clove > Storage > Clear Data`) or by completely reinstalling the application.



## Predefined Methods

#### Root Level Core Methods
* [`Clove.ready()`](methods/core/ready.md)
* [`Clove.connectIoT(config, callback)`](methods/core/connect-iot.md)

#### Clove.device (System Analytics)
* [`Clove.device.info()`](methods/device/info.md)

#### Clove.network (Connectivity Mapping)
* [`Clove.network.status()`](methods/network/status.md)

#### Clove.storage (Local Storage)
* [`Clove.storage.get(key)`](methods/storage/get.md)
* [`Clove.storage.set(key, value)`](methods/storage/set.md)
* [`Clove.storage.remove(key)`](methods/storage/remove.md)
* [`Clove.storage.clear()`](methods/storage/clear.md)

#### Clove.file (Sandbox File System)
* [`Clove.file.write(path, data)`](methods/file/write.md)
* [`Clove.file.read(path, options)`](methods/file/read.md)
* [`Clove.file.exists(path)`](methods/file/exists.md)
* [`Clove.file.remove(path)`](methods/file/remove.md)
* [`Clove.file.open(path, mimeType)`](methods/file/open.md)
* [`Clove.file.getAssetURL(path)`](methods/file/get-asset-url.md)

#### Clove.http (Network Pipelines)
* [`Clove.http.request(options)`](methods/http/request.md)
* [`Clove.http.get(url, options)`](methods/http/get.md)
* [`Clove.http.post(url, data, options)`](methods/http/post.md)
* [`Clove.http.put(url, data, options)`](methods/http/put.md)
* [`Clove.http.patch(url, data, options)`](methods/http/patch.md)
* [`Clove.http.delete(url, options)`](methods/http/delete.md)
* [`Clove.http.setHeader(host, header, value)`](methods/http/set-header.md)
* [`Clove.http.setDataSerializer(serializer)`](methods/http/set-data-serializer.md)

#### Clove.notification (User Experience Feedback)
* [`Clove.notification.alert(msg, title, btn)`](methods/notification/alert.md)
* [`Clove.notification.confirm(msg, title, btns)`](methods/notification/confirm.md)
* [`Clove.notification.prompt(msg, title, btns, defText)`](methods/notification/prompt.md)
* [`Clove.notification.beep(times)`](methods/notification/beep.md)
* [`Clove.notification.vibrate(ms)`](methods/notification/vibrate.md)

#### Clove.bluetooth (Bluetooth Classic SPP)
* [`Clove.bluetooth.list()`](methods/bluetooth/list.md)
* [`Clove.bluetooth.discoverUnpaired()`](methods/bluetooth/discover-unpaired.md)
* [`Clove.bluetooth.connect(address)`](methods/bluetooth/connect.md)
* [`Clove.bluetooth.disconnect()`](methods/bluetooth/disconnect.md)
* [`Clove.bluetooth.write(data)`](methods/bluetooth/write.md)
* [`Clove.bluetooth.read()`](methods/bluetooth/read.md)
* [`Clove.bluetooth.readUntil(delimiter)`](methods/bluetooth/read-until.md)
* [`Clove.bluetooth.subscribe(delimiter, callback)`](methods/bluetooth/subscribe.md)
* [`Clove.bluetooth.unsubscribe()`](methods/bluetooth/unsubscribe.md)
* [`Clove.bluetooth.isConnected()`](methods/bluetooth/is-connected.md)
* [`Clove.bluetooth.isEnabled()`](methods/bluetooth/is-enabled.md)
* [`Clove.bluetooth.enable()`](methods/bluetooth/enable.md)

#### Clove.ble (Bluetooth Low Energy GATT)
* [`Clove.ble.scan(services, seconds)`](methods/ble/scan.md)
* [`Clove.ble.stopScan()`](methods/ble/stop-scan.md)
* [`Clove.ble.connect(id)`](methods/ble/connect.md)
* [`Clove.ble.disconnect(id)`](methods/ble/disconnect.md)
* [`Clove.ble.read(id, serviceUuid, characteristicUuid)`](methods/ble/read.md)
* [`Clove.ble.write(id, serviceUuid, characteristicUuid, data)`](methods/ble/write.md)
* [`Clove.ble.writeWithoutResponse(id, serviceUuid, characteristicUuid, data)`](methods/ble/write-without-response.md)
* [`Clove.ble.startNotification(id, serviceUuid, characteristicUuid, callback)`](methods/ble/start-notification.md)
* [`Clove.ble.stopNotification(id, serviceUuid, characteristicUuid)`](methods/ble/stop-notification.md)
* [`Clove.ble.isEnabled()`](methods/ble/is-enabled.md)

#### Clove.wifi (Wi-Fi Infrastructure Linkages)
* [`Clove.wifi.getSSID()`](methods/wifi/get-ssid.md)
* [`Clove.wifi.getIP()`](methods/wifi/get-ip.md)
* [`Clove.wifi.list()`](methods/wifi/list.md)
* [`Clove.wifi.connect(ssid, pass, algo, hid)`](methods/wifi/connect.md)
* [`Clove.wifi.disconnect()`](methods/wifi/disconnect.md)
* [`Clove.wifi.isEnabled()`](methods/wifi/is-enabled.md)

#### Clove.usb (Wired Serial Interfaces)
* [`Clove.usb.requestPermission(options)`](methods/usb/request-permission.md)
* [`Clove.usb.open(options)`](methods/usb/open.md)
* [`Clove.usb.close()`](methods/usb/close.md)
* [`Clove.usb.write(data)`](methods/usb/write.md)
* [`Clove.usb.read(callback)`](methods/usb/read.md)

#### Clove.camera (Image Captures)
* [`Clove.camera.getPicture(options)`](methods/camera/get-picture.md)

#### Clove.geolocation (Spatial Tracking)
* [`Clove.geolocation.getCurrentPosition(options)`](methods/geolocation/get-current-position.md)
* [`Clove.geolocation.watchPosition(callback, options)`](methods/geolocation/watch-position.md)
* [`Clove.geolocation.clearWatch(watchId)`](methods/geolocation/clear-watch.md)

#### Clove.mqtt (Asynchronous Pub/Sub Client)
* [`Clove.mqtt.connect(options)`](methods/mqtt/connect.md)
* [`Clove.mqtt.disconnect()`](methods/mqtt/disconnect.md)
* [`Clove.mqtt.publish(topic, payload, options)`](methods/mqtt/publish.md)
* [`Clove.mqtt.subscribe(topic, callback, options)`](methods/mqtt/subscribe.md)
* [`Clove.mqtt.unsubscribe(topic)`](methods/mqtt/unsubscribe.md)



## Contributing & Support

We welcome anyone to raise an issue, but please check the documentation and search existing entries first to ensure it's not a duplicate. Right now, we are actively looking for compatibility feedback from people testing Clove with various embedded systems and development boards.

- **Compatibility Feedback:** Let us know how our predefined methods perform with your specific hardware (such as an ESP32, Arduino, or Raspberry Pi).
- **Get Support:** Connect on LinkedIn or email me at [me@euome.com](mailto:me@euome.com).



## Prompt: Teaching AI to Build Clove Dashboards

Copy and paste the prompt block below into any Large Language Model (ChatGPT, Claude, Gemini) along with your dashboard UI idea. This sets up the AI with the complete context required to generate flawless vanilla HTML/CSS/JS code that integrates directly with the Clove framework.

```text
You are an expert frontend software engineer specialized in building custom user interface templates for the Clove OS runtime framework. Clove is an Android application acting as a native IoT client sandbox. It lets developers upload bundled frontend assets (HTML, CSS, JS) and runs them inside an optimized container.

The runtime eliminates standard browser CORS restrictions by routing network requests via native proxy layers, and abstracts native Android capabilities (Bluetooth, BLE, USB Serial, Wi-Fi, Filesystem) into an asynchronous JavaScript API bridge (`window.Clove`).

### CRITICAL RULES:
1. DO NOT assume the presence of packaging tools, module bundlers, or package managers (No Webpack, Vite, npm, React, or Vue). Write clean, standalone ES6+ JavaScript, CSS3, and HTML5.
2. Every hardware interaction must use `async/await` syntax wrapped in robust `try/catch` blocks.
3. Always await framework initialization before running native functions: `await window.Clove.ready();`.
4. Distinguish clearly between ONE-TIME DATA READS (e.g., `device.info()`, `ble.read()`, `bluetooth.readUntil()`, `geolocation.getCurrentPosition()`) and CONTINUOUS DATA STREAMS (e.g., `connectIoT()`, `bluetooth.subscribe()`, `ble.startNotification()`, `geolocation.watchPosition()`).
5. NEVER mention or reference any third-party wrapper plugins.

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
