# Clove.ble.read(deviceId, serviceUUID, characteristicUUID)

Reads the binary value of a specified GATT characteristic from a connected BLE peripheral.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `deviceId` | `string` | Address or unique hardware identifier sequence matching the target device. | `"AA:BB:CC:DD:EE:FF"` |
| `serviceUUID` | `string` | The specific GATT Service UUID identifying the functional category block. | `"180F"` |
| `characteristicUUID` | `string` | The targeting GATT Characteristic UUID string mapping the precise value field. | `"2A19"` |

## Return Type

* **Type:** `Promise<ArrayBuffer>`
* **Description:** Resolves with a raw JavaScript binary `ArrayBuffer` containing the data payload bytes extracted directly from the peripheral's memory registry.

## Code Example

```javascript
async function readBatteryLevelCharacteristic() {
  const deviceId = "AA:BB:CC:DD:EE:FF";
  const batteryServiceUuid = "180F";
  const batteryLevelCharacteristicUuid = "2A19";

  try {
    await Clove.ready();
    
    // Fetch raw binary buffer from remote GATT layer
    const rawBuffer = await Clove.ble.read(deviceId, batteryServiceUuid, batteryLevelCharacteristicUuid);
    
    // Decode the binary array chunk mapping values (Battery Level is normally 1 byte integer)
    const dataView = new DataView(rawBuffer);
    const percentageValue = dataView.getUint8(0);
    
    console.log(`Peripheral Battery Diagnostics: ${percentageValue}%`);
    
  } catch (error) {
    console.error("Failed to execute characteristic read operations over current GATT bridge:", error);
  }
}

readBatteryLevelCharacteristic();
```