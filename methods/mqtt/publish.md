# Clove.mqtt.publish(t, p, o)

Dispatches a data payload message package targeting a specific destination topic routing coordinate on the MQTT broker.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `t` | `string` | The destination topic path hierarchy coordinate route identifying where to publish. | `"telemetry/ewaste/bihar"` |
| `p` | `string` | The text message contents or stringified payload dataset package bytes to transmit. | `"{\"status\": \"active\", \"load\": 45}"` |
| `o` | `Object` | Optional payload parameter criteria properties passed down to the underlying client driver. | `{ qos: 1, retain: false }` |

### Optional `o` Configuration Parameters
| Property | Type | Description | Default / Settings |
| :--- | :--- | :--- | :--- |
| `qos` | `number` | Quality of Service routing delivery tracking metrics scale. | `0` (At most once), `1` (At least once), `2` (Exactly once) |
| `retain` | `boolean` | Instructs the broker to save this message payload as the definitive current snapshot tracking value. | `true` or `false` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value once the message transmission has successfully passed down into local socket buffers.

## Code Example

```javascript
async function emitTelemetryData() {
  const targetTopicRoute = "telemetry/ewaste/bihar";
  const structuralPayload = JSON.stringify({
    timestamp: Date.now(),
    nodeStatus: "Operational",
    batteryLevel: 92
  });
  const publishingOptions = { qos: 1, retain: true };

  try {
    await Clove.ready();
    console.log(`Publishing tracking updates under topic branch: [${targetTopicRoute}]`);
    
    await Clove.mqtt.publish(targetTopicRoute, structuralPayload, publishingOptions);
    console.log("MQTT broker acknowledges transmission payload queue commit.");
    
  } catch (error) {
    console.error("Message delivery failed to pass down to target routing branches:", error);
  }
}
```