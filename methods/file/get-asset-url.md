# Clove.file.getAssetURL(path)

Transforms internal sandboxed data asset paths into absolute web-friendly URL vectors to seamlessly map files inside standard browser HTML DOM context tags.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `path` | `string` | Local sandboxed repository file pointer tracking line mapping string. | `"photos/device_icon.png"` |

## Return Type

* **Type:** `Promise<string>`
* **Description:** Resolves with an absolute, browser-executable URL string token configuration pointing directly towards the localized asset resource stream mapping.

## Code Example

```javascript
async function renderDeviceProfilePicture() {
  const targetLocalResource = "photos/device_icon.png";

  try {
    await Clove.ready();
    
    // Transpile sandboxed asset into localized absolute URL resource vector tokens
    const publicAssetUrlString = await Clove.file.getAssetURL(targetLocalResource);
    
    console.log(`Generated browser-safe URL rendering target reference point: ${publicAssetUrlString}`);
    
    // Bind generated resource asset directly into DOM viewport element
    document.getElementById("avatar-display-node").src = publicAssetUrlString;
    
  } catch (error) {
    console.error("Failed to map secure platform path blocks cleanly down onto local asset URLs:", error);
  }
}

renderDeviceProfilePicture();
```