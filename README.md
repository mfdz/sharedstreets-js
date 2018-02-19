# SharedStreets (Node.js & Javascript)

[![npm version](https://badge.fury.io/js/sharedstreets.svg)](https://badge.fury.io/js/sharedstreets)
[![Build Status](https://travis-ci.org/sharedstreets/sharedstreets-js.svg?branch=master)](https://travis-ci.org/sharedstreets/sharedstreets-js)

Node.js & Javascript implementation of [SharedStreets Reference System](https://github.com/sharedstreets/sharedstreets-ref-system).

## Install

**In Node.js**

```bash
$ yarn add sharedstreets
```

**CommonJS**

```js
const sharedstreets = require('sharedstreets');
```

**Typescript**

```js
import * as sharedstreets from 'sharedstreets';
```

## In Browser

For a full list of web examples, check out [SharedStreets examples](https://github.com/sharedstreets/sharedstreets-examples).

## How to build

```bash
$ git clone git@github.com:sharedstreets/sharedstreets-js.git
$ cd sharedstreets-js
$ yarn
$ yarn test
```

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### Table of Contents

-   [geometryId](#geometryid)
-   [geometry](#geometry)
-   [intersectionId](#intersectionid)
-   [intersection](#intersection)
-   [referenceId](#referenceid)
-   [reference](#reference)
-   [forwardReference](#forwardreference)
-   [backReference](#backreference)
-   [metadata](#metadata)
-   [outboundBearing](#outboundbearing)
-   [inboundBearing](#inboundbearing)
-   [distanceToNextRef](#distancetonextref)
-   [lonlatsToCoords](#lonlatstocoords)
-   [coordsToLonlats](#coordstolonlats)
-   [generateHash](#generatehash)
-   [getRoadClassString](#getroadclassstring)
-   [getRoadClassNumber](#getroadclassnumber)
-   [getFormOfWayString](#getformofwaystring)
-   [getFormOfWay](#getformofway)
-   [getStartCoord](#getstartcoord)
-   [getEndCoord](#getendcoord)
-   [getFormOfWayNumber](#getformofwaynumber)
-   [getCoords](#getcoords)
-   [round](#round)

### geometryId

Geometry Id

**Parameters**

-   `line` **(Feature&lt;LineString> | [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)>>)** Line Geometry as a GeoJSON LineString or an Array of Positions Array&lt;&lt;longitude, latitude>>.

**Examples**

```javascript
const id = sharedstreets.geometryId([[110, 45], [115, 50], [120, 55]]);
id // => "ce9c0ec1472c0a8bab3190ab075e9b21"
```

Returns **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** SharedStreets Geometry Id

### geometry

geometry

**Parameters**

-   `line` **(Feature&lt;LineString> | [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)>>)** GeoJSON LineString Feature
-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Optional parameters (optional, default `{}`)
    -   `options.formOfWay` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Property field that contains FormOfWay value (number/string).
    -   `options.roadClass` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Property field that contains RoadClass value (number/string).

**Examples**

```javascript
const line = [[110, 45], [115, 50], [120, 55]];
const geom = sharedstreets.geometry(line);
geom.id; // => "ce9c0ec1472c0a8bab3190ab075e9b21"
geom.lonlats; // => [ 110, 45, 115, 50, 120, 55 ]
```

Returns **SharedStreetsGeometry** SharedStreets Geometry

### intersectionId

Intersection Id

**Parameters**

-   `pt` **(Feature&lt;Point> | [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)>)** Point location reference as a GeoJSON Point or an Array of numbers &lt;longitude, latitude>.

**Examples**

```javascript
const id = sharedstreets.intersectionId([110, 45]);
id // => "71f34691f182a467137b3d37265cb3b6"
```

Returns **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** SharedStreets Intersection Id

### intersection

Intersection

**Parameters**

-   `pt` **(Feature&lt;Point> | [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)>)** Point location reference as a GeoJSON Point or an Array of numbers &lt;longitude, latitude>.
-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Optional parameters (optional, default `{}`)
    -   `options.nodeId` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Define NodeId for Intersection

**Examples**

```javascript
const intersection = sharedstreets.intersection([110, 45]);
intersection.id // => "71f34691f182a467137b3d37265cb3b6"
```

Returns **SharedStreetsIntersection** SharedStreets Intersection

### referenceId

Reference Id

**Parameters**

-   `locationReferences` **[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;LocationReference>** An Array of Location References.
-   `formOfWay` **FormOfWay** Form Of Way (optional, default `0`)

**Examples**

```javascript
const locationReferences = [
  sharedstreets.locationReference([-74.0048213, 40.7416415], {outboundBearing: 208, distanceToNextRef: 9279}),
  sharedstreets.locationReference([-74.0051265, 40.7408505], {inboundBearing: 188})
];
const formOfWay = 2; // => "MultipleCarriageway"

const id = sharedstreets.referenceId(locationReferences, formOfWay);
id // => "ef209661aeebadfb4e0a2cb93153493f"
```

Returns **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** SharedStreets Reference Id

### reference

Reference

**Parameters**

-   `geom` **SharedStreetsGeometry** SharedStreets Geometry
-   `locationReferences` **[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;LocationReference>** An Array of Location References.
-   `formOfWay` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** Form Of Way (default Undefined) (optional, default `0`)

**Examples**

```javascript
const line = [[110, 45], [115, 50], [120, 55]];
const geom = sharedstreets.geometry(line);
const locationReferences = [
  sharedstreets.locationReference([-74.0048213, 40.7416415], {outboundBearing: 208, distanceToNextRef: 9279}),
  sharedstreets.locationReference([-74.0051265, 40.7408505], {inboundBearing: 188}),
];
const formOfWay = 2; // => "MultipleCarriageway"
const ref = sharedstreets.reference(geom, locationReferences, formOfWay);
ref.id // => "ef209661aeebadfb4e0a2cb93153493f"
```

Returns **SharedStreetsReference** SharedStreets Reference

### forwardReference

Forward Reference

**Parameters**

-   `line` **(Feature&lt;LineString> | [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)>>)** GeoJSON LineString Feature or an Array of Positions
-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Optional parameters (optional, default `{}`)
    -   `options.formOfWay` **([number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number) \| [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String))** Form of Way (default "Undefined") (optional, default `0`)

**Examples**

```javascript
const line = [[110, 45], [115, 50], [120, 55]];
const ref = sharedstreets.forwardReference(line);
ref.id // => "3f652e4585aa7d7df3c1fbe4f55cea0a"
```

Returns **SharedStreetsReference** Forward SharedStreets Reference

### backReference

Back Reference

**Parameters**

-   `line` **(Feature&lt;LineString> | [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)>>)** GeoJSON LineString Feature or an Array of Positions
-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Optional parameters (optional, default `{}`)
    -   `options.formOfWay` **([number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number) \| [string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String))** Form of Way (default "Undefined") (optional, default `0`)

**Examples**

```javascript
const line = [[110, 45], [115, 50], [120, 55]];
const ref = sharedstreets.backReference(line);
ref.id // => "a18b2674e41cad630f5693154837baf4"
```

Returns **SharedStreetsReference** Back SharedStreets Reference

### metadata

Metadata

**Parameters**

-   `geom` **SharedStreetsGeometry** SharedStreets Geometry
-   `osmMetadata` **OSMMetadata** OSM Metadata (optional, default `{}`)
-   `gisMetadata` **[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;GISMetadata>** GIS Metadata (optional, default `[]`)

**Examples**

```javascript
const line = [[110, 45], [115, 50], [120, 55]];
const geom = sharedstreets.geometry(line);
const metadata = sharedstreets.metadata(geom)
```

Returns **SharedStreetsMetadata** SharedStreets Metadata

### outboundBearing

Calculates outbound bearing from a LineString

**Parameters**

-   `line` **(Feature&lt;LineString> | [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)>>)** GeoJSON LineString or an Array of Positions

**Examples**

```javascript
const line = [[110, 45], [115, 50], [120, 55]];
const outboundBearing = sharedstreets.outboundBearing(line);
outboundBearing; // => 208
```

Returns **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** Outbound Bearing

### inboundBearing

Calculates inbound bearing from a LineString

**Parameters**

-   `line` **(Feature&lt;LineString> | [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)>>)** GeoJSON LineString or an Array of Positions

**Examples**

```javascript
const line = [[110, 45], [115, 50], [120, 55]];
const inboundBearing = sharedstreets.inboundBearing(line);
inboundBearing; // => 188
```

Returns **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** Inbound Bearing

### distanceToNextRef

Calculates inbound bearing from a LineString

**Parameters**

-   `start` **Coord** GeoJSON Point or an Array of numbers [Longitude/Latitude]
-   `end` **Coord** GeoJSON Point or an Array of numbers [Longitude/Latitude]

**Examples**

```javascript
const start = [110, 45];
const end = [120, 55];
const distanceToNextRef = sharedstreets.distanceToNextRef(start, end);
distanceToNextRef; // => 9279
```

Returns **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** Distance to next Ref in centimeters

### lonlatsToCoords

Converts lonlats to GeoJSON LineString Coords

**Parameters**

-   `lonlats` **[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)>** Single Array of paired longitudes & latitude

**Examples**

```javascript
const coords = lonlatsToCoords([110, 45, 120, 55]);
coords // => [[110, 45], [120, 55]]
```

Returns **[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)>>** GeoJSON LineString coordinates

### coordsToLonlats

Converts GeoJSON LineString Coords to lonlats

**Parameters**

-   `coords` **[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number), [number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)>>** GeoJSON LineString coordinates

**Examples**

```javascript
const lonlats = coordsToLonlats([[110, 45], [120, 55]]);
lonlats // => [110, 45, 120, 55]
```

Returns **[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)>** lonlats Single Array of paired longitudes & latitude

### generateHash

Generates Base16 Hash

**Parameters**

-   `message` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Message to hash

**Examples**

```javascript
const message = "Intersection -74.00482177734375 40.741641998291016";
const hash = sharedstreets.generateHash(message);
hash // => "69f13f881649cb21ee3b359730790bb9"
```

Returns **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** SharedStreets Reference ID

### getRoadClassString

Get RoadClass from a Number to a String

**Parameters**

-   `value` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** Number value [between 0-8]

**Examples**

```javascript
sharedstreets.getRoadClassString(0); // => "Motorway"
sharedstreets.getRoadClassString(5); // => "Residential"
```

Returns **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Road Class

### getRoadClassNumber

Get RoadClass from a String to a Number

**Parameters**

-   `value` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** String value ["Motorway", "Trunk", "Primary", etc...]

**Examples**

```javascript
sharedstreets.getRoadClassNumber("Motorway"); // => 0
sharedstreets.getRoadClassNumber("Residential"); // => 5
```

Returns **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Road Class

### getFormOfWayString

Get FormOfWay from a GeoJSON LineString and/or Optional parameters

**Parameters**

-   `value` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** Number value [between 0-7]

**Examples**

```javascript
sharedstreets.getFormOfWayString(0); // => "Undefined"
sharedstreets.getFormOfWayString(5); // => "TrafficSquare"
```

Returns **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Form of Way

### getFormOfWay

Get FormOfWay from a GeoJSON LineString

**Parameters**

-   `line` **(Feature&lt;LineString> | [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)>>)** GeoJSON LineString Feature or an Array of Positions
-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Optional parameters (optional, default `{}`)
    -   `options.formOfWay` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** Form of Way (optional, default `0`)

**Examples**

```javascript
const lineA = turf.lineString([[110, 45], [115, 50], [120, 55]], {formOfWay: 3});
const lineB = turf.lineString([[110, 45], [115, 50], [120, 55]]);
const lineC = turf.lineString([[110, 45], [115, 50], [120, 55]], {formOfWay: "Motorway"});

sharedstreets.getFormOfWay(lineA); // => 3
sharedstreets.getFormOfWay(lineB); // => 0
sharedstreets.getFormOfWay(lineC); // => 1
```

### getStartCoord

Get Start Coordinate from a GeoJSON LineString

**Parameters**

-   `line` **(Feature&lt;LineString> | [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;Position>)** GeoJSON LineString or an Array of Positiosn

**Examples**

```javascript
const line = turf.lineString([[110, 45], [115, 50], [120, 55]]);
const start = sharedstreets.getStartCoord(line);
start // => [110, 45]
```

Returns **Position** Start Coordinate

### getEndCoord

Get Start Coordinate from a GeoJSON LineString

**Parameters**

-   `line` **(Feature&lt;LineString> | [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;Position>)** GeoJSON LineString or an Array of Positiosn

**Examples**

```javascript
const line = turf.lineString([[110, 45], [115, 50], [120, 55]]);
const end = sharedstreets.getEndCoord(line);
end // => [120, 55]
```

Returns **Position** Start Coordinate

### getFormOfWayNumber

Get FormOfWay from a String to a Number

**Parameters**

-   `value` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** String value [ex: "Undefined", "Motorway", etc...]

**Examples**

```javascript
sharedstreets.getFormOfWayNumber("Undefined"); // => 0
sharedstreets.getFormOfWayNumber("TrafficSquare"); // => 5
```

Returns **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** Form of Way

### getCoords

getCoords

**Parameters**

-   `line` **(Feature&lt;LineString> | [Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)>>)** GeoJSON LineString or an Array of positions

**Examples**

```javascript
const line = turf.lineString([[110, 45], [115, 50], [120, 55]]);
const coords = sharedstreets.getCoords(line);
coords; // => [[110, 45], [115, 50], [120, 55]]
```

Returns **[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)>>** Array of positions

### round

Round Number to 6 decimals

**Parameters**

-   `num` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** Number to round
-   `decimalPlaces` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)** Decimal Places (optional, default `6`)

**Examples**

```javascript
sharedstreets.round(10.123456789) // => 10.123457
```

Returns **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Big Number fixed string
