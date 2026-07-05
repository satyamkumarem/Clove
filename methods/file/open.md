# Clove.file.open(path, mimeType)

Launches an external native application utility engine via Android Intent frameworks to display, execute, or manage target file types.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `path` | `string` | Target file location tracking coordinates reference pointer string. | `"exports/chart.pdf"` |
| `mimeType` | `string` | Standardized documentation content type mapping string identifier. | `"application/pdf"` |

## Return Type

* **Type:** `Promise<any>`
* **Description:** Resolves when the underlying native system intent structure handles handoffs over to processing target platform application containers cleanly. Rejects if no handling application framework maps matching configuration parameters natively.

## Code Example

```javascript
async function viewExportedReport() {
  const targetDocument = "exports/chart.pdf";
  const formatSignature = "application/pdf";

  try {
    await Clove.ready();
    
    console.log(`Requesting native system shell allocation hooks for rendering PDF framework: ${targetDocument}`);
    
    // Launch external viewer intent pipeline
    await Clove.file.open(targetDocument, formatSignature);
    console.log("Native Android intent handoff executed cleanly.");
    
  } catch (error) {
    console.error("Failed to locate native platform software utilities optimized to decode document profiles:", error);
  }
}

viewExportedReport();
```