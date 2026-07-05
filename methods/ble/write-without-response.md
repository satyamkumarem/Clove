# Clove.ble.writeWithoutResponse(deviceId, serviceUUID, characteristicUUID, value)

Pushes a binary value to a specific GATT characteristic using unacknowledged transfer modes. This optimizes transfer speeds for high-throughput streaming by omitting acknowledgment handshakes.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `deviceId` | `string` | Tracking address or unique destination target UUID assignment mapping. | `"AA:BB:CC:DD:EE:FF"` |
| `serviceUUID` | `string` | Target GATT Service UUID tracking structural layout patterns. | `"FFE0"` |
| `characteristicUUID` | `string` | Target GATT Characteristic UUID optimized for unacknowledged streaming lines. | `"FFE2"` |
| `value` | `ArrayBuffer` | Raw binary container block holding the byte sequence to blast downstream. | `new Uint8Array([0xAA, 0xBB]).buffer` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value immediately when the binary chunk leaves the native outbound adapter buffers. It does not verify receipt.

## Code Example

```javascript
async function streamRealTimeTelemetryPackets() {
  const deviceId = "AA:BB:CC:DD:EE:FF";
  const streamServiceUuid = "FFE0";
  const fastWriteCharacteristicUuid = "FFE2";

  const telemetryDataChunk = new Uint8Array([0x0A, 0x14, 0x28, 0x32]);

  try {
    await Clove.ready();
    
    // Blast data downstream quickly without stalling for handshakes
    await Clove.ble.writeWithoutResponse(deviceId, streamServiceUuid, fastWriteCharacteristicUuid, telemetryDataChunk.buffer);
    
  } catch (error) {
    console.error("Fast-write streaming pipeline failed to drop buffer payload onto adapter lanes:", error);
  }
}

// Push fast metrics every 100 milliseconds
setInterval(streamRealTimeTelemetryPackets, 100);
```