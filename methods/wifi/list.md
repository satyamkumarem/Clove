# Clove.wifi.list()

Triggers a localized infrastructure scan of nearby Wi-Fi network access points broadcasting signals over available bands.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<Array<Object>>`
* **Description:** Resolves with a list array collection detailing local wireless infrastructure hotspots detected during the execution frame window.

### Array Element Properties:
| Property | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `ssid` | `string` | The human-readable broadcast tracking identity name string of the hotspot network. | `"Office_Guest_Secure"` |
| `bssid` | `string` | The physical hardware MAC routing address of the specific access point radio transceiver. | `"AA:11:BB:22:CC:33"` |
| `level` | `number` | The received signal power calculation measured in dBm metrics. | `-58` |

## Code Example

```javascript
async function scanForWirelessHotspots() {
  try {
    await Clove.ready();
    console.log("Triggering physical airwave scan for nearby Wi-Fi endpoints...");
    
    // Query available station rosters
    const availableNetworks = await Clove.wifi.list();
    
    console.log(`Scan phase concluded. Discovered ${availableNetworks.length} endpoints.`);
    availableNetworks.forEach(network => {
      console.log(`-> SSID: ${network.ssid || "[Hidden]"} | Signal Strength: ${network.level} dBm | BSSID: ${network.bssid}`);
    });
    
  } catch (error) {
    console.error("Failed executing structural infrastructure airwave scans:", error);
  }
}

scanForWirelessHotspots();
```