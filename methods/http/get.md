# Clove.http.get(url, options)

A convenience shorthand utility wrapper optimized to execute asynchronous HTTP GET web request operations.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `url` | `string` | The absolute target web endpoint path address tracking string. | `"https://api.euome.com/status"` |
| `options` | `Object` | Optional secondary configurations metadata map (such as custom `headers`). | `{ headers: { "Accept": "application/json" } }` |

## Return Type

* **Type:** `Promise<Object>`
* **Description:** Resolves with a standardized response layout interface model object matching `{ ok, status, body, headers }`.

## Code Example

```javascript
async function checkSystemStatus() {
  const targetUrl = "[https://api.euome.com/status](https://api.euome.com/status)";

  try {
    await Clove.ready();
    
    // Execute GET transaction
    const response = await Clove.http.get(targetUrl);
    
    if (response.ok) {
      console.log("System diagnostic state resolved cleanly:", response.body);
    } else {
      console.warn(`Server responded with code tracking error metric: ${response.status}`);
    }
    
  } catch (error) {
    console.error("Failed to run HTTP GET request configuration pipeline:", error);
  }
}

checkSystemStatus();
```