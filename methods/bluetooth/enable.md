# Clove.bluetooth.enable()

Prompts the user via native OS-level dialogs to turn on the device's Bluetooth radio hardware adapter.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<boolean>`
* **Description:** Resolves with `true` if the radio adapter transitions cleanly into a fully operational active state, or `false` if the initialization request is rejected.

## Code Example

```javascript
async function ensureBluetoothIsActive() {
  try {
    await Clove.ready();
    
    const isHardwareReady = await Clove.bluetooth.isEnabled();
    
    if (!isHardwareReady) {
      console.log("Requesting system intervention to power on the Bluetooth radio adapter...");
      
      // Fire activation intent sequence
      const activationSuccess = await Clove.bluetooth.enable();
      
      if (activationSuccess) {
        console.log("Bluetooth hardware has been powered on by user verification layout.");
      } else {
        console.warn("User declined or hardware failed to switch the Bluetooth radio module on.");
      }
    } else {
      console.log("Bluetooth hardware is already powered on and ready.");
    }
    
  } catch (error) {
    console.error("Failed to invoke native system hardware toggle utilities:", error);
  }
}

ensureBluetoothIsActive();
```