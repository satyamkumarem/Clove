# Clove.wifi.connect(ssid, password)

Attempts to authenticate and associate the device's wireless adapter radio pipelines with a specified network access point.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `ssid` | `string` | The exact target broadcast network tracking name string to bind with. | `"Office_Guest_Secure"` |
| `password` | `string` | The secure WPA/WPA2 pre-shared key security authentication credentials payload tracking string. | `"SecretPasscode99"` |

## Return Type

* **Type:** `Promise<boolean>`
* **Description:** Resolves with `true` if the handshake, authentication, and DHCP lease allocations establish connection paths successfully, or `false` if rejected.

## Code Example

```javascript
async function connectToTargetHotspot() {
  const targetNetworkSsid = "Office_Guest_Secure";
  const securityCredentials = "SecretPasscode99";

  try {
    await Clove.ready();
    console.log(`Initiating Wi-Fi network routing request targeting: ${targetNetworkSsid}`);
    
    // Execute connection process pipeline
    const connectionSucceeded = await Clove.wifi.connect(targetNetworkSsid, securityCredentials);
    
    if (connectionSucceeded) {
      console.log("Wi-Fi link established successfully! Local route configurations synced.");
    } else {
      console.warn("Handshake rejected. Verify passphrase validation matrices.");
    }
    
  } catch (error) {
    console.error("Failed to map connection handshakes over wireless infrastructure drivers:", error);
  }
}

connectToTargetHotspot();
```