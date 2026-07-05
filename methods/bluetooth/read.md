# Clove.bluetooth.read()

Performs a raw pull execution block targeting the internal incoming native socket receive memory buffers.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<string>`
* **Description:** Resolves with a raw string capture grouping containing whatever bytes are currently waiting unprocessed in the native input queue stream. Returns an empty string if the queue is empty.

## Code Example

```javascript
async function flushIncomingBufferBytes() {
  try {
    await Clove.ready();
    
    // Execute a read action targeting incoming socket queues
    const waitingBufferString = await Clove.bluetooth.read();
    
    if (waitingBufferString.length > 0) {
      console.log(`Intercepted data fragments straight out from buffer: ${waitingBufferString}`);
    } else {
      console.log("No characters are waiting inside the stream lines currently.");
    }
    
  } catch (error) {
    console.error("Failed to empty incoming native stream memory blocks:", error);
  }
}

// Check buffer every second manually
setInterval(flushIncomingBufferBytes, 1000);
```