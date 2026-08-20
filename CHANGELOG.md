# Changelog

## Unreleased

No user-facing changes since `2.2.1`.

## 2.2.1

### Changed

- Flysystem exceptions raised by the adapter now carry a reason. Where the underlying failure is a `BlobStorageException`, the reason is prefixed with the Azure error code (for example `BlobNotFound`), so callers can distinguish a missing blob from an authorization or throttling failure without unwrapping `getPrevious()`.

## 2.2.0

### Changed

- Blob listings now tolerate entries without a last-modified timestamp, as returned for uncommitted blobs.
- The package now requires `azure-oss/storage-blob:^2.2`.

## 2.1.0

### Added

- Added ETag- and lease-aware writes through the `conditions` write option.
