# Clove.bluetooth.readUntil(delimiter)

Reads data from the internal native buffer stream up until it encounters a specific delimiter character sequence.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `delimiter` | `string` | The string sequence token defining completion parameters for chunk capture metrics. | `"\n"` |

## Return Type

* **Type:** `Promise<string>`
* **Description:** Resolves with the accumulated string payload up to and including the matching delimiter characters sequence.

## Code Example

```javascript
async function readNextDataLine() {
  const targetEndSequenceDelimiter = "\n";

  try {
    await Clove.ready();
    
    // Read up until a newline character is encountered
    const dataRow = await Clove.bluetooth.readUntil(targetEndSequenceDelimiter);
    console.log(`Extracted a complete data statement sequence: ${dataRow.trim()}`);
    
  } catch (error) {
    console.error("Failed to locate delimiter within tracking limits:", error);
  }
}

readNextDataLine();
```