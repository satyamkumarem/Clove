# Clove.ble.stopScan()

Terminates an ongoing active BLE hardware scanning loop prematurely.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves when the native BLE adapter successfully stops looking for peripheral broadcasts.

## Code Example

```javascript
async function forceCancelBleScan() {
  try {
    await Clove.ready();
    
    console.log("Requesting early termination of active BLE scanner...");
    await Clove.ble.stopScan();
    console.log("BLE airwave scanning sequence halted successfully.");
    
  } catch (error) {
    console.error("Failed to stop ongoing BLE scanning execution:", error);
  }
}

forceCancelBleScan();
```