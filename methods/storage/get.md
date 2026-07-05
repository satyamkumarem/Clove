# Clove.storage.get(key)

Retrieves a value from the application's permanent sandboxed key-value storage system.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `key` | `string` | The target key mapping lookup name used to identify the saved data. | `"session_uid"` |

## Return Type

* **Type:** `Promise<any>`
* **Description:** Resolves with the stored content payload. Primitive values, arrays, and objects are automatically parsed back into their original JavaScript data types. Resolves with `null` if the key does not exist.

## Code Example

```javascript
async function getUserSession() {
  try {
    await Clove.ready();
    
    // Retrieve the stored session ID
    const userId = await Clove.storage.get("session_uid");
    
    if (userId) {
      console.log(`Retrieved active session ID: ${userId}`);
    } else {
      console.log("No active user session found in persistent storage.");
    }
    
  } catch (error) {
    console.error("Failed to read from persistent storage:", error);
  }
}

getUserSession();
```