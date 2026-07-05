# Clove.ble.startNotification(deviceId, serviceUUID, characteristicUUID, callback)

Subscribes to real-time value change notification updates from a specified GATT characteristic.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `deviceId` | `string` | Unique tracking address identification signature string of the target peripheral. | `"AA:BB:CC:DD:EE:FF"` |
| `serviceUUID` | `string` | The specific GATT Service UUID indicating the active category space. | `"180D"` |
| `characteristicUUID` | `string` | The specific GATT Characteristic UUID supporting asynchronous push notification frames. | `"2A37"` |
| `callback` | `Function` | Listener method triggered automatically whenever the remote peripheral pushes a data change packet. | `(buffer) => {}` |

### Parameter Details
* **`callback` Payload Format:** The listener function intercepts a single raw argument consisting of an `ArrayBuffer` containing the peripheral's mutated attribute states.

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves when the Client Characteristic Configuration Descriptor (CCCD) is modified successfully to enable notification streams.

## Code Example

```javascript
async function monitorHeartRateSensorUpdates() {
  const deviceId = "AA:BB:CC:DD:EE:FF";
  const heartRateServiceUuid = "180D";
  const measurementCharacteristicUuid = "2A37";

  const onHeartRateMeasurementArrived = (rawBuffer) => {
    const dataView = new DataView(rawBuffer);
    const flags = dataView.getUint8(0);
    const heartRateBpm = dataView.getUint8(1);
    
    console.log(`Asynchronous Telemetry Push -> Heart Rate Resolved: ${heartRateBpm} BPM`);
  };

  try {
    await Clove.ready();
    console.log("Registering real-time subscription monitors over target GATT characteristic...");
    
    await Clove.ble.startNotification(deviceId, heartRateServiceUuid, measurementCharacteristicUuid, onHeartRateMeasurementArrived);
    console.log("Notification subscription active. Listening for remote hardware telemetry alerts.");
    
  } catch (error) {
    console.error("Failed to map push notification listeners over targeted descriptor paths:", error);
  }
}

monitorHeartRateSensorUpdates();
```