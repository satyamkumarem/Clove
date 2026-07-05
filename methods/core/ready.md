# Clove.ready()

Blocks JavaScript runtime execution until the background native channel between the WebView container and the Android operating system is verified and established. This must be resolved before any hardware or network methods are executed.

## Parameters

This method does not accept any parameters.

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the bridge connection is established and safe to use. Rejects if the native bridge fails to initialize.

## Code Example

```javascript
async function initializeApp() {
  try {
    console.log("Initializing native bridge...");
    
    // Block execution until Clove is ready
    await Clove.ready();
    
    console.log("Clove bridge is online! Safe to call hardware APIs.");
    // You can now safely call other Clove methods here
    
  } catch (error) {
    console.error("Bridge initialization failed:", error);
  }
}

initializeApp();
```