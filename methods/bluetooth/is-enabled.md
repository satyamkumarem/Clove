# Clove.bluetooth.isEnabled()

Queries the physical device to determine if the internal Bluetooth radio hardware adapter is turned on.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<boolean>`
* **Description:** Resolves with `true` if the system Bluetooth transceiver module is switched on and ready, or `false` if it is currently disabled.

## Code Example

```javascript
async function checkRadioHardwareState() {
  try {
    await Clove.ready();
    
    // Query physical adapter status
    const isRadioPoweredOn = await Clove.bluetooth.isEnabled();
    
    if (isRadioPoweredOn) {
      console.log("Host Bluetooth adapter hardware is active and scanning ready.");
    } else {
      console.warn("Host Bluetooth radio transceiver is completely powered down.");
    }
    
  } catch (error) {
    console.error("Failed to extract structural hardware radio state configurations:", error);
  }
}

checkRadioHardwareState();
```