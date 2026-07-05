# Clove.bluetooth.unsubscribe()

Removes any active continuous real-time stream subscription listener attached to the incoming connection pipelines.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when background polling or interrupt routines are disconnected safely.

## Code Example

```javascript
async function stopStreamingSubscription() {
  try {
    await Clove.ready();
    
    // Cancel the continuous stream subscription
    await Clove.bluetooth.unsubscribe();
    console.log("Background streaming subscription decoupled safely.");
    
  } catch (error) {
    console.error("Failed to disconnect active listener subscriptions profiles cleanly:", error);
  }
}

stopStreamingSubscription();
```