# Clove.ble.write(deviceId, serviceUUID, characteristicUUID, value)

Writes a value to a specific GATT characteristic, blocking execution until the remote BLE peripheral sends back a confirmation response acknowledgement.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `deviceId` | `string` | Destination address or tracking UUID string assignment for the target peripheral. | `"AA:BB:CC:DD:EE:FF"` |
| `serviceUUID` | `string` | Target GATT Service UUID string defining the operational cluster profile. | `"FFE0"` |
| `characteristicUUID` | `string` | Targeted GATT Characteristic UUID where the value payload should overwrite configuration. | `"FFE1"` |
| `value` | `ArrayBuffer` | Raw binary container block holding the byte sequences meant for output transmission. | `new Uint8Array([0x01]).buffer` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value once the target peripheral writes the bytes into memory and successfully transmits a verification handshake receipt back to the host.

## Code Example

```javascript
async function writeConfigurationToPeripheral() {
  const deviceId = "AA:BB:CC:DD:EE:FF";
  const customServiceUuid = "FFE0";
  const controlCharacteristicUuid = "FFE1";

  // Build binary array stream: [0x41, 0x42] -> "AB"
  const payloadBytes = new Uint8Array([0x41, 0x42]);

  try {
    await Clove.ready();
    console.log("Dispatching written payload metrics across secure GATT characteristic lanes...");
    
    await Clove.ble.write(deviceId, customServiceUuid, controlCharacteristicUuid, payloadBytes.buffer);
    console.log("Write transaction completed and acknowledged by remote BLE hardware.");
    
  } catch (error) {
    console.error("GATT write block pipeline returned critical error sequence:", error);
  }
}

writeConfigurationToPeripheral();
```