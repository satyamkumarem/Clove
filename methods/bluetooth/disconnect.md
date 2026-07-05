# Clove.bluetooth.disconnect()

Closes the active Bluetooth Classic Serial Port Profile (SPP) connection socket.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the internal socket connection loops have been safely torn down.

## Code Example

```javascript
async function closeActiveConnection() {
  try {
    await Clove.ready();
    
    console.log("Tearing down active serial link channels...");
    await Clove.bluetooth.disconnect();
    
    console.log("Bluetooth serial channel closed safely.");
    
  } catch (error) {
    console.error("Failed to disconnect from the active session cleanly:", error);
  }
}

closeActiveConnection();
```