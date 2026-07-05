# Clove.notification.prompt(msg, title, btns, defText)

Launches a modal dialogue interface template complete with interactive native keyboard entry text field maps.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `msg` | `string` | The explanatory request instruction string text positioned above the input component field. | `"Enter new server target endpoint address:"` |
| `title` | `string` | The tracking identification layout heading text applied onto the dialogue window frame. | `"Routing Alteration"` |
| `btns` | `Array<string>` | An array mapping textual labels intended to manage interaction action buttons. | `["Cancel", "Commit"]` |
| `defText` | `string` | Default fallback validation template text pre-populated directly into the keyboard text entry input wrapper. | `"192.168.1.1"` |

## Return Type

* **Type:** `Promise<Object>`
* **Description:** Resolves with a structured response tracker object isolating user input profiles.

### Return Object Properties:
| Property | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `buttonIndex` | `number` | The **1-based index** reference tracker noting which layout button string option was selected. | `2` |
| `input1` | `string` | The exact textual data contents extracted out from the entry input form layer. | `"192.168.1.50"` |

## Code Example

```javascript
async function modifyTargetEndpointUrl() {
  const instructionPrompt = "Please map the absolute destination server routing gateway address details below:";
  const header = "Endpoint Assignment Trace";
  const layoutButtons = ["Discard", "Save Settings"];
  const baselineDefaultPlaceholder = "[https://api.euome.com/v1](https://api.euome.com/v1)";

  try {
    await Clove.ready();
    
    // Spin up text collection prompt modal interface context elements
    const interactionResponse = await Clove.notification.prompt(instructionPrompt, header, layoutButtons, baselineDefaultPlaceholder);
    
    // Check if the user selected 'Save Settings' (Button index position 2)
    if (interactionResponse.buttonIndex === 2) {
      const configurationUrlResult = interactionResponse.input1;
      console.log(`Successfully intercepted manual URL re-routing entry parameter points: ${configurationUrlResult}`);
      // Apply re-routing transformations here
    } else {
      console.log("Configuration update loops abandoned by user request.");
    }
    
  } catch (error) {
    console.error("Failed to launch input layout overlay modules across display drivers:", error);
  }
}

modifyTargetEndpointUrl();
```