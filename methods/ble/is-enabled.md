# Clove.ble.isEnabled()

Queries the host platform environment to verify if the system Bluetooth Low Energy hardware controller functions are active.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<boolean>`
* **Description:** Resolves with `true` if the host BLE radio hardware stack is fully turned on and accessible, or `false` if it is inactive.

## Code Example

```javascript
async function checkBleAdapterHealthStatus() {
  try {
    await Clove.ready();
    
    const isBleActive = await Clove.ble.isEnabled();
    
    if (isBleActive) {
      console.log("Device Bluetooth Low Energy driver layer confirms status: [READY]");
    } else {
      console.warn("Device Bluetooth Low Energy adapter is down. Enable system Bluetooth settings.");
    }
    
  } catch (error) {
    console.error("Failed to read hardware controller tracking states:", error);
  }
}

checkBleAdapterHealthStatus();
```