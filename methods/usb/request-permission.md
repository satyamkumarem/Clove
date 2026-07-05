# Clove.usb.requestPermission(opts)

Requests explicit Android OS system-level permission from the user to communicate with a physically attached USB peripheral device.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `opts` | `Object` | Optional filter criteria used to target specific USB device hardware identifiers. | `{ vid: 1027, pid: 24577 }` |

### Key `opts` Filtering Matrix
| Property | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `vid` | `number` | The Vendor ID hex/integer of the target USB micro-controller asset. | `1027` (FTDI) |
| `pid` | `number` | The Product ID hex/integer of the target USB micro-controller asset. | `24577` |
| `driver` | `string` | Force a specific native USB-to-Serial driver profile implementation mapping. | `"Fx232Driver"` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value once the operator explicitly grants permission via the OS dialog viewport. Rejects if access is denied.

## Code Example

```javascript
async function initializeUsbHardwareAccess() {
  const hardwareTargetFilters = {
    vid: 1027, // Hex representation matching target peripheral vendors
    pid: 24577
  };

  try {
    await Clove.ready();
    console.log("Invoking native Android OS USB hardware access prompt...");
    
    await Clove.usb.requestPermission(hardwareTargetFilters);
    console.log("USB communication channel authorization approved by operator.");
    
  } catch (error) {
    console.error("USB interface access rejected or device disconnected from root port:", error);
  }
}

initializeUsbHardwareAccess();
```