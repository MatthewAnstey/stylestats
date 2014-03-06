![StyleStats](http://i.imgur.com/81kKnxH.png)

Stylestats is a efficient Node.js library for keeping stylesheet statistics.

[![Build Status](https://secure.travis-ci.org/t32k/stylestats.png?branch=master)](http://travis-ci.org/t32k/stylestats)
[![NPM version](https://badge.fury.io/js/stylestats.png)](http://badge.fury.io/js/stylestats)
[![Dependency Status](https://david-dm.org/t32k/stylestats.png)](https://david-dm.org/t32k/stylestats)
[![devDependency Status](https://david-dm.org/t32k/stylestats/dev-status.png)](https://david-dm.org/t32k/stylestats#info=devDependencies)


## Installation

```
$ npm install stylestats
```

## Usage


```sh
$ stylestats path/to/stylesheet.css
StyleStats!
┌───────────────────────────┬───────────────┐
│ Size                      │ 498.0B        │
├───────────────────────────┼───────────────┤
│ Rules                     │ 8             │
├───────────────────────────┼───────────────┤
│ Selectors                 │ 11            │
├───────────────────────────┼───────────────┤
│ Simplicity                │ 72.73%        │
├───────────────────────────┼───────────────┤
│ Lowest Cohesion           │ 6             │
├───────────────────────────┼───────────────┤
│ Lowest Cohesion Selecotor │ hr            │
├───────────────────────────┼───────────────┤
│ Total Unique Font Sizes   │ 5             │
├───────────────────────────┼───────────────┤
│ Unique Font Size          │ 10px          │
│                           │ 12px          │
│                           │ 14px          │
│                           │ 16px          │
│                           │ 18px          │
├───────────────────────────┼───────────────┤
│ Total Unique Colors       │ 2             │
├───────────────────────────┼───────────────┤
│ Unique Color              │ #333          │
│                           │ #CCC          │
├───────────────────────────┼───────────────┤
│ Id Selectors              │ 1             │
├───────────────────────────┼───────────────┤
│ Important Keywords        │ 1             │
├───────────────────────────┼───────────────┤
│ Media Queries             │ 1             │
├───────────────────────────┼───────────────┤
│ Properties Count          │ font-size: 5  │
│                           │ margin: 4     │
│                           │ padding: 3    │
│                           │ color: 2      │
│                           │ display: 1    │
│                           │ height: 1     │
│                           │ border: 1     │
│                           │ border-top: 1 │
└───────────────────────────┴───────────────┘
```

## Metrics

#### Simplicity

The __Simplicity__ is measured as __Rules__ divided by __Selectors__.

#### Lowest Cohesion

The __Lowest Cohesion__ metric is the count of the declarations of the most declared selector.

#### Properties Count

The __Properties Count__ is ranking of declared properties. Default option is display the top `10`.


## Configuration

You must configure Stylestats before use.

CLI:

```shell
$ stylestats -c path/to/.stylestatsrc
```

API:

```js
var StyleStats = require('stylestats');
var stats = new StyleStats('path/to/stylesheet.css', 'path/to/.stylestatsrc');
```

Default configuration is [here](lib/defaultOptions.js).

Here is configuration's JSON example of enabling display gzipped size:

```
{
  "gzippedSize": true
}
```

## CLI Reference


```shell
$ stylestats -h

  Usage: stylestats [options] <file ...>

  Options:

    -h, --help                output usage information
    -V, --version             output the version number
    -c, --config [path]       Path and name of the incoming JSON file.
    -e, --extension [format]  Specify the format to convert. <json|csv>
    -s, --simple              Display compact log.
```

```shell
$ stylestats path/to/stylesheet.css -s -c path/to/.stylestatsrc
StyleStats!
┌───────────────────────────┬───────────────┐
│ Rules                     │ 8             │
│ Selectors                 │ 11            │
│ Lowest Cohesion           │ 6             │
│ Total Unique Font Sizes   │ 5             │
│ Total Unique Colors       │ 2             │
│ Id Selectors              │ 1             │
│ Important Keywords        │ 1             │
│ Media Queries             │ 1             │
└───────────────────────────┴───────────────┘
```

+ [Plot Stylestats data with Jenkins](https://github.com/t32k/stylestats/wiki/Plot-with-Jenkins)

## API Reference

```javascript
var StyleStats = require('stylestats');
var stats = new StyleStats('path/to/stylesheet.css');

console.log(JSON.stringify(stats.parse(), null, 2));
```

### Example

[This stylesheet](test/fixture/test.css)'s stats tree:

```json
{
  "size": 498,
  "rules": 8,
  "selectors": 11,
  "simplicity": 0.7272727272727273,
  "lowestCohesion": 6,
  "lowestCohesionSelecotor": [ "hr" ],
  "totalUniqueFontSizes": 5,
  "uniqueFontSize": [ "10px","12px","14px","16px","18px" ],
  "totalUniqueColors": 2,
  "uniqueColor": [ "#333", "#CCC" ],
  "idSelectors": 1,
  "importantKeywords": 1,
  "mediaQueries": 1,
  "propertiesCount": [
    [ "font-size", 5], [ "margin", 4 ], [ "padding", 3 ], [ "color", 2 ], [ "display", 1 ], [ "height", 1 ], [ "border", 1 ], [ "border-top", 1 ]
  ]
}
```



## Online Tool

_(Coming soon)_


# License

 Code is released under [the MIT license](LICENSE).
