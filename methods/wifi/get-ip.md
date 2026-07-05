# Clove.wifi.getIP()

Queries the active local network interface connection to resolve the IP address assigned to the host Android device.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<string \| null>`
* **Description:** Resolves with the localized IPv4 addressing string assigned to the device, or `null` if no network interface addressing routing exists.

## Code Example

```javascript
async function resolveLocalIpAddress() {
  try {
    await Clove.ready();
    
    // Fetch local network IP configuration
    const localIpAddress = await Clove.wifi.getIP();
    
    if (localIpAddress) {
      console.log(`Device localized IP routing coordinate: ${localIpAddress}`);
    } else {
      console.warn("No valid IP binding found. Check adapter connection health matrix.");
    }
    
  } catch (error) {
    console.error("Failed to query localized interface addressing parameters:", error);
  }
}

resolveLocalIpAddress();
```