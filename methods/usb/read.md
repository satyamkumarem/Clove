# Clove.usb.read(cb)

Registers a persistent background event callback listener that executes automatically whenever incoming data packages are intercepted on the physical Rx serial line.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `cb` | `Function` | The receiver event listener target function triggered automatically whenever bytes appear on the serial interface. | `(rawData) => {}` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the native driver-level callback proxy routing is successfully established.

## Code Example

```javascript
async function mountUsbDataStreamIngress() {
  // Callback tracking handler logic
  const processIncomingSerialBytes = (rawIncomingPayload) => {
    // Note: Raw binary byte data streams are automatically routed 
    // through internal TextDecoder wrappers before reaching this point.
    console.log(`Incoming Serial Event String Data: [${rawIncomingPayload}]`);
  };

  try {
    await Clove.ready();
    console.log("Binding continuous asynchronous Rx monitoring loops over target USB serial port...");
    
    await Clove.usb.read(processIncomingSerialBytes);
    console.log("Wired data streaming listener attached. Monitoring input buffers...");
    
  } catch (error) {
    console.error("Platform driver rejected data stream callback connection mappings:", error);
  }
}

mountUsbDataStreamIngress();
```