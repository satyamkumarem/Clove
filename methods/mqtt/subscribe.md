# Clove.mqtt.subscribe(t, c, o)

Registers a persistent interest in a designated topic routing branch, linking an asynchronous handler callback to process messages that match the string format criteria.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `t` | `string` | The topic string tracking route filter pattern to look up. Supports single-level (`+`) and multi-level (`#`) pattern wildcards. | `"telemetry/ewaste/+"` |
| `c` | `Function` | The event listener tracking callback function invoked automatically every time a matching message payload arrives. | `(topic, message) => {}` |
| `o` | `Object` | Optional transaction properties passed down to the client layout matrix interface layer. | `{ qos: 1 }` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the subscription registry criteria verification is successfully saved inside broker tables.

## Code Example

```javascript
async function attachTelemetryStreamMonitor() {
  const trackingTopicPattern = "telemetry/ewaste/#";
  const deliveryOptions = { qos: 1 };

  // Message interception tracking handler routine
  const handleIncomingBrokerPayload = (topic, messageString) => {
    console.log(`-> Incoming Message [Topic: ${topic}]`);
    try {
      const complexDataObj = JSON.parse(messageString);
      console.log("Decoded Stream Object Context:", complexDataObj);
    } catch {
      console.log(`Raw text package contents parsed: ${messageString}`);
    }
  };

  try {
    await Clove.ready();
    console.log(`Binding active structural subscription pattern matrix: [${trackingTopicPattern}]`);
    
    await Clove.mqtt.subscribe(trackingTopicPattern, handleIncomingBrokerPayload, deliveryOptions);
    console.log("Subscription registration synchronized. Stream listening active.");
    
  } catch (error) {
    console.error("Broker rejected structural subscription configuration layout parameters:", error);
  }
}
```