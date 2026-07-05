# Clove.network.status()

Inspects the system's real-time network connectivity status to verify internet access availability and active adapter routing paths.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<Object>`
* **Description:** Resolves with an object highlighting internet presence availability matrices.

### Return Object Properties:
| Property | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `online` | `boolean` | Flag indicating whether the system currently has active internet connectivity. | `true` |
| `type` | `string` | The direct network transport pipeline adapter protocol signature. | `"wifi"` |

> 💡 **Supported values for `type`:** `"wifi"`, `"cellular"`, or `"none"`.

## Code Example

```javascript
async function verifyNetworkConnectivity() {
  try {
    await Clove.ready();
    
    // Run network check
    const status = await Clove.network.status();
    
    if (status.online) {
      console.log(`Network is active. Connection medium: ${status.type}`);
    } else {
      console.warn("Device is running in offline standalone safe mode.");
    }
    
  } catch (error) {
    console.error("Failed to execute network telemetry tracking diagnostics:", error);
  }
}

verifyNetworkConnectivity();
```