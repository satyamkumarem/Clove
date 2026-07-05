# Clove.http.delete(url, options)

A convenience shorthand utility wrapper optimized to execute asynchronous HTTP DELETE request command properties targeting remote host assets.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `url` | `string` | The absolute target web destination resource coordinate mapping endpoint tracking string. | `"https://api.euome.com/v1/cache/purge-all"` |
| `options` | `Object` | Optional configuration properties bundle (such as localized request headers). | `{ headers: { "X-Confirm-Purge": "true" } }` |

## Return Type

* **Type:** `Promise<Object>`
* **Description:** Resolves with a standardized response layout interface model object matching `{ ok, status, body, headers }`.

## Code Example

```javascript
async function clearRemoteServerCache() {
  const targetPurgeUrl = "[https://api.euome.com/v1/cache/purge-all](https://api.euome.com/v1/cache/purge-all)";

  try {
    await Clove.ready();
    
    // Execute resource destruction via DELETE request format
    const response = await Clove.http.delete(targetPurgeUrl);
    
    if (response.ok) {
      console.log("Remote server cache structures dismantled successfully.");
    }
    
  } catch (error) {
    console.error("Failed to transmit asset destruction requests up along networking pipelines:", error);
  }
}

clearRemoteServerCache();
```