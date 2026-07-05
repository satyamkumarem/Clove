# Clove.notification.beep(times)

Forces the host system's audio speaker hardware modules to cycle standardized acoustic tracking tone alert sounds.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `times` | `number` | The absolute total number of sequential acoustic beep sound cycles to repeat natively. | `2` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value once the native hardware drivers finish cycling the audio beep signal tracks completely.

## Code Example

```javascript
async function alertOperatorOnHardwareCritical() {
  const loopCountCycleQuantity = 3;

  try {
    await Clove.ready();
    console.warn("Triggering high-priority sound signals across hardware driver layers...");
    
    // Force sound alert iteration loops
    await Clove.notification.beep(loopCountCycleQuantity);
    console.log("Audio audio tracking tone pulses fired cleanly into localized speaker modules.");
    
  } catch (error) {
    console.error("Failed to map sound generation triggers down straight into native audio boards:", error);
  }
}

alertOperatorOnHardwareCritical();
```