# Clove.camera.getPicture(opts)

Launches the device's native camera application interface to capture a new photo, or opens the system photo gallery to retrieve an existing image file.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `opts` | `Object` | Configuration options controlling image properties (quality, format, dimensions, source type). Maps directly to native Cordova Camera properties. | `{ quality: 75, destinationType: 0 }` |

### Key `opts` Configuration Matrix
| Property | Type | Description | Common Settings |
| :--- | :--- | :--- | :--- |
| `quality` | `number` | Compression ratio of the saved image, scale ranging from `0` to `100`. | `50` (Default balance) |
| `destinationType` | `number` | Format structure of the returned image payload coordinate string. | `0` (Base64 String Data), `1` (Local File URI) |
| `sourceType` | `number` | The hardware origin source location to pull the picture asset from. | `1` (Physical Camera), `0` (Photo Library) |
| `encodingType` | `number` | Choose the compressed image binary wrapper encoding scheme format. | `0` (JPEG representation), `1` (PNG layout) |
| `targetWidth` | `number` | Target width in pixels to automatically scale the captured frame image. | `800` |
| `targetHeight` | `number` | Target height in pixels to automatically scale the captured frame image. | `800` |

## Return Type

* **Type:** `Promise<string>`
* **Description:** Resolves with either a raw Base64 image data string or a localized system file path string asset pointer, corresponding to your defined `destinationType`.

## Code Example

```javascript
async function captureUserAvatar() {
  // Configured to launch camera and export clean Base64 data strings directly
  const captureConfig = {
    quality: 80,
    destinationType: 0, // Request Base64 Data URL payload
    sourceType: 1,      // Force open physical hardware lens array
    encodingType: 0,     // Output standard compressed JPEG data bytes
    targetWidth: 600,
    targetHeight: 600
  };

  try {
    await Clove.ready();
    console.log("Requesting background pipeline authorization for camera intents...");
    
    const base64DataPayload = await Clove.camera.getPicture(captureConfig);
    
    // Bind base64 payload layout data blocks straight to DOM elements
    const avatarImgElement = document.getElementById("user-avatar-display");
    if (avatarImgElement) {
      avatarImgElement.src = `data:image/jpeg;base64,${base64DataPayload}`;
      console.log("Native image transaction resolved successfully.");
    }
    
  } catch (error) {
    console.error("Camera viewport interface dismissed or runtime connection failed:", error);
  }
}

captureUserAvatar();
```