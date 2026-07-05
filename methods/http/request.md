# Clove.http.request(options)

A low-level foundational networking engine wrapper designed to execute highly customized asynchronous HTTP web request configurations. 

> ⚠️ **CORS Bypass Feature:** Because these requests are routed entirely through low-level native Android socket pipelines, they completely bypass standard browser-enforced Same-Origin Policy (CORS) rules.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `options` | `Object` | Configuration criteria defining the request method, target URL, payloads, and request-specific header mappings. | See properties details below. |

### Parameter Details

#### `options` Object Properties:
* **`method`** (`string`): The HTTP verb payload mechanism. Supported options: `"GET"`, `"POST"`, `"PUT"`, `"PATCH"`, or `"DELETE"`.
* **`url`** (`string`): The absolute destination endpoint URL path routing address string.
* **`data`** (`Object \| string \| Array`): Optional payload context parameters bundle to transmit downstream (typically for POST, PUT, or PATCH commands).
* **`headers`** (`Object`): Optional key-value structural configuration mapping for request-specific headers.

## Return Type

* **Type:** `Promise<Object>`
* **Description:** Resolves with a structured response metadata object detailing request evaluation metrics.

### Return Object Properties:
| Property | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `ok` | `boolean` | Flag tracking status validation code metrics between 200–299 range structures. | `true` |
| `status` | `number` | The exact HTTP status integer returned by the processing server. | `201` |
| `body` | `any` | The raw or automatically parsed context response body content payload. | `{ id: "node_12", status: "active" }` |
| `headers` | `Object` | Key-value mapping pairs detailing response headers sent back by the host. | `{ "content-type": "application/json" }` |

## Code Example

```javascript
async function executeCustomWebRequest() {
  const customConfig = {
    method: "POST",
    url: "[https://api.euome.com/v1/sensors](https://api.euome.com/v1/sensors)",
    headers: {
      "X-Custom-Client-Token": "hardware_node_alpha_99"
    },
    data: {
      sensorId: "temp_probe_01",
      reading: 24.85
    }
  };

  try {
    await Clove.ready();
    console.log("Dispatching low-level native HTTP socket request...");
    
    // Fire custom request pipeline
    const response = await Clove.http.request(customConfig);
    
    if (response.ok) {
      console.log(`Server responded with status code: ${response.status}`);
      console.log("Payload data processed cleanly:", response.body);
    } else {
      console.error(`HTTP request rejected with server status code: ${response.status}`);
    }
    
  } catch (error) {
    console.error("Critical socket pipeline execution failure:", error);
  }
}

executeCustomWebRequest();
```