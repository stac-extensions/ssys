# Solar System Extension Specification

- **Title:** Solar System
- **Identifier:** <https://raw.githubusercontent.com/thareUSGS/ssys/main/json-schema/schema.json>
- **Field Name Prefix:** ssys
- **Scope:** Item, Catalog, Collection
- **Extension [Maturity Classification]:** Proposal
- **Owner**: @thareUSGS

This document explains the fields of the STAC Solar System (SSYS) Extension to a STAC Item, Catalog, or Collection. 
SSYS covers data sets that represents an individual image, mosaic, or derived raster of a planetary body. Examples 
of SSYS data include sensors with visible, short-wave and mid-wave IR bands (e.g., the THEMIS instrument on Mars 
Odyssey), visible images (e.g. Context Camera (CTX) aboard Mars Global Surveyor), or derived data sets like digital 
elevation models (DEM/DTM).

- Examples:
- [Catalog Example (Europa Galileo SSI Image)](examples/catalog.json)
- [Collection Example (Europa Galileo SSI Image)](examples/collection.json)
- [Item Example (Europa Galileo SSI Image)](examples/item.json)
- [SSYS JSON Schema](json-schema/schema.json)
- [Changelog](./CHANGELOG.md)

## Item Properties

| Field Name      | Type        | Description |
| --------------- | ----------- | ----------- |
| ssys:targets    | [string]    | Array to hold list of target bodies (e.g. Mars, Moon, Earth) |
| ssys:local_solar_time | number | The time of an observation relative to the sensor and sun position. |
| ssys:start_Ls | The start time of year for a Mars observation. |
| ssys:stop_Ls | The start time of year for a Mars observation. |
| ssys:start_mars_year | The start Mars year of an observation. |
| ssys:stop_mars_year | The stop Mars year of an observation. |

### Additional Field Information

#### ssys:targets

the field `ssys:targets` allows to have one or more targets listed within an array of strings. This can 
happen, for example, if several moons are in the same view. As an example, this scene has both of Ganymede
and Jupiter in the same image as taken by the NASA mission Cassini [PIA02862](https://photojournal.jpl.nasa.gov/catalog/PIA02862).

#### ssys:\*_local_solar_time, ssys:\*_Ls, ssys:\*_mars_year
the fields `ssys:local_solar_time`, `ssys:Ls`, and `ssys:mars_year` allow for tracking of temporal information not tied to Earth standards. More information about the Martian Calendar is available [here](https://www.planetary.org/articles/mars-calendar).

## Contributing

All contributions are subject to the
[STAC Specification Code of Conduct](https://github.com/radiantearth/stac-spec/blob/master/CODE_OF_CONDUCT.md).
For contributions, please follow the
[STAC specification contributing guide](https://github.com/radiantearth/stac-spec/blob/master/CONTRIBUTING.md) Instructions
for running tests are copied here for convenience.
