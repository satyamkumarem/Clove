# Clove.bluetooth.isConnected()

Audits the current connection pipeline map to determine if a functioning link session is active.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<boolean>`
* **Description:** Resolves with `true` if an SPP RFCOMM communication session is live and functional, or `false` if disconnected.

## Code Example

```javascript
async function verifySessionHealth() {
  try {
    await Clove.ready();
    
    // Check connection health matrices
    const isSessionLive = await Clove.bluetooth.isConnected();
    
    if (isSessionLive) {
      console.log("Bluetooth serial socket pipeline status link: [CONNECTED]");
    } else {
      console.warn("Bluetooth serial socket pipeline status link: [DISCONNECTED]");
    }
    
  } catch (error) {
    console.error("Failed to execute socket state tracking routines:", error);
  }
}

verifySessionHealth();
```