# Solar System Extension Specification

- **Title:** Solar System
- **Identifier:** <https://stac-extensions.github.io/ssys/v1.0.0/schema.json>
- **Field Name Prefix:** ssys
- **Scope:** Item
- **Extension [Maturity Classification]:** Proposal
- **Owner**: @thareUSGS

This document explains the fields of the STAC Solar System (SSYS) Extension to a STAC Item. SSYS covers data sets that represents an individual image, mosaic, or derived raster of a planetary body. Examples of SSYS data include sensors with visible, short-wave and mid-wave IR bands (e.g., the THEMIS instrument on
Mars Odyssey), visable images (e.g. Context Camera (CTX) aboard Mars Global Surveyor), or derived data sets like digital elevation models (DEM/DTM).

- Examples:
- [Item Example (Europa Galelio SSI)](examples/mars_THEMIS_IR-sample.json)
- [JSON Schema](json-schema/schema.json)
- [Changelog](./CHANGELOG.md)

## Item Properties and Collection Fields

| Field Name           | Type                      | Description |
| -------------------- | ------------------------- | ----------- |
| ssys:targets         | string                    | The name of the target body (e.g. Mars, Moon, Earth) |

### Additional Field Information

#### ssys:targets

the field `sys:targets` allows to have one or more targets listed. This can happen for example if several moons are in the same view. For example this view of Ganymede and Jupiter in the same image as taken by the NASA mission Cassini [PIA02862](https://photojournal.jpl.nasa.gov/catalog/PIA02862).

## Contributing

All contributions are subject to the
[STAC Specification Code of Conduct](https://github.com/radiantearth/stac-spec/blob/master/CODE_OF_CONDUCT.md).
For contributions, please follow the
[STAC specification contributing guide](https://github.com/radiantearth/stac-spec/blob/master/CONTRIBUTING.md) Instructions
for running tests are copied here for convenience.
