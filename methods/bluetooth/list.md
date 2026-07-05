# Clove.bluetooth.list()

Queries the host Android system to retrieve a collection of all bonded (paired) Bluetooth Classic devices.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<Array<Object>>`
* **Description:** Resolves with an array of objects representing paired peripheral devices.

### Array Element Properties:
| Property | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `name` | `string` | The human-readable broadcast identifier name of the peripheral. | `"HC-05-Serial"` |
| `address` | `string` | The unique physical hardware MAC address sequence of the module. | `"00:14:03:05:59:BA"` |
| `id` | `string` | Distinct system tracking reference matching the MAC address mapping. | `"00:14:03:05:59:BA"` |

## Code Example

```javascript
async function getPairedDevices() {
  try {
    await Clove.ready();
    
    console.log("Fetching list of bonded Bluetooth Classic devices...");
    const pairedDevices = await Clove.bluetooth.list();
    
    console.log(`Found ${pairedDevices.length} paired devices.`);
    pairedDevices.forEach(device => {
      console.log(`-> Name: ${device.name} | MAC: ${device.address}`);
    });
    
  } catch (error) {
    console.error("Failed to retrieve paired device roster:", error);
  }
}

getPairedDevices();
```