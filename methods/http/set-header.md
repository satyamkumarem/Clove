# Clove.http.setHeader(host, header, value)

Configures persistent global HTTP request web header variables tied explicitly to a target host domain mapping profile. Once committed, all outgoing Clove HTTP requests routed to this matching host domain automatically inject this header configuration.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `host` | `string` | The target domain parsing matching configuration string to track (omit protocol headers like `https://`). | `"api.euome.com"` |
| `header` | `string` | The exact header identification key string sequence to configure globally. | `"Authorization"` |
| `value` | `string` | The content token string properties payload to map onto the global header variable space. | `"Bearer token_xyz"` |

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the header parameter mapping is successfully hard-coded inside the persistent native HTTP engine configuration states.

## Code Example

```javascript
async function configureGlobalAuthentication() {
  const domain = "api.euome.com";
  const tokenKey = "Authorization";
  const tokenCredentialValue = "Bearer secret_api_key_jwt_signature_here";

  try {
    await Clove.ready();
    
    // Commit persistent credentials header tracking line across the domain
    await Clove.http.setHeader(domain, tokenKey, tokenCredentialValue);
    console.log(`Persistent header successfully locked into domain engine profile: [${domain}]`);
    
    // Any future operations (e.g., Clove.http.get("[https://api.euome.com/status](https://api.euome.com/status)")) 
    // will now transparently include the Authorization header automatically!
    
  } catch (error) {
    console.error("Failed to commit global configuration parameters into native HTTP profile managers:", error);
  }
}

configureGlobalAuthentication();
```