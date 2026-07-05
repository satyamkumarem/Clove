# Clove.notification.confirm(msg, title, btns)

Presents user selections within interactive native multi-button layout models, allowing interactive branching path execution based on their choice.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `msg` | `string` | The actionable confirmation directive query string presented to the user. | `"Wipe device configuration partitions?"` |
| `title` | `string` | The header title label mapping string applied onto the top boundary profile. | `"System Purge"` |
| `btns` | `Array<string>` | An array containing label text mapping configurations for custom buttons to instantiate inside the modal interface. | `["Abort", "Confirm Reset"]` |

## Return Type

* **Type:** `Promise<number>`
* **Description:** Resolves with a **1-based index** integer mapping corresponding strictly to the order index position of the chosen button array path elements. Returns `0` if the interaction frame is dismissed without a direct selection event.

## Code Example

```javascript
async function promptDatabaseWipe() {
  const confirmationQueryText = "Do you want to clear out all localized telemetry tracking databases from storage permanently?";
  const dialogBoxHeader = "Destructive System Action";
  const choiceSelections = ["Cancel", "Proceed Wipe"]; // Button 1 index mapping: 1, Button 2 mapping: 2

  try {
    await Clove.ready();
    
    // Spawn interactive confirmation layout block
    const userChoiceIndex = await Clove.notification.confirm(confirmationQueryText, dialogBoxHeader, choiceSelections);
    
    if (userChoiceIndex === 2) {
      console.warn("User initiated target system data partition purge. Processing destroy sequence...");
      // Execute database wipe routines here
    } else {
      console.log("Destructive system action trace aborted by runtime operator.");
    }
    
  } catch (error) {
    console.error("Failed to build interactive prompt elements within native view windows:", error);
  }
}

promptDatabaseWipe();
```