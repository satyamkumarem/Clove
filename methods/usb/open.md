# Clove.usb.open(opts)

Opens a direct serial data line connection channel over the physical USB interface layout using specified communication criteria.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `opts` | `Object` | Connection configuration properties dictating line speed, parity checks, and bit streams. | `{ baudRate: 9600, dataBits: 8 }` |

### Common `opts` Line Properties
| Property | Type | Description | Default / Options |
| :--- | :--- | :--- | :--- |
| `baudRate` | `number` | Sequential communication speed metric bits-per-second rate. | `9600`, `115200` |
| `dataBits` | `number` | Number of sequential data bits transmitted per frame structure pack. | `8` (Standard), `7` |
| `stopBits` | `number` | Sequential stop bits utilized to flag frame termination markers. | `1` (Standard), `2` |
| `parity` | `number` | Parity bit error monitoring scheme definition rules. | `0` (None), `1` (Odd), `2` (Even) |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the internal native UART/Serial parameters link up successfully with the target device.

## Code Example

```javascript
async function openSerialPipeline() {
  const lineConfiguration = {
    baudRate: 115200,
    dataBits: 8,
    stopBits: 1,
    parity: 0
  };

  try {
    await Clove.ready();
    console.log("Configuring serial terminal lines over active physical port connection...");
    
    await Clove.usb.open(lineConfiguration);
    console.log("USB serial communication pipe is now completely open and active.");
    
  } catch (error) {
    console.error("Failed to sync serial line parameters with the connected hardware node:", error);
  }
}
```