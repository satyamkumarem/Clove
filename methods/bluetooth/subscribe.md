# Clove.bluetooth.subscribe(delimiter, callback)

Attaches a continuous real-time background listener line targeting the serial input connection pipeline.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `delimiter` | `string` | Character boundary condition indicating a complete structural frame has been parsed. | `"\r\n"` |
| `callback` | `Function` | Executable routine triggered automatically whenever a complete frame matching delimiter boundaries arrives. | `(frame) => {}` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves when the persistent background listener interface loop is registered and active.

## Code Example

```javascript
async function startRealTimeDataSubscription() {
  const frameBreakDelimiter = "\n";
  
  const processIncomingFrame = (rawPacketStr) => {
    console.log(`Stream Subscription Intercept: ${rawPacketStr.trim()}`);
  };

  try {
    await Clove.ready();
    
    // Subscribe to continuous incoming frames
    await Clove.bluetooth.subscribe(frameBreakDelimiter, processIncomingFrame);
    console.log("Continuous background streaming pipeline subscription is active.");
    
  } catch (error) {
    console.error("Failed to assert streaming background subscription connections:", error);
  }
}

startRealTimeDataSubscription();
```