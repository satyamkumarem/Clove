# Clove.notification.vibrate(ms)

Triggers physical haptic vibration eccentric rotating mass motor weights inside mechanical device housings for a specified duration.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `ms` | `number` | The exact time duration limit window measured in milliseconds to sustain continuous haptic motor operations. | `250` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value immediately when the native platform driver receives the haptic feedback command instructions.

## Code Example

```javascript
async function performErrorHapticFeedback() {
  const vibrationDurationWindowLimit = 500; // Define haptic operation tracking parameters for 500ms

  try {
    await Clove.ready();
    console.log("Initiating haptic tracking weight patterns...");
    
    // Spin up hardware mechanical vibration weights
    await Clove.notification.vibrate(vibrationDurationWindowLimit);
    console.log("Haptic feedback pulses distributed cleanly to physical device components.");
    
  } catch (error) {
    console.error("Failed to establish continuous control tracking over physical device haptic lines:", error);
  }
}

performErrorHapticFeedback();
```