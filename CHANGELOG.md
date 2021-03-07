# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

- Added clarification about how collection-level asset object properties do 
  not remove the need for item-level asset object properties in the `item-assets` extension ([#880](https://github.com/radiantearth/stac-spec/pull/880))

### Added

### Changed

### Deprecated

### Removed

### Fixed

[Unreleased]: <https://github.com/stac-extensions/template/compare/v1.0.0...HEAD>

## [v1.0.0-beta.1] - 2020-05-29

### Changed

- `asset` extension renamed to `item-assets` and renamed `assets` field in Collections to `item_assets`
- `item-assets` extension only requires any two fields to be available, not the two specific fields `title` and `type`
