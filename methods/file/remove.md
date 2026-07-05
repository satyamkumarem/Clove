# Clove.file.remove(path)

Deletes target file properties from internal app container disk storage blocks permanently.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `path` | `string` | The explicit path tracking coordinate layout mapping of the target file to erase. | `"temp/cache.tmp"` |

## Return Type

* **Type:** `Promise<any>`
* **Description:** Resolves successfully with an operation status verification payload when the target resource file system node has been cleanly unlinked and purged from disk storage partitions.

## Code Example

```javascript
async function clearTemporaryCache() {
  const targetCacheFile = "temp/cache.tmp";

  try {
    await Clove.ready();
    
    console.log(`Purging structural cache resource file node tracking lines: ${targetCacheFile}`);
    
    // Execute destruction payload pipeline
    await Clove.file.remove(targetCacheFile);
    console.log("Cache file block cleared securely from internal application partition layers.");
    
  } catch (error) {
    console.error("Failed to drop cache structures from device file architecture configuration profiles:", error);
  }
}

clearTemporaryCache();
```