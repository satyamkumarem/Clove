# Clove.usb.write(data)

Transmits raw string text data or hex instructions downstream through the active physical USB serial connection channel.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `data` | `string` | The text context characters, message payload string, or command string instructions to send. | `"INIT_NODE_CMD\n"` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value once the byte payload passes cleanly into native lower-level serial buffer rings.

## Code Example

```javascript
async function dispatchHardwareCommand() {
  const rawCommandText = "TRIGGER_SAMPLING_STREAM\r\n";

  try {
    await Clove.ready();
    console.log("Writing raw instruction sequence blocks to USB interface...");
    
    await Clove.usb.write(rawCommandText);
    console.log("Bytes written to serial Tx pipeline buffers successfully.");
    
  } catch (error) {
    console.error("Hardware Tx pipe blocked. Failed to pass string data natively:", error);
  }
}
```