# Solar System Extension Specification

- **Title:** Solar System
- **Identifier:** <https://stac-extensions.github.io/ssys/v1.2.0/schema.json>
- **Field Name Prefix:** ssys
- **Scope:** Item, Catalog, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/README.md#extension-maturity):** Proposal
- **Owner**: @jlaura

This document explains the fields of the STAC Solar System (SSYS) Extension to a STAC Item, Catalog, or Collection.
SSYS covers data sets that represents an individual image, mosaic, or derived raster of a planetary 
body.
Examples of SSYS data include sensors with visible, short-wave and mid-wave IR bands (e.g., the 
THEMIS instrument on Mars Odyssey), visible images (e.g. Context Camera (CTX) aboard Mars Global 
Surveyor), or derived data sets like digital elevation models (DEM/DTM).

- Examples:
- [Catalog Example (Europa Galileo SSI Image)](examples/catalog.json)
- [Collection Example (Europa Galileo SSI Image)](examples/collection.json)
- [Item Example (Europa Galileo SSI Image)](examples/item.json)
- [SSYS JSON Schema](json-schema/schema.json)

## Item Properties

| Field Name      | Type        | Description |
| --------------- | ----------- | ----------- |
| ssys:targets    | \[string\]    | Array to hold list of target bodies (e.g. Mars, Moon, Earth) conforming to the [International Virtual Observatory Alliance](https://www.ivoa.net/documents/EPNTAP/20220822/REC-EPNTAP-2.0.html#tth_sEc2.1.3) target name specification. |
| ssys:local_time  | string      | Lexicographically sortable time string (e.g., 01:115:12.343) |
| ssys:target_class | string | The identity of the type of the target as defined by the [International Virtual Observatory Alliance](https://www.ivoa.net/documents/EPNTAP/20220822/REC-EPNTAP-2.0.html#tth_sEc2.1.3) |
| ssys:north_azimuth | number | The angle between a line from the image center to the north pole and a horizontal reference line from the image center to the middle of the right edge, increasing clockwise, with the image displayed according to its declared display direction. Range: 0-360°. |
| ssys:solar_longitude | number | The angle between the body-Sun line at the time of interest and the body-Sun line at the vernal equinox, giving a measure of the season on the target body. Range: 0-360°. |
| ssys:local_true_solar_time | number | The local time on a rotating body, equal to 12 h at the subsolar point and increasing by 1 h for every 15° of east longitude away from it, for prograde rotation. Expressed in decimal hours, range 0-24. |
| ssys:emission_angle | number | The angle, measured at the intercept point, between the local surface normal and the direction of light leaving the surface toward the instrument. It is 0° for nadir viewing and 90° at the limb. Range: 0-90° for surfaces. |
| ssys:incidence_angle | number | The angle, measured at the intercept point, between the direction of incoming light and the local surface normal. It ranges from 0° when the intercept point coincides with the subsolar point to 90° when the line of sight is tangent to the target's surface. Range: 0-90° for surfaces. |
| ssys:phase_angle | number | The angle, measured at the intercept point, between the direction of incoming light from the source and the direction of outgoing light toward the instrument. Range: 0-180°. |
| ssys:sub_solar_azimuth | number | The angle between a line from the image center to the subsolar point and a horizontal reference line toward the middle of the right edge, increasing clockwise. Range: 0-360°. |
| ssys:sub_solar_latitude | number | The planetocentric latitude of the subsolar point on the target. Range: -90 to 90°. |
| ssys:sub_solar_longitude | number | The planetocentric longitude of the subsolar point on the target. Range: 0-360°. |
| ssys:sub_spacecraft_latitude | number | The planetocentric latitude of the sub-spacecraft point on the target. Range: -90 to 90°. |
| ssys:sub_spacecraft_longitude | number | The planetocentric longitude of the sub-spacecraft point on the target. Range: 0-360°. |

### Additional Field Information

#### ssys:targets

the field `ssys:targets` allows to have one or more targets listed within an array of strings. 
This can happen, for example, if several moons are in the same view. As an example, this scene 
has both of Ganymede and Jupiter in the same image as taken by the NASA mission Cassini 
[PIA02862](https://photojournal.jpl.nasa.gov/catalog/PIA02862).

The extension adopts the best practice from the 
[IVOA](https://www.ivoa.net/documents/EPNTAP/20201027/WD-epntap-2.0-20201027.html#tth_sEc2.1.3) standard. 
For almost all targets, the best practice is to use the official designation of the
 target as defined by [IAU](https://www.iau.org/public/themes/naming/)(e.g., from
 their official naming guide available via the previously linked page or
[here](https://docs.google.com/spreadsheets/d/1CEXGyancLRtHyPW7u0L_JNi0V8aDuIhv/edit#gid=1358030832)). 
This parameter is case sensitive (mixing lower/upper cases) and all values must use
the standard spelling and case; unusual characters (such as intermediate 
spaces) are allowed, except quotes (preferably changed to _ , which is the 
single-character wildcard in TAP queries). Data providers must be aware that 
services which do not use the IAU designations might not be accessible by the 
clients.

If the target is not an IAU named body, extension users can consider using one of the following:
- The Exoplanet Encyclopedia provides a nearly complete list of currently 
known extrasolar planets: [http://exoplanet.eu/](http://exoplanet.eu/index.php).
- Asteroids: Usage is to use preferably name (if it exists) or principal 
designation.
- Calibration targets: Values can relate to existing names in a given archive (e.g., 
the PSA contains values such as bias, checkout, dark, flatfield, internal source…).

#### ssys:local_time

the field `ssys:local_time` allows for API searchable non-UTC time definitions. The time should be 
encoded in a string that is lexicographically sortable. It is unlikley that this time should be 
something like the SpacecraftClockCount or another entry from the PDS metadata as most metadata 
files do not include a local (or local solar time). This field exists to support discovery in a 
time format that is meaningful to the user. Suggested formats are provided below:

| Body | Time String Format       |
| -----| -------------------------|
| Mars | `MarsYear:Sol:LocalTime` |

As a fallback one can consider using the Julian date. This has drawbacks though, as the Julian date
does not account for the day/night cycle in different bodies which is often a factor in selecting data.

#### ssys:target_class

the field `ssys:target_class` identifies the type of the target. Solar System bodies are defined without ambiguity by the couple
target_class and target_name. Values for this class are derived from the 
[International Virtual Observatory Alliance](https://www.ivoa.net/documents/EPNTAP/20220822/REC-EPNTAP-2.0.html#tth_sEc2.1.3)
target description parameter.

Accepted values are:

- asteroid
- dwarf_planet
- planet
- satellite
- comet
- exoplanet
- interplanetary_medium
- sample
- sky
- spacecraft
- spacejunk
- star
- calibration

#### ssys:north_azimuth

the field `ssys:north_azimuth` is the angle between a line from the image center to the north pole and a horizontal 
reference line from the image center to the middle of the right edge, increasing clockwise, with the image displayed 
according to its declared display direction. Range: 0-360°. Source: NASA PDS4 Data Dictionary, `geom:north_azimuth` 
(class `Object_Orientation_North_East`).

#### ssys:solar_longitude

the field `ssys:solar_longitude` is the angle between the body-Sun line at the time of interest and the body-Sun line 
at the vernal equinox, giving a measure of the season on the target body. Range: 0-360°. Source: NASA PDS4 Data 
Dictionary, `lro:start_solar_longitude` (class `LRO_Parameters`).

#### ssys:local_true_solar_time

the field `ssys:local_true_solar_time` is the local time on a rotating body, equal to 12 h at the subsolar point and 
increasing by 1 h for every 15° of east longitude away from it, for prograde rotation. It is expressed in ssys as 
decimal hours, in the range 0-24. Source: NASA PDS4 Data Dictionary, `pds:local_true_solar_time` (class 
`Time_Coordinates`), where it is encoded as a string.

#### ssys:emission_angle

the field `ssys:emission_angle` is the angle, measured at the intercept point, between the local surface normal and 
the direction of light leaving the surface toward the instrument. It is 0° for nadir viewing and 90° at the limb; 
higher values mean more oblique viewing. Range: 0-90° for surfaces. Source: NASA PDS4 Data Dictionary, 
`geom:emission_angle` (class `Derived_Geometry`).

#### ssys:incidence_angle

the field `ssys:incidence_angle` is the angle, measured at the intercept point, between the direction of incoming 
light and the local surface normal. It ranges from 0° when the intercept point coincides with the subsolar point to 
90° when the line of sight is tangent to the target's surface. Range: 0-90° for surfaces. Source: NASA PDS4 Data 
Dictionary, `geom:incidence_angle` (class `Derived_Geometry`).

#### ssys:phase_angle

the field `ssys:phase_angle` is the angle, measured at the intercept point, between the direction of incoming light 
from the source and the direction of outgoing light toward the instrument. It is small when the light source is 
behind the instrument. Range: 0-180°. Source: NASA PDS4 Data Dictionary, `geom:phase_angle` (class 
`Illumination_Specific`).

#### ssys:sub_solar_azimuth

the field `ssys:sub_solar_azimuth` is the angle between a line from the image center to the subsolar point and a 
horizontal reference line toward the middle of the right edge, increasing clockwise. Range: 0-360°. Source: NASA 
PDS4 Data Dictionary, `geom:subsolar_azimuth` (class `Surface_Geometry_Specific`).

#### ssys:sub_solar_latitude

the field `ssys:sub_solar_latitude` is the planetocentric latitude of the subsolar point on the target. Range: -90 
to 90°. Source: NASA PDS4 Data Dictionary, `geom:subsolar_latitude` (class `Surface_Geometry_Specific`).

#### ssys:sub_solar_longitude

the field `ssys:sub_solar_longitude` is the planetocentric longitude of the subsolar point on the target. Range: 
0-360°. Source: NASA PDS4 Data Dictionary, `geom:subsolar_longitude` (class `Surface_Geometry_Specific`).

#### ssys:sub_spacecraft_latitude

the field `ssys:sub_spacecraft_latitude` is the planetocentric latitude of the sub-spacecraft point on the target. 
Range: -90 to 90°. Source: NASA PDS4 Data Dictionary, `geom:subspacecraft_latitude` (class 
`Surface_Geometry_Specific`).

#### ssys:sub_spacecraft_longitude

the field `ssys:sub_spacecraft_longitude` is the planetocentric longitude of the sub-spacecraft point on the 
target. Range: 0-360°. Source: NASA PDS4 Data Dictionary, `geom:subspacecraft_longitude` (class 
`Surface_Geometry_Specific`).

## Contributing

All contributions are subject to the
[STAC Specification Code of Conduct](https://github.com/radiantearth/stac-spec/blob/master/CODE_OF_CONDUCT.md).
For contributions, please follow the
[STAC specification contributing guide](https://github.com/radiantearth/stac-spec/blob/master/CONTRIBUTING.md) Instructions
for running tests are copied here for convenience.

### Running tests

The same checks that run as checks on PR's are part of the repository and can be run locally to verify that changes are valid.
To run tests locally, you'll need `npm`, which is a standard part of any [node.js installation](https://nodejs.org/en/download/).

First you'll need to install everything with npm once. Just navigate to the root of this repository and on 
your command line run:

```bash
npm install
```

Then to check markdown formatting and test the examples against the JSON schema, you can run:

```bash
npm test
```

This will spit out the same texts that you see online, and you can then go and fix your markdown or examples.

If the tests reveal formatting problems with the examples, you can fix them with:

```bash
npm run format-examples
```
