# Clove.bluetooth.write(data)

Transmits raw data packages down across the open active RFCOMM serial pipe channel.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `data` | `string \| Uint8Array` | The string sequence command or raw byte data payload to push to the serial pipeline. | `"GET_TELEMETRY\n"` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value immediately when the complete array of byte streams flushes into the native transmit hardware queue.

## Code Example

```javascript
async function sendCommandToHardware() {
  const commandString = "LED_ON\n";

  try {
    await Clove.ready();
    
    // Write data out across the open stream link 
    await Clove.bluetooth.write(commandString);
    console.log(`Command stream written successfully: ${commandString.trim()}`);
    
  } catch (error) {
    console.error("Failed to push data packets across active Bluetooth serial interface:", error);
  }
}

sendCommandToHardware();
```