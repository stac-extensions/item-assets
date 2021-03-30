# Item Assets Definition Extension Specification

- **Title:** Item Assets Definition
- **Identifier:** <https://stac-extensions.github.io/item-assets/v1.0.0/schema.json>
- **Field Name Prefix:** -
- **Scope:** Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @matthewhanson

This document explains the Item Assets Definition Extension to the 
[SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.

This extension serves two purposes:

1. Provide a human-readable definition of assets available in any Items 
   belonging to this Collection so that the user can determine the key(s) 
   of assets they are interested in.
2. Provide a way to programmatically determine what assets are available 
   in any member Item. Otherwise a random Item needs to be examined to 
   determine assets available, but a random Item may not be representative of the set.

- Examples:
  - [Landsat-8 Collection Example](examples/example-landsat8.json): Shows the basic usage of the extension in a STAC Collection
- [JSON Schema](json-schema/schema.json)
- [Changelog](./CHANGELOG.md)

## Collection Fields

This extension introduces a single new field, `item_assets` at the top level of a Collection.
An Asset Object defined at the Collection level is nearly the same as the 
[Asset Object in Items](https://github.com/radiantearth/stac-spec/tree/v1.0.0-rc.1/item-spec/item-spec.md#asset-object), except for two differences.
The `href` field is not required, because Collections don't point to any data by themselves, but at least two other fields must be present.

| Field Name  | Type                                       | Description |
| ----------- | ------------------------------------------ | ----------- |
| item_assets | Map<string, [Asset Object](#asset-object)> | **REQUIRED.** A dictionary of assets that can be found in member Items |

### Asset Object

An asset is an object that contains details about the datafiles that will be included in member Items.
Assets included at the Collection level do not imply that all assets are available from all Items.
However, it is recommended that the Asset Definition is a complete set of all assets that may be available from any member Items.

| Field Name  | Type      | Description |
| ----------- | --------- | ----------- |
| title       | string    | The displayed title for clients and users. |
| description | string    | A description of the Asset providing additional details, such as how it was processed or created. [CommonMark 0.29](http://commonmark.org/) syntax MAY be used for rich text representation. |
| type        | string    | [Media type](https://github.com/radiantearth/stac-spec/tree/v1.0.0-rc.1/catalog-spec/catalog-spec.md#media-types) of the asset. |
| roles       | \[string] | The [semantic roles](https://github.com/radiantearth/stac-spec/tree/v1.0.0-rc.1/item-spec/item-spec.md#asset-role-types) of the asset, similar to the use of `rel` in links. |

Other custom fields, or fields from other extensions may also be included in the Asset object.

Any property that exists for a Collection-level asset object must also exist in the corresponding assets object in 
each Item. If a collection's asset object contains properties that are not explicitly stated in the Item's asset 
object then that property does not apply to the item's asset. Item asset objects at the Collection-level can 
describe any of the properties of an asset, but those assets properties and values must also reside in the item's 
asset object. To consolidate item-level asset object properties in an API setting, consider storing the STAC Item 
objects without the larger properties internally as 'invalid' STAC items, and merge in the desired properties at 
serving time from the Collection-level.

At least two fields (e.g. `title` and `type`) are required to be provided, in order for it to adequately describe Item assets.
The two fields must not necessarily be taken from the list above and may include any custom field.

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
