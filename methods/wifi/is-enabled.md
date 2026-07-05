# Clove.wifi.isEnabled()

Queries the host handset infrastructure to ensure the integrated local Wi-Fi adapter transceiver is powered on.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<boolean>`
* **Description:** Resolves with `true` if the system wireless adapter hardware layer is fully turned on and accessible, or `false` if deactivated.

## Code Example

```javascript
async function evaluateWifiHardwareState() {
  try {
    await Clove.ready();
    
    // Query structural state
    const isWifiHardwareActive = await Clove.wifi.isEnabled();
    
    if (isWifiHardwareActive) {
      console.log("Host Wi-Fi controller architecture status line: [ACTIVE]");
    } else {
      console.warn("Host Wi-Fi physical transceiver adapter is currently completely turned off.");
    }
    
  } catch (error) {
    console.error("Failed to audit device wireless adapter hardware profiles:", error);
  }
}

evaluateWifiHardwareState();
```