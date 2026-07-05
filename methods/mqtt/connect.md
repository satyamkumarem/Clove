# Clove.mqtt.connect(opts)

Initializes a persistent background socket connection to a target MQTT broker to allow asynchronous message publishing and subscription streaming.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `opts` | `Object` | Connection configuration options required to locate, authorize, and bind to the MQTT broker. | `{ host: "tcp://broker.hivemq.com", port: 1883 }` |

### Common `opts` Configuration Matrix
| Property | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `host` | `string` | The network URL coordinate protocol address of the target MQTT broker. | `"tcp://broker.emqx.io"` or `"ssl://localhost"` |
| `port` | `number` | The hardware socket connection port utilized by the destination broker. | `1883` (Non-secure) or `8883` (SSL/TLS) |
| `clientId` | `string` | Unique client tracking identity string token passed to the broker during handshakes. | `"LPU_Device_Node_99"` |
| `username` | `string` | Optional access identity authorization profile tracking string identifier. | `"admin_developer"` |
| `password` | `string` | Optional security credential string asset utilized alongside the username profile. | `"SecretMqttToken"` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value once the broker completes TCP session handshakes and registers the client connection session successfully.

## Code Example

```javascript
async function establishBrokerSession() {
  const connectionConfiguration = {
    host: "tcp://broker.hivemq.com",
    port: 1883,
    clientId: "Clove_Client_Node_Alpha",
    timeout: 30
  };

  try {
    await Clove.ready();
    console.log(`Connecting to remote MQTT broker network at: ${connectionConfiguration.host}`);
    
    await Clove.mqtt.connect(connectionConfiguration);
    console.log("MQTT tracking connection established safely. Pub/Sub engine listening.");
    
  } catch (error) {
    console.error("MQTT connection pipeline halted. Check address string or network health:", error);
  }
}

establishBrokerSession();
```