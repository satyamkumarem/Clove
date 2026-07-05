# Clove.storage.remove(key)

Purges a matching record key and its associated value from the application's persistent sandboxed storage blocks.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `key` | `string` | The target key mapping name to be deleted from storage. | `"session_uid"` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the target key sequence is successfully destroyed or if it did not exist.

## Code Example

```javascript
async function logoutUser() {
  try {
    await Clove.ready();
    
    // Delete the single session key
    await Clove.storage.remove("session_uid");
    console.log("Session token purged. User logged out locally.");
    
  } catch (error) {
    console.error("Failed to remove target key from storage profile:", error);
  }
}

logoutUser();
```