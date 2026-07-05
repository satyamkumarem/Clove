# Clove.http.put(url, data, options)

A convenience shorthand utility wrapper optimized to execute asynchronous HTTP PUT requests designed to perform complete state resource overrides.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `url` | `string` | The absolute destination endpoint tracking coordinate layout string path. | `"https://api.euome.com/v1/profiles/user_42"` |
| `data` | `any` | The full collection profile data object parameters bundle to overwrite the target resource. | `{ firstName: "John", status: "verified" }` |
| `options` | `Object` | Optional configurations metadata object mapping options (such as target custom header structures). | `{ headers: { "X-Audit-Reason": "manual_override" } }` |

## Return Type

* **Type:** `Promise<Object>`
* **Description:** Resolves with a standardized response layout interface model object matching `{ ok, status, body, headers }`.

## Code Example

```javascript
async function overwriteUserProfile() {
  const profileUrl = "[https://api.euome.com/v1/profiles/user_42](https://api.euome.com/v1/profiles/user_42)";
  const completeProfileState = {
    username: "dev_pioneer",
    accessRole: "administrator",
    securityClearance: "level_5"
  };

  try {
    await Clove.ready();
    
    // Commit state override via PUT request pipeline
    const response = await Clove.http.put(profileUrl, completeProfileState);
    
    if (response.status === 200 || response.status === 204) {
      console.log("User data profile records completely updated on server storage.");
    }
    
  } catch (error) {
    console.error("Failed to execute state replacement transaction pipeline:", error);
  }
}

overwriteUserProfile();
```