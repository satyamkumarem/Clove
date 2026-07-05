# Clove.geolocation.getCurrentPosition(opts)

Queries the device's native positioning hardware layer (GPS, Wi-Fi, and Cellular triangulation) to resolve the exact snapshot geographical coordinates of the handset.

## Parameters

| Parameter | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `opts` | `Object` | Optional tracking performance configuration criteria passed downstream to the native location framework. | `{ enableHighAccuracy: true, timeout: 5000 }` |

### Key `opts` Configuration Matrix
| Property | Type | Description | Default / Options |
| :--- | :--- | :--- | :--- |
| `enableHighAccuracy` | `boolean` | Demands high-precision data coordinates (usually fires up physical power-heavy GPS hardware). | `true` or `false` |
| `timeout` | `number` | The maximum lifespan allowance window in milliseconds allowed to resolve location before returning an error. | `Infinity` (Default) |
| `maximumAge` | `number` | Instructs the driver to accept a cached coordinate snapshot if its age is within the specified millisecond threshold. | `0` (Force raw update) |

## Return Type

* **Type:** `Promise<Object>`
* **Description:** Resolves with a standard Geolocation position object containing standard geospatial data metrics.

### Success Payload Payload Properties:
| Property | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `coords.latitude` | `number` | Geographic latitude coordinates measured in precise decimal degrees. | `25.5941` |
| `coords.longitude` | `number` | Geographic longitude coordinates measured in precise decimal degrees. | `85.1376` |
| `coords.accuracy` | `number` | The level of horizontal coordinate calculation uncertainty reported in meters. | `12.5` |
| `timestamp` | `number` | Epoch time integer indicating precisely when the spatial snapshot data was bound. | `1719655564000` |

## Code Example

```javascript
async function captureSpatialCoordinates() {
  const positioningOptions = {
    enableHighAccuracy: true,
    timeout: 10000,
    maximumAge: 0
  };

  try {
    await Clove.ready();
    console.log("Polling onboard physical GPS and network triangulation matrices...");
    
    const position = await Clove.geolocation.getCurrentPosition(positioningOptions);
    
    console.log("Location successfully locked:");
    console.log(`Latitude coordinate tracking:  ${position.coords.latitude}`);
    console.log(`Longitude coordinate tracking: ${position.coords.longitude}`);
    console.log(`Uncertainty bounds verification: Within ${position.coords.accuracy} meters.`);
    
  } catch (error) {
    console.error("Spatial coordinate resolution step halted due to timeout or rejected permissions:", error);
  }
}

captureSpatialCoordinates();
```