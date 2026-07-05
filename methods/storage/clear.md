# Clove.storage.clear()

Wipes out all stored configurations, keys, and data payloads completely within the current application container profile sandbox.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the storage workspace directory has been completely wiped.

## Code Example

```javascript
async function factoryResetStorage() {
  try {
    await Clove.ready();
    
    console.warn("Wiping local persistent configurations...");
    // Clear the entire data sandbox
    await Clove.storage.clear();
    
    console.log("Storage wiped clean. All application key-value pairs are deleted.");
    
  } catch (error) {
    console.error("Failed to clear local application storage environment:", error);
  }
}

factoryResetStorage();
```