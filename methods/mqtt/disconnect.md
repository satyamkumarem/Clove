# Clove.mqtt.disconnect()

Gracefully severs the active TCP link socket association with the connected MQTT broker, clean closing any pending tracking handles.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the interface connection handles tear down natively and release resources.

## Code Example

```javascript
async function closeBrokerSession() {
  try {
    await Clove.ready();
    console.log("Severing active MQTT pipeline connection bindings...");
    
    await Clove.mqtt.disconnect();
    console.log("MQTT client detached gracefully from broker cluster.");
    
  } catch (error) {
    console.error("Failed to execute clean disconnect handlers over active MQTT pipeline:", error);
  }
}
```