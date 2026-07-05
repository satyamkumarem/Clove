# Clove.file.read(path, options)

Loads a localized file resource from the secure sandboxed application container directly back into runtime memory.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `path` | `string` | Target file structural path coordinate mapping string to read from disk storage. | `"logs/sensor.txt"` |
| `options` | `Object` | Optional parameters mapping configuration schema used to dictate character data format rules. | `{ mode: "text" }` |

### Parameter Details

#### `options` Object Properties:
* **`mode`** (`string`): Defines parsing context rules. Supported configurations: `"text"` or `"json"`. Defaults to `"text"` if omitted.

## Return Type

* **Type:** `Promise<any>`
* **Description:** Resolves with the extracted content of the file. Returns a clean primitive string configuration if `mode: "text"`, or a parsed JavaScript Object/Array if configured for `"json"`.

## Code Example

```javascript
async function loadSavedLogs() {
  try {
    await Clove.ready();
    
    const configurationOptions = { mode: "text" };
    
    // Execute data reading transaction pipeline
    const fileContents = await Clove.file.read("logs/sensor.txt", configurationOptions);
    
    console.log("File loaded from disk cleanly:");
    console.log(fileContents);
    
  } catch (error) {
    console.error("Failed to parse and extract target data logs configuration track:", error);
  }
}

loadSavedLogs();
```