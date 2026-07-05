# Clove.device.info()

Queries the host Android handset to expose fundamental platform hardware properties and unique identification strings.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<Object>`
* **Description:** Resolves with an object detailing the physical device architecture properties.

### Return Object Properties:
| Property | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `manufacturer` | `string` | The company that manufactured the device hardware. | `"Samsung"` |
| `model` | `string` | The structural model name designation of the device. | `"Galaxy S23"` |
| `platform` | `string` | The host operating system running the application environment. | `"Android"` |
| `version` | `string` | The exact firmware OS version configuration details. | `"14.0.0"` |
| `uuid` | `string` | Universally unique identifier tied permanently to the device hardware profile. | `"9774d56d682e3b4d"` |

## Code Example

```javascript
async function checkDeviceHardware() {
  try {
    await Clove.ready();
    
    // Fetch system properties
    const hardwareInfo = await Clove.device.info();
    
    console.log("Device profile fetched successfully:", hardwareInfo);
    console.log(`Running on: ${hardwareInfo.manufacturer} ${hardwareInfo.model}`);
    console.log(`OS Build Version: ${hardwareInfo.version}`);
    
  } catch (error) {
    console.error("Failed to query hardware properties:", error);
  }
}

checkDeviceHardware();
```