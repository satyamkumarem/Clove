# Clove.wifi.getSSID()

Retrieves the Service Set Identifier (SSID)—the broadcast network name—of the Wi-Fi access point to which the device is currently connected.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<string \| null>`
* **Description:** Resolves with the network SSID string if the device is actively associated with a Wi-Fi network, or `null` if the Wi-Fi interface is disconnected.

## Code Example

```javascript
async function identifyCurrentNetwork() {
  try {
    await Clove.ready();
    
    // Fetch active SSID string
    const currentSsid = await Clove.wifi.getSSID();
    
    if (currentSsid) {
      console.log(`Device is currently associated with Wi-Fi network: [${currentSsid}]`);
    } else {
      console.warn("The device is not associated with an active Wi-Fi access point.");
    }
    
  } catch (error) {
    console.error("Failed to extract active Wi-Fi network name profiles:", error);
  }
}

identifyCurrentNetwork();
```