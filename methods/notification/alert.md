# Clove.notification.alert(msg, title, btn)

Displays a native modal system alert dialog box frame overlaying the interface to show a critical feedback message.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `msg` | `string` | The primary content message text body to render inside the dialog viewport. | `"Operation finished cleanly!"` |
| `title` | `string` | The header label title text displayed at the top section of the alert box. | `"System Check"` |
| `btn` | `string` | The text label tracking option to assign to the dismissive confirmation action button. | `"Dismiss"` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the user taps the acknowledgment confirmation button to close the dialogue window frame.

## Code Example

```javascript
async function triggerSystemAlert() {
  const alertText = "Device calibrations updated completely across physical hardware registers.";
  const windowHeaderTitle = "Calibration System Check";
  const confirmationButtonText = "Acknowledge";

  try {
    await Clove.ready();
    
    console.log("Launching modal popup warning UI components...");
    // Present native alert window frames
    await Clove.notification.alert(alertText, windowHeaderTitle, confirmationButtonText);
    
    console.log("User closed the dialog box configuration profile.");
    
  } catch (error) {
    console.error("Failed to draw native UI dialog frames over application layers:", error);
  }
}

triggerSystemAlert();
```