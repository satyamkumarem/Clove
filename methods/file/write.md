# Clove.file.write(path, data)

Writes raw string buffers or objects to a localized file target directory path inside the application's secure storage sandbox.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `path` | `string` | The target filename path tracking string relative to the app data root. | `"logs/sensor.txt"` |
| `data` | `string \| Object` | Payload context strings or structured data objects to write to the file. | `"Data Entry Line 1\n"` |

### Parameter Details
* If an object or array is passed into the `data` parameter, the system will automatically format it into a valid serialized JSON string before committing it to disk.

## Return Type

* **Type:** `Promise<any>`
* **Description:** Resolves with an operational success confirmation metric metadata object once the data writing stream is flushed cleanly onto the storage partition.

## Code Example

```javascript
async function appendSensorData() {
  const logPath = "logs/sensor.txt";
  const logContent = `Timestamp: ${Date.now()} - Sensor Value: 42.8\n`;

  try {
    await Clove.ready();
    
    // Commit content to disk path
    await Clove.file.write(logPath, logContent);
    console.log(`Successfully compiled entries onto file: ${logPath}`);
    
  } catch (error) {
    console.error("Failed to commit payload metrics directly into sandboxed file track:", error);
  }
}

appendSensorData();
```