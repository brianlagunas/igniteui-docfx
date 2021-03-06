---
title: Map | Data Visualization Tools | Ignite UI for Angular | Contour Line Series | Infragistics
_description: The Map allows you to display data that contains geographic locations from view models or geo-spatial data loaded from shape files on geographic imagery maps.View the demo, dependencies, usage and toolbar for more information. 
_keywords: map, Ignite UI for Angular, infragistics
---

## Contour Line Series

In the Ignite UI for Angular map component, the `GeographicContourLineSeries` is a visual map element that draws colored contour lines, in a geographic context, based on a triangulation of longitude and latitude data with a numeric value assigned to each point.
This type of geographic series is useful for rendering scattered data defined by geographic locations such as weather temperature, atmospheric pressure, precipitation, population distribution, topographic data, etc. The `GeographicContourLineSeries` works a lot like the `GeographicScatterAreaSeries` except that it represents data as contour lines, colored using a fill scale and the geographic scatter area series, represents data as a surface interpolated using a color scale.

### Demo

<div class="sample-container" style="height: 500px">
    <iframe id="map-geographic-contour-line-series-iframe" src='{environment:demosBaseUrl}/maps/map-geographic-contour-line-series' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn"   data-iframe-id="map-geographic-contour-line-series-iframe" data-demos-base-url="{environment:demosBaseUrl}">View on StackBlitz
    </button>
</div>

<div class="divider--half"></div>

The following table summarized data structures required for each type of geographic series :

### Data Requirements

Similar to other types of geographic series in the map component, the `GeographicContourLineSeries` has the `ItemsSource` property for data binding. This property can be bound to an object that implements an IEnumerable interface.
In addition, each item in the items source must have three data columns, two that store geographic location (longitude and latitude coordinates) and one data column that stores a value associated with the geographic location. These data column, are identified by `LongitudeMemberPath`, `LatitudeMemberPath`, and `ValueMemberPath` properties of the geographic series.
The `GeographicContourLineSeries` automatically performs built-in data triangulation on items in the ItemsSource if no triangulation is set to the `TrianglesSource` property. However, computing triangulation can be a very time-consuming process, so the runtime performance will be better when specifying a `TriangulationSource` for this property, especially when a large number of data items are present.

### Data Binding

The following table summarizes properties of `GeographicContourLineSeries` used for data binding.

| Property Name               | Property Type | Description                                                                                                                                                                                                                                                      |
| --------------------------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ItemsSource`               | IEnumerable   | Gets or sets the source of items to perform triangulation on if the TrianglesSource property provides no triangulation data.                                                                                                                                     |
| `TrianglesSource`           | IEnumerable   | Gets or sets the source of triangulation data. Setting Triangles of the TriangulationSource object to this property improves both runtime performance and geographic series rendering.                                                                           |
| `LongitudeMemberPath`       | string        | The name of the property containing the Longitude for each item in the ItemsSource.                                                                                                                                                                              |
| `LatitudeMemberPath`        | string        | The name of the property containing the Latitude for each item in the ItemsSource.                                                                                                                                                                               |
| `ValueMemberPath`           | string        | The name of the property on each data item containing a numeric value which can be converted to a brush by a fill scale set to the FillScale property.                                                                                                           |
| `TriangleVertexMemberPath1` | string        | The name of the property of the TrianglesSource items which, for each triangle, contains the index of the first vertex point in the ItemsSource. It is not mandatory to set this property. It is taken by default unless custom triangulation logic is provided. |
| `TriangleVertexMemberPath2` | string        | The name of the property of the TrianglesSource items which, for each triangle, contains the index of the first vertex point in the ItemsSource. It is not mandatory to set this property. It is taken by default unless custom triangulation logic is provided. |
| `TriangleVertexMemberPath3` | string        | The name of the property of the TrianglesSource items which, for each triangle, contains the index of the first vertex point in the ItemsSource. It is not mandatory to set this property. It is taken by default unless custom triangulation logic is provided. |

### Contour Fill Scale

Use the `FillScale` property of the `GeographicContourLineSeries` to resolve fill brushes of the contour lines of the geographic series.
The provided \`ValueBrushScale class should satisfy most of your coloring needs, but the application for custom coloring logic can inherit the ValueBrushScale class.
The following table list properties of the CustomPaletteColorScale affecting the surface coloring of the GeographicContourLineSeries.

| Property Name  | Property Type   | Description                                                                                      |
| -------------- | --------------- | ------------------------------------------------------------------------------------------------ |
| `Brushes`      | BrushCollection | Gets or sets the collection of brushes for filling contours of the `GeographicContourLineSeries` |
| `MaximumValue` | double          | The highest value to assign a brush in a fill scale.                                             |
| `MinimumValue` | double          | The lowest value to assign a brush in a fill scale.                                              |

### Contour Value Resolver\`

The `GeographicContourLineSeries` renders using exactly 10 contour lines at even intervals between the minimum and maximum values of the items mapped to the `ValueMemberPath` property. If you desire more or fewer contours, you can assign the LinearContourValueResolver with a number of contours to the `ValueResolver` property of the `GeographicContourLineSeries`.

The following code shows how to configure the number of contour lines in the `GeographicContourLineSeries`

To determine the position of contour lines in an application, implement the Custom value resolvers. This is accomplished by inheriting from the `ContourValueResolver` and overriding the `GetContourValues` method.

The following code shows implementation of a custom contour value resolver that specifies contour lines at predefined positions.

### Code Snippet

The following code shows how to bind the `GeographicContourLineSeries` to triangulation data representing precipitation over the United States.
