# Clove.file.exists(path)

Checks for the physical presence of a target file profile structure inside the application's isolated storage sandboxed directories.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `path` | `string` | Target file path tracking coordinates schema string to audit. | `"branding/logo.png"` |

## Return Type

* **Type:** `Promise<boolean>`
* **Description:** Resolves with `true` if the target structural tracking pathway matches a physical asset file currently residing on disk, or `false` if it does not exist.

## Code Example

```javascript
async function verifyAssetAvailability() {
  const targetLogoPath = "branding/logo.png";

  try {
    await Clove.ready();
    
    // Verify file profile presence
    const fileExists = await Clove.file.exists(targetLogoPath);
    
    if (fileExists) {
      console.log(`Verified mapping check: ${targetLogoPath} is available on disk.`);
    } else {
      console.warn(`Target reference file is completely missing from runtime storage coordinates.`);
    }
    
  } catch (error) {
    console.error("Failed to compile diagnostic checks targeting application file paths:", error);
  }
}

verifyAssetAvailability();
```