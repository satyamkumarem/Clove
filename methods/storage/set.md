# Clove.storage.set(key, value)

Saves primitives, objects, or arrays into permanent sandboxed storage. Objects and structural arrays are automatically transformed into valid JSON string representations natively before being committed to disk.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `key` | `string` | Target key mapping variable assignment name. | `"user_settings"` |
| `value` | `any` | The content payload (string, number, boolean, array, or object) to commit to permanent storage. | `{ darkMode: true, interval: 1000 }` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the data structure has been successfully written and synced to persistent disk storage.

## Code Example

```javascript
async function saveUserSettings() {
  const settings = {
    darkMode: true,
    syncInterval: 5000,
    tags: ["iot", "mobile", "clove"]
  };

  try {
    await Clove.ready();
    
    // Commit the object to storage
    await Clove.storage.set("user_settings", settings);
    console.log("User settings saved securely to persistent disk.");
    
  } catch (error) {
    console.error("Failed to write configurations to storage:", error);
  }
}

saveUserSettings();
```