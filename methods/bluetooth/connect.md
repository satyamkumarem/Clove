# Clove.bluetooth.connect(address)

Establishes a dedicated Serial Port Profile (SPP) RFCOMM communication link channel to a target peripheral module.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `address` | `string` | The hardware MAC address tracking string of the destination peripheral module. | `"00:14:03:05:59:BA"` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves successfully when the native SPP RFCOMM socket establishes a handshake connection with the hardware node.

## Code Example

```javascript
async function connectToSerialModule() {
  const targetMacAddress = "00:14:03:05:59:BA";

  try {
    await Clove.ready();
    console.log(`Attempting connection pipeline tracking straight to: ${targetMacAddress}`);
    
    // Connect to the device
    await Clove.bluetooth.connect(targetMacAddress);
    console.log("Connected successfully over Classic Bluetooth Serial Port Profile.");
    
  } catch (error) {
    console.error(`Failed to lock SPP link with target node [${targetMacAddress}]:`, error);
  }
}

connectToSerialModule();
```