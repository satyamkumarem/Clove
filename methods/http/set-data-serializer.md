# Clove.http.setDataSerializer(serializer)

Alters the default outbound payload body encoding serialization data model pipeline for all subsequent native HTTP requests.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `serializer` | `string` | The explicit target format string key name mapping selection to enforce globally. | `"urlencoded"` |

> 💡 **Supported values for `serializer`:**
> * `"json"` - Direct JSON mapping strings transformation (Default setup formatting option).
> * `"urlencoded"` - `application/x-www-form-urlencoded` key-value pairs text stream blocks conversion.
> * `"utf8"` - Encodes raw processing data tracks as raw string text context blocks.
> * `"multipart"` - Form data boundary chunk streams parsing optimization routines (useful for multi-part file uploads).

## Return Type

* **Type:** `Promise<void>`
* **Description:** Resolves with no value when the serialization pipeline rules have been updated natively.

## Code Example

```javascript
async function shiftNetworkPayloadFormat() {
  try {
    await Clove.ready();
    
    console.log("Reconfiguring default network serialization mechanism to Form URL Encoding standard...");
    
    // Alter default formatting pipeline engine characteristics globally
    await Clove.http.setDataSerializer("urlencoded");
    console.log("Global networking serializer shifted to: [urlencoded] cleanly.");
    
  } catch (error) {
    console.error("Failed to modify serialization operational settings profiles within network drivers:", error);
  }
}

shiftNetworkPayloadFormat();
```