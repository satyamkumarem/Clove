# Clove.wifi.disconnect()

Severs connection associations completely with the active Wi-Fi endpoint station, dropping address bindings.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the interface association handles drop cleanly and return back to idle monitoring status tracking modes.

## Code Example

```javascript
async function terminateActiveWirelessLink() {
  try {
    await Clove.ready();
    
    console.log("Severing active network adapter association blocks...");
    await Clove.wifi.disconnect();
    console.log("Wi-Fi network connection terminated safely.");
    
  } catch (error) {
    console.error("Failed to cleanly disconnect the current Wi-Fi configuration tracking line:", error);
  }
}

terminateActiveWirelessLink();
```