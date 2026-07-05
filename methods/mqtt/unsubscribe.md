# Clove.mqtt.unsubscribe(t)

Removes an active topic registration matching pattern from the broker client context matching tables, tearing down associated message stream events.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `t` | `string` | The exact string pattern matching filter path configuration string to clear from background loops. | `"telemetry/ewaste/#"` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the subscription profile is removed from the network interface state layout cleanly.

## Code Example

```javascript
async function detachTelemetryStreamMonitor() {
  const targetPatternToClear = "telemetry/ewaste/#";

  try {
    await Clove.ready();
    console.log(`Dismantling active subscription tracking filters for path: ${targetPatternToClear}`);
    
    await Clove.mqtt.unsubscribe(targetPatternToClear);
    console.log("Subscription hook detached securely from engine tracking filters.");
    
  } catch (error) {
    console.error("Failed to unbind destination tracking arrays from broker registry blocks:", error);
  }
}
```