# Clove.ble.disconnect(deviceId)

Tears down an active Generic Attribute Profile (GATT) connection link pointing to a specific BLE device.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `deviceId` | `string` | The system tracking address identifier or MAC string matching the target BLE device. | `"AA:BB:CC:DD:EE:FF"` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the internal GATT channel session has been cleanly unlinked.

## Code Example

```javascript
async function disconnectBleDevice() {
  const targetedActiveNodeId = "AA:BB:CC:DD:EE:FF";

  try {
    await Clove.ready();
    console.log(`Severing active GATT connection link context to: ${targetedActiveNodeId}`);
    
    await Clove.ble.disconnect(targetedActiveNodeId);
    console.log("BLE peripheral connection dismantled securely.");
    
  } catch (error) {
    console.error("Failed to execute BLE disconnection sequences cleanly:", error);
  }
}

disconnectBleDevice();
```