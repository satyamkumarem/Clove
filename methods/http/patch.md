# Clove.http.patch(url, data, options)

A convenience shorthand utility wrapper optimized to dispatch asynchronous HTTP PATCH requests designed to execute incremental mutations on data subsets.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `url` | `string` | The absolute destination target API structural endpoint route mapping string. | `"https://api.euome.com/v1/devices/node_7"` |
| `data` | `any` | A partial configuration data object containing individual field changes to apply to the resource. | `{ isActive: false }` |
| `options` | `Object` | Optional request configuration mapping properties parameters block. | `{ headers: { "Authorization": "Bearer token_abc" } }` |

## Return Type

* **Type:** `Promise<Object>`
* **Description:** Resolves with a standardized response layout interface model object matching `{ ok, status, body, headers }`.

## Code Example

```javascript
async function deactivateTargetDevice() {
  const nodePatchEndpoint = "[https://api.euome.com/v1/devices/node_7](https://api.euome.com/v1/devices/node_7)";
  const partialStateDelta = { isActive: false };

  try {
    await Clove.ready();
    
    // Issue partial state updates via PATCH
    const response = await Clove.http.patch(nodePatchEndpoint, partialStateDelta);
    
    if (response.ok) {
      console.log("Device records successfully mutated. Target node is now deactivated.");
    }
    
  } catch (error) {
    console.error("Failed to map partial parameter modifications onto processing network server:", error);
  }
}

deactivateTargetDevice();
```