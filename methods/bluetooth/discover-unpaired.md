# Clove.bluetooth.discoverUnpaired()

Initiates a live, low-level RF air scan to discover nearby unpaired Bluetooth Classic peripherals.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<Array<Object>>`
* **Description:** Resolves with an array of newly discovered unpaired peripheral objects detected during the discovery window cycle.

### Array Element Properties:
| Property | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `name` | `string` | The human-readable broadcast identifier name of the device. | `"Thermal-Printer-X"` |
| `address` | `string` | The unique physical hardware MAC address sequence of the module. | `"20:22:04:11:AB:CD"` |
| `id` | `string` | System tracking reference tracking identity matching the hardware node. | `"20:22:04:11:AB:CD"` |

## Code Example

```javascript
async function scanForNewDevices() {
  try {
    await Clove.ready();
    
    console.log("Scanning airwaves for unpaired Bluetooth Classic modules (this may take a few seconds)...");
    const discoveredDevices = await Clove.bluetooth.discoverUnpaired();
    
    console.log(`Scan completed. Found ${discoveredDevices.length} unpaired devices.`);
    discoveredDevices.forEach(device => {
      console.log(`-> Target: ${device.name || "Unknown Device"} [${device.address}]`);
    });
    
  } catch (error) {
    console.error("Failed executing hardware discovery sequences:", error);
  }
}

scanForNewDevices();
```