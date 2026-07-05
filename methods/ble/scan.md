# Clove.ble.scan(services, seconds, callback)

Scans for Bluetooth Low Energy (BLE) peripherals in the vicinity. Results are passed continuously to the provided callback function as they are discovered.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `services` | `Array<string>` | An array of service UUID strings to filter the scan. Pass an empty array `[]` to scan for all available BLE devices. | `["180D", "180F"]` |
| `seconds` | `number` | The duration window in seconds for how long the native BLE hardware scanner should actively run. | `5` |
| `callback` | `Function` | A callback function executed every time a matching BLE device is discovered during the scan window. | `(device) => {}` |

### Parameter Details

#### `callback` Parameter Device Object Structure:
| Property | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `name` | `string` | Human-readable broadcast name of the BLE device. | `"Smart-Heart-Rate"` |
| `id` | `string` | The unique MAC address (Android) or system UUID assigned to the device. | `"AA:BB:CC:DD:EE:FF"` |
| `rssi` | `number` | Received Signal Strength Indicator demonstrating signal quality metrics. | `-65` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves when the native background scanning routine is successfully launched. It does not wait for the scan duration to finish.

## Code Example

```javascript
async function startBleDeviceScan() {
  const targetServices = []; // Scan for all available BLE peripherals
  const scanDurationSeconds = 10;

  const onDeviceDiscovered = (device) => {
    console.log(`Discovered BLE Periphery -> Name: ${device.name || "Unknown"} | ID: ${device.id} | RSSI: ${device.rssi}`);
  };

  try {
    await Clove.ready();
    console.log("Starting BLE peripheral discovery loops...");
    
    await Clove.ble.scan(targetServices, scanDurationSeconds, onDeviceDiscovered);
    console.log(`BLE scanning initialized for ${scanDurationSeconds} seconds.`);
    
  } catch (error) {
    console.error("Failed to launch BLE hardware scanner instance:", error);
  }
}

startBleDeviceScan();
```