# Clove.ble.connect(deviceId, disconnectCallback)

Establishes a persistent Generic Attribute Profile (GATT) connection to a specific target BLE peripheral.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `deviceId` | `string` | The system identifier address or MAC string matching the target BLE hardware module. | `"AA:BB:CC:DD:EE:FF"` |
| `disconnectCallback` | `Function` | An optional background callback triggered automatically if the device unexpectedly drops connection. | `(event) => {}` |

## Return Type

* **Type:** `Promise<Object>`
* **Description:** Resolves with a structured device metadata schema reporting successful GATT service discovery and peripheral handshakes.

## Code Example

```javascript
async function connectToBlePeripheral() {
  const targetId = "AA:BB:CC:DD:EE:FF";

  const handleUnexpectedDisconnect = (event) => {
    console.warn(`Critical alert: BLE connection dropped unexpectedly for peripheral ${event.id}`);
  };

  try {
    await Clove.ready();
    console.log(`Initializing GATT connection sequence targeting node: ${targetId}`);
    
    const peripheralDetails = await Clove.ble.connect(targetId, handleUnexpectedDisconnect);
    console.log("GATT handshake completed successfully. Discovered services:", peripheralDetails.services);
    
  } catch (error) {
    console.error(`Failed to assert functional connection to BLE peripheral [${targetId}]:`, error);
  }
}

connectToBlePeripheral();
```