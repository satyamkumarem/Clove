# Clove.geolocation.watchPosition(cb, opts)

Establishes a continuous event-driven tracking stream that fires a callback method automatically every time the device registers a physical change in its geographic coordinates.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `cb` | `Function` | The event listener target method executed automatically whenever fresh spatial coordinates stream from native drivers. | `(position) => {}` |
| `opts` | `Object` | Optional tracking profile configuration properties managing native location provider behaviors. | `{ enableHighAccuracy: true }` |

## Return Type

* **Type:** `Promise<number>`
* **Description:** Resolves with a numeric unique `watchId` identifier token tracking this active listener lifecycle window. This ID is used to cleanly unbind the stream later.

## Code Example

```javascript
let globalTrackingToken = null;

async function startAssetTrackingPipeline() {
  const configurationProperties = {
    enableHighAccuracy: true,
    maximumAge: 3000
  };

  const handleCoordinateStreamMutation = (updatedPosition) => {
    const { latitude, longitude, accuracy } = updatedPosition.coords;
    console.log(`Asynchronous Telemetry Stream -> Lat: ${latitude} | Long: ${longitude} | Deviation Radius: ${accuracy}m`);
  };

  try {
    await Clove.ready();
    console.log("Binding continuous native event streaming pipelines targeting hardware sensors...");
    
    // Register background pipeline monitoring metrics
    globalTrackingToken = await Clove.geolocation.watchPosition(handleCoordinateStreamMutation, configurationProperties);
    console.log(`Spatial telemetry engine active. Allocated Registry Identifier: [${globalTrackingToken}]`);
    
  } catch (error) {
    console.error("Failed to map target callback sequences over platform tracking drivers:", error);
  }
}

startAssetTrackingPipeline();
```