# Clove.ble.stopNotification(deviceId, serviceUUID, characteristicUUID)

Unsubscribes from GATT characteristic value notifications, stopping asynchronous push events from updating background listeners.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `deviceId` | `string` | Unique tracking address layout signature mapping string matching the peripheral. | `"AA:BB:CC:DD:EE:FF"` |
| `serviceUUID` | `string` | Target GATT Service UUID location properties context. | `"180D"` |
| `characteristicUUID` | `string` | Targeted GATT Characteristic UUID tracking metrics. | `"2A37"` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves when the Client Characteristic Configuration Descriptor (CCCD) is modified successfully to disable notification streams natively.

## Code Example

```javascript
async function cancelHeartRateMonitoring() {
  const deviceId = "AA:BB:CC:DD:EE:FF";
  const heartRateServiceUuid = "180D";
  const measurementCharacteristicUuid = "2A37";

  try {
    await Clove.ready();
    console.log("Dismantling notification descriptors over remote peripheral attributes...");
    
    await Clove.ble.stopNotification(deviceId, heartRateServiceUuid, measurementCharacteristicUuid);
    console.log("Asynchronous push notifications deactivated cleanly.");
    
  } catch (error) {
    console.error("Failed to unbind notification bindings on target characteristic descriptor pathways:", error);
  }
}

cancelHeartRateMonitoring();
```