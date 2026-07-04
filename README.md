# Clove OS: Smart UI Sandbox Framework
### Developer Interface & API Reference Guide

---

## 📖 Application Overview

The **Clove Android Application** is a client-side runtime environment engineered for IoT interaction, data visualization, and hardware control. Instead of relying on rigid, pre-built dashboard architectures, Clove provides an open-ended presentation layer sandbox.

### How the Ecosystem Works:
1. **Custom UI Provisioning:** Developers bundle standard web assets (`index.html`, `styles.css`, JS modules, and static graphics) into a `.zip` file and upload it directly to the Clove app.
2. **Native Abstraction Virtualization:** The app renders these assets inside a secure sandbox viewport.
3. **Zero Native Code Required:** The runtime intercepts execution requests via the global window bridge (`window.Clove`), allowing your JavaScript to natively control hardware sensors, Bluetooth, USB serial, and file systems without writing a single line of Kotlin or Java.

---

## 🔗 Interactive API Reference

* [Framework Core Initialization](#1-framework-core-initialization)
* [Unified IoT Gateway (Stream vs. Polling)](#2-unified-iot-gateway)
* [Device & Network Diagnostics](#3-device--network-diagnostics)
* [Persistent State Storage](#4-persistent-state-storage)
* [Sandboxed File System](#5-sandboxed-file-system)
* [Enterprise HTTP Networking](#6-enterprise-http-networking)
* [User Experience & Feedback Modals](#7-user-experience--feedback)
* [Bluetooth Classic Serial (SPP)](#8-bluetooth-classic-serial-spp)
* [Bluetooth Low Energy (GATT)](#9-bluetooth-low-energy-gatt)
* [Wi-Fi Adapter Linkages](#10-wi-fi-adapter-linkages)
* [Wired Hardware USB Serial](#11-wired-hardware-usb-serial)
* [Native Camera Capture](#12-native-camera-capture)
* [Spatial Geolocation](#13-spatial-geolocation)
* [MQTT Protocol Engine](#14-mqtt-protocol-engine)
* [🤖 AI Developer Prompt Template](#15--ai-developer-prompt-template)

---

### 1. Framework Core Initialization

#### `Clove.ready()`
Blocks downstream JavaScript execution until the Android container environment is fully initialized and securely bound to the web view.

* **Returns:** `Promise<void>`

```javascript
// Always wrap your initialization logic inside an async DOMContentLoaded listener
document.addEventListener("DOMContentLoaded", async () => {
  try {
    console.log("Waiting for Clove runtime...");
    await window.Clove.ready();
    console.log("Sandbox bridge online. Safe to call native APIs.");
    
    // Initialize your UI components here
    initializeDashboard();
  } catch (error) {
    console.error("Failed to initialize Clove OS bridge:", error);
  }
});
```

---

### 2. Unified IoT Gateway

#### `Clove.connectIoT(config, onDataReceived)`
An abstract pipeline gateway that automates connection lifecycles, decodes incoming binary buffers, and streams standard structured data directly to your frontend.

* **Arguments:** * `config` *(Object)*: Connection topology setup.
  * `onDataReceived` *(Function)*: Continuous stream callback `(data) => void`.

##### Example: Continuous Data Streaming (Real-Time Telemetry)
```javascript
async function startContinuousHeartRateStream() {
  await window.Clove.ready();

  const bleConfig = {
    type: "ble",
    target: "AA:BB:CC:11:22:33", // MAC Address
    serviceUuid: "180D",         // Heart Rate Service
    characteristicUuid: "2A37"   // Heart Rate Measurement
  };

  // This callback fires continuously every time the hardware pushes new data
  window.Clove.connectIoT(bleConfig, (incomingTelemetry) => {
    const heartRate = incomingTelemetry.value;
    const timestamp = new Date().toLocaleTimeString();
    
    // Update live dashboard elements
    document.getElementById("live-hr-display").innerText = `${heartRate} BPM`;
    updateChart(timestamp, heartRate);
  });
}
```

##### Example: One-Time Data Polling over HTTP
```javascript
async function fetchServerStatusOnce() {
  await window.Clove.ready();

  const httpConfig = {
    type: "http",
    target: "[https://api.myiotgateway.local/status](https://api.myiotgateway.local/status)",
    pollInterval: 0 // 0 or omitted disables continuous polling for a single fetch
  };

  window.Clove.connectIoT(httpConfig, (response) => {
    console.log("Single snapshot snapshot received:", response);
    document.getElementById("firmware-version").innerText = response.firmware;
  });
}
```

---

### 3. Device & Network Diagnostics

#### `Clove.device.info()` & `Clove.network.status()`
Retrieves hardware specs and inspects active network connectivity before running heavy operations.

```javascript
async function performSystemDiagnostics() {
  await window.Clove.ready();

  // 1. Fetch hardware details (One-time read)
  const deviceInfo = await window.Clove.device.info();
  console.log(`App running on: ${deviceInfo.manufacturer} ${deviceInfo.model} (${deviceInfo.platform})`);

  // 2. Check network readiness before sending telemetry
  const netStatus = await window.Clove.network.status();
  
  if (netStatus.online) {
    console.log(`Connected via ${netStatus.type}. Syncing data...`);
    syncLocalLogsToServer();
  } else {
    console.warn("Device offline. Caching data locally.");
    showOfflineBanner();
  }
}
```

---

### 4. Persistent State Storage

#### `Clove.storage.get(key)` / `.set(key, value)` / `.remove(key)` / `.clear()`
Persists data across app restarts. Automatically handles JSON serialization and deserialization for arrays and objects.

```javascript
async function manageUserPreferences() {
  await window.Clove.ready();

  const defaultSettings = {
    theme: "dark",
    telemetryRate: 1000,
    autoConnect: true
  };

  // Save complex object (One-time write)
  await window.Clove.storage.set("app_settings", defaultSettings);

  // Retrieve data later (One-time read)
  const savedSettings = await window.Clove.storage.get("app_settings");
  
  if (savedSettings && savedSettings.theme === "dark") {
    document.body.classList.add("dark-mode");
  }
}
```

---

### 5. Sandboxed File System

#### `Clove.file.write()` / `.read()` / `.exists()` / `.remove()` / `.open()`
Provides full CRUD access to a private local directory for saving logs, CSV exports, or caching configurations.

```javascript
async function exportTelemetryLog(logArray) {
  await window.Clove.ready();
  const filePath = "exports/session_log.json";

  // Check if file exists
  const exists = await window.Clove.file.exists(filePath);
  if (exists) {
    console.log("Overwriting previous session log...");
  }

  // Write structured data directly to disk
  await window.Clove.file.write(filePath, {
    exportDate: new Date().toISOString(),
    recordCount: logArray.length,
    data: logArray
  });

  // Read it back to verify contents
  const verifiedFile = await window.Clove.file.read(filePath, { mode: "json" });
  console.log(`Successfully verified ${verifiedFile.recordCount} records on disk.`);

  // Prompt Android to open the file using system apps
  await window.Clove.file.open(filePath, "application/json");
}
```

---

### 6. Enterprise HTTP Networking

#### `Clove.http.request(options)`
Routes API calls through the native OS layer, bypassing browser Cross-Origin Resource Sharing (CORS) blocks completely.

```javascript
async function postSensorSnapshot(sensorPayload) {
  await window.Clove.ready();

  // Configure global authentication header first
  await window.Clove.http.setHeader("api.cloud-iot.com", "Authorization", "Bearer token_xyz123");
  await window.Clove.http.setDataSerializer("json");

  try {
    const response = await window.Clove.http.post(
      "[https://api.cloud-iot.com/v1/telemetry](https://api.cloud-iot.com/v1/telemetry)",
      {
        deviceId: "NODE-883",
        batteryLevel: 88,
        readings: sensorPayload
      }
    );

    if (response.ok) {
      console.log("Payload accepted by server:", response.body);
    } else {
      console.error(`Server rejected request: HTTP ${response.status}`);
    }
  } catch (err) {
    console.error("Native HTTP transmission failed:", err);
  }
}
```

---

### 7. User Experience & Feedback

#### `Clove.notification.alert()` / `.confirm()` / `.prompt()` / `.vibrate()`
Triggers native OS modals and haptic vibration motors.

```javascript
async function executeDestructiveAction() {
  await window.Clove.ready();

  // 1. Trigger tactile haptic feedback to get user attention
  await window.Clove.notification.vibrate(200);

  // 2. Show native confirmation dialog
  const userChoice = await window.Clove.notification.confirm(
    "Are you sure you want to format the external sensor flash memory? This cannot be undone.",
    "Hardware Warning",
    ["Format Memory", "Cancel"]
  );

  // Index 1 matches "Format Memory"
  if (userChoice === 1) {
    // 3. Prompt for confirmation security PIN
    const pinDialog = await window.Clove.notification.prompt(
      "Enter Admin PIN to confirm:",
      "Security Auth",
      ["Submit", "Cancel"],
      ""
    );

    if (pinDialog.buttonIndex === 1 && pinDialog.input1 === "1234") {
      await window.Clove.notification.alert("Flash memory formatted successfully.", "Success", "OK");
    }
  }
}
```

---

### 8. Bluetooth Classic Serial (SPP)

#### One-Time Command & Read vs. Continuous Subscription
Bluetooth Classic (RFCOMM) is widely used by Arduino, ESP32, and legacy serial modules. You can query data once or subscribe to a continuous stream.

```javascript
const SPP_MAC = "00:11:22:33:44:55";

// PATTERN A: One-Time Data Fetch (e.g., Querying device battery or config)
async function getFirmwareVersionOnce() {
  await window.Clove.ready();
  
  if (!await window.Clove.bluetooth.isConnected()) {
    await window.Clove.bluetooth.connect(SPP_MAC);
  }

  // Send request command to serial module
  await window.Clove.bluetooth.write("GET_FIRMWARE_VER\n");

  // Wait and read once until new line character arrives
  const versionString = await window.Clove.bluetooth.readUntil("\n");
  console.log("Firmware Version snapshot:", versionString.trim());
}

// PATTERN B: Continuous Reading (e.g., Live sensor stream coming at 10Hz)
async function startSerialLiveStream() {
  await window.Clove.ready();
  
  if (!await window.Clove.bluetooth.isConnected()) {
    await window.Clove.bluetooth.connect(SPP_MAC);
  }

  console.log("Subscribing to serial stream...");
  
  // Attach a persistent listener that fires every time a newline '\n' is received
  await window.Clove.bluetooth.subscribe("\n", (rawLine) => {
    const cleanData = rawLine.trim();
    console.log("Live stream packet:", cleanData);
    
    // Parse incoming CSV: e.g., "TEMP:24.5,HUM:55"
    const parts = cleanData.split(",");
    document.getElementById("temp-readout").innerText = parts[0];
  });
}
```

---

### 9. Bluetooth Low Energy (GATT)

#### One-Time Characteristic Read vs. Continuous Notifications
BLE communicates via Services and Characteristics. Use `.read()` for snapshots and `.startNotification()` for real-time sensor updates.

```javascript
const BLE_MAC = "F3:D2:C1:00:AA:BB";
const ENV_SERVICE = "181A";
const TEMP_CHAR = "2A6E";

// PATTERN A: One-Time Read Snapshot
async function readTemperatureOnce() {
  await window.Clove.ready();
  await window.Clove.ble.connect(BLE_MAC);

  // Read binary ArrayBuffer once from GATT server
  const rawBuffer = await window.Clove.ble.read(BLE_MAC, ENV_SERVICE, TEMP_CHAR);
  
  // Decode raw byte buffer (e.g., 16-bit integer divided by 100)
  const dataView = new DataView(rawBuffer);
  const tempCelsius = dataView.getInt16(0, true) / 100;
  
  console.log("Snapshot Temperature Read:", tempCelsius, "°C");
}

// PATTERN B: Continuous Live Notifications
async function subscribeToLiveTemperature() {
  await window.Clove.ready();
  await window.Clove.ble.connect(BLE_MAC);

  console.log("Enabling GATT Notifications...");

  // Instruct native BLE radio to stream updates to callback function
  await window.Clove.ble.startNotification(BLE_MAC, ENV_SERVICE, TEMP_CHAR, (rawBuffer) => {
    const dataView = new DataView(rawBuffer);
    const liveTemp = dataView.getInt16(0, true) / 100;
    
    // Update dashboard gauge in real time
    document.getElementById("temp-gauge").setAttribute("data-value", liveTemp);
  });
}
```

---

### 10. Wi-Fi Adapter Linkages

#### `Clove.wifi.list()` & `.connect()`
Scans local airspace and connects the Android hardware to an IoT Access Point (AP).

```javascript
async function connectToDeviceHotspot() {
  await window.Clove.ready();

  if (!await window.Clove.wifi.isEnabled()) {
    await window.Clove.notification.alert("Please turn on Wi-Fi first.", "Notice", "OK");
    return;
  }

  // Scan surrounding APs (One-time fetch)
  const networks = await window.Clove.wifi.list();
  const targetNet = networks.find(n => n.SSID.startsWith("ESP32_Setup_"));

  if (targetNet) {
    console.log(`Found device hotspot: ${targetNet.SSID}. Connecting...`);
    await window.Clove.wifi.connect(targetNet.SSID, "secretpass123", "WPA", false);
    console.log("Successfully bound to device local subnet.");
  } else {
    console.error("Target hardware AP not in range.");
  }
}
```

---

### 11. Wired Hardware USB Serial

#### `Clove.usb.requestPermission()` / `.open()` / `.write()` / `.read()`
Enables direct wired communication with FTDI, CP210X, or Arduino chips plugged via USB OTG.

```javascript
async function startUsbSerialLoop() {
  await window.Clove.ready();

  const usbConfig = {
    baudRate: 115200,
    dataBits: 8,
    stopBits: 1,
    parity: 0
  };

  // Request Android OTG hardware permission
  await window.Clove.usb.requestPermission(usbConfig);
  await window.Clove.usb.open(usbConfig);

  // Setup Continuous Reader Loop
  await window.Clove.usb.read((incomingBuffer) => {
    const textDecoder = new TextDecoder("utf-8");
    const incomingString = textDecoder.decode(incomingBuffer);
    
    // Append terminal logs
    const terminal = document.getElementById("usb-terminal");
    terminal.value += incomingString;
    terminal.scrollTop = terminal.scrollHeight;
  });

  // Send startup command
  await window.Clove.usb.write("START_DEBUG_OUTPUT\n");
}
```

---

### 12. Native Camera Capture

#### `Clove.camera.getPicture(options)`
Launches the device's native camera viewfinder to capture inspection images.

```javascript
async function captureInspectionPhoto() {
  await window.Clove.ready();

  const camOptions = {
    quality: 85,
    destinationType: 0, // 0 = Base64 String, 1 = File Path
    sourceType: 1       // 1 = Camera Viewfinder
  };

  try {
    const base64Image = await window.Clove.camera.getPicture(camOptions);
    
    // Render directly into the DOM
    const imgElement = document.getElementById("inspection-preview");
    imgElement.src = `data:image/jpeg;base64,${base64Image}`;
    imgElement.style.display = "block";
  } catch (err) {
    console.log("User canceled camera viewfinder.", err);
  }
}
```

---

### 13. Spatial Geolocation

#### One-Time GPS Fix vs. Continuous Asset Tracking
Fetch precise satellite positioning coordinates for spatial mapping or telemetry geotagging.

```javascript
// PATTERN A: One-Time Position Snapshot
async function tagEventLocationOnce() {
  await window.Clove.ready();

  const pos = await window.Clove.geolocation.getCurrentPosition({
    enableHighAccuracy: true,
    timeout: 5000
  });

  console.log(`Single GPS Snapshot: ${pos.coords.latitude}, ${pos.coords.longitude}`);
  return pos.coords;
}

// PATTERN B: Continuous Asset Tracking (Live GPS Stream)
let gpsWatchId = null;

async function startLiveGpsTracking() {
  await window.Clove.ready();

  // Streams updated location continuously as the physical device moves
  gpsWatchId = await window.Clove.geolocation.watchPosition((livePos) => {
    const { latitude, longitude, speed } = livePos.coords;
    
    // Update live dashboard map marker
    updateMapMarker(latitude, longitude);
    document.getElementById("speedometer").innerText = `${(speed || 0).toFixed(1)} m/s`;
  }, {
    enableHighAccuracy: true
  });
}

async function stopLiveGpsTracking() {
  if (gpsWatchId !== null) {
    await window.Clove.geolocation.clearWatch(gpsWatchId);
    gpsWatchId = null;
    console.log("GPS tracking loop stopped.");
  }
}
```

---

### 14. MQTT Protocol Engine

#### `Clove.mqtt.connect()` / `.publish()` / `.subscribe()`
Connects directly to remote IoT message brokers (HiveMQ, AWS IoT, Mosquitto) natively over TCP/WebSockets.

```javascript
async function startMqttPipeline() {
  await window.Clove.ready();

  // 1. Establish persistent broker connection
  await window.Clove.mqtt.connect({
    host: "broker.hivemq.com",
    port: 1883,
    clientId: "clove_client_" + Math.random().toString(16).substr(2, 8)
  });

  // 2. Subscribe to Continuous Incoming Message Stream
  await window.Clove.mqtt.subscribe("factory/line1/alerts", (topic, payload) => {
    console.log(`Continuous stream alert on [${topic}]:`, payload);
    showRedAlertBanner(payload);
  });

  // 3. Publish a One-Time Command Message
  const commandPayload = JSON.stringify({ action: "RESET_COUNTERS", operatorId: "OP-44" });
  await window.Clove.mqtt.publish("factory/line1/control", commandPayload);
  console.log("Control command dispatched.");
}
```

---

### 15. 🤖 AI Developer Prompt Template

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

### COMPLETE GLOBAL API REFERENCE:
* Core: `Clove.ready()`, `Clove.connectIoT({type, target, serviceUuid, characteristicUuid, delimiter, pollInterval}, callback)`
* Device Info & Network: `Clove.device.info()`, `Clove.network.status()`
* Persistent Storage: `Clove.storage.get(k)`, `Clove.storage.set(k, v)`, `Clove.storage.remove(k)`, `Clove.storage.clear()`
* Local Filesystem: `Clove.file.write(path, data)`, `Clove.file.read(path, {mode})`, `Clove.file.exists(path)`, `Clove.file.remove(path)`, `Clove.file.open(path, mime)`
* Proxy HTTP Networking: `Clove.http.get(url, opts)`, `Clove.http.post(url, data, opts)`, `Clove.http.setHeader(host, header, val)`, `Clove.http.setDataSerializer(format)`
* UI Feedback: `Clove.notification.alert(m, t, b)`, `Clove.notification.confirm(m, t, [b])`, `Clove.notification.prompt()`, `Clove.notification.vibrate(ms)`
* Classic Serial SPP: `Clove.bluetooth.list()`, `Clove.bluetooth.connect(addr)`, `Clove.bluetooth.write(str)`, `Clove.bluetooth.readUntil(delim)`, `Clove.bluetooth.subscribe(delim, cb)`, `Clove.bluetooth.disconnect()`
* Low-Energy GATT BLE: `Clove.ble.scan(services, secs)`, `Clove.ble.connect(id)`, `Clove.ble.read(id, s, c)`, `Clove.ble.write(id, s, c, buf)`, `Clove.ble.startNotification(id, s, c, cb)`
* Wi-Fi Management: `Clove.wifi.list()`, `Clove.wifi.connect(ssid, pass, algo)`, `Clove.wifi.isEnabled()`
* Wired OTG USB: `Clove.usb.requestPermission(opts)`, `Clove.usb.open(opts)`, `Clove.usb.write(str)`, `Clove.usb.read(cb)`, `Clove.usb.close()`
* Camera: `Clove.camera.getPicture(opts)`
* Geolocation: `Clove.geolocation.getCurrentPosition(opts)`, `Clove.geolocation.watchPosition(cb, opts)`, `Clove.geolocation.clearWatch(id)`
* MQTT Messaging: `Clove.mqtt.connect(opts)`, `Clove.mqtt.publish(topic, msg)`, `Clove.mqtt.subscribe(topic, cb)`

Acknowledge these API parameters and constraints, and generate the complete code suite (HTML/CSS/JS) for my specific dashboard request described below.
```
