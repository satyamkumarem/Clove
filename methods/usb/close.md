# Clove.usb.close()

Dismantles and terminates the active USB serial stream link connection, releasing the hardware port mapping handles back to the OS.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the interface line handles drop natively back to idle states.

## Code Example

```javascript
async function terminateUsbConnection() {
  try {
    await Clove.ready();
    console.log("Severing active serial pipeline connections natively...");
    
    await Clove.usb.close();
    console.log("USB hardware serial connection closed safely.");
    
  } catch (error) {
    console.error("An error occurred during physical USB port closing procedures:", error);
  }
}
```