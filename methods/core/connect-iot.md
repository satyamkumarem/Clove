# Clove.connectIoT(config, callback)

A universal master orchestrator designed to route continuous hardware communication lines through a single method interface. It establishes a connection to a target peripheral stream and handles continuous data incoming events.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `config` | `Object` | Configuration criteria defining the connection type, target physical address, and data frame delimiter. | `{ type: "bluetooth", target: "00:11:22:33:44:55", delimiter: "\\n" }` |
| `callback` | `Function` | A callback function fired continuously whenever complete data frames pass through the connection pipeline. | `(data) => { console.log(data); }` |

### Parameter Details

#### 1. `config` Object Properties:
* **`type`** (`string`): The connection protocol. Supported options: `"bluetooth"`, `"ble"`, `"usb"`.
* **`target`** (`string`): The hardware identifier (MAC address, UUID, or hardware ID).
* **`delimiter`** (`string`): The character sequence used to split incoming data into complete frames.

#### 2. `callback` Function Signature:
* Receives a single argument containing the raw string or data packet frame processed by the native driver layer.

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves successfully when the pipeline listener loop is successfully instantiated.

## Code Example

```javascript
async function startIoTStream() {
  const connectionConfig = {
    type: "bluetooth",
    target: "00:11:22:33:44:55",
    delimiter: "\n"
  };

  const handleIncomingData = (dataFrame) => {
    console.log("New telemetry frame arrived:", dataFrame);
  };

  try {
    await Clove.ready();
    
    // Establish the continuous stream pipeline
    await Clove.connectIoT(connectionConfig, handleIncomingData);
    console.log("IoT connection channel opened successfully.");
    
  } catch (error) {
    console.error("Failed to establish IoT communication channel:", error);
  }
}

startIoTStream();
```