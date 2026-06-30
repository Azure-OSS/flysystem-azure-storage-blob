# Azure Storage Blob Flysystem Adapter

[![Latest Version on Packagist](https://img.shields.io/packagist/v/azure-oss/storage-blob-flysystem.svg)](https://packagist.org/packages/azure-oss/storage-blob-flysystem)
[![Packagist Downloads](https://img.shields.io/packagist/dt/azure-oss/storage-blob-flysystem)](https://packagist.org/packages/azure-oss/storage-blob-flysystem)

A Flysystem adapter for Azure Blob Storage built on top of `azure-oss/storage-blob`.

> [!IMPORTANT]
> This package is community-maintained and is not affiliated with, endorsed by, or supported by Microsoft.

## Install

```shell
composer require azure-oss/storage-blob-flysystem
```

## Quickstart

```php
<?php

use AzureOss\Storage\Blob\BlobServiceClient;
use AzureOss\Storage\BlobFlysystem\AzureBlobStorageAdapter;
use League\Flysystem\Filesystem;

$service = BlobServiceClient::fromConnectionString(
    getenv('AZURE_STORAGE_CONNECTION_STRING')
);

$container = $service->getContainerClient(
    getenv('AZURE_STORAGE_CONTAINER')
);

$adapter = new AzureBlobStorageAdapter($container);
$filesystem = new Filesystem($adapter);

// Write
$filesystem->write('docs/hello.txt', 'Hello Azure Blob + Flysystem');

// Read
$contents = $filesystem->read('docs/hello.txt');

// Stream upload
$stream = fopen('/path/to/big-file.zip', 'r');
$filesystem->writeStream('archives/big-file.zip', $stream);
fclose($stream);

// List recursively
foreach ($filesystem->listContents('docs', true) as $item) {
    echo $item->path().PHP_EOL;
}

// Delete
$filesystem->delete('docs/hello.txt');
```

## Documentation

You can read the documentation [here](https://php-oss-for-azure.github.io/category/storage-blob-flysystem).

## Migration Guide

Migrating from `league/flysystem-azure-blob-storage`?
[Migrate from league/flysystem-azure-blob-storage](https://php-oss-for-azure.github.io/storage-blob-flysystem/migrate-from-league-flysystem-azure-blob-storage).

## Related packages

- **[azure-oss/storage](https://packagist.org/packages/azure-oss/storage)** — Meta package for the Storage SDKs
- **[azure-oss/storage-common](https://packagist.org/packages/azure-oss/storage-common)** — Shared authentication, HTTP, and SAS primitives
- **[azure-oss/storage-blob](https://packagist.org/packages/azure-oss/storage-blob)** — Blob Storage SDK
- **[azure-oss/storage-blob-flysystem-bundle](https://packagist.org/packages/azure-oss/storage-blob-flysystem-bundle)** — Symfony Flysystem bundle
- **[azure-oss/storage-blob-laravel](https://packagist.org/packages/azure-oss/storage-blob-laravel)** — Laravel filesystem driver
- **[azure-oss/storage-queue](https://packagist.org/packages/azure-oss/storage-queue)** — Queue Storage SDK
- **[azure-oss/storage-queue-laravel](https://packagist.org/packages/azure-oss/storage-queue-laravel)** — Laravel queue connector
- **[azure-oss/storage-file-share](https://packagist.org/packages/azure-oss/storage-file-share)** — File Share SDK
- **[azure-oss/identity](https://packagist.org/packages/azure-oss/identity)** — Microsoft Entra ID token authentication

## Maintenance

This package is part of the community-maintained PHP OSS for Azure project. It is an independent project and is not affiliated with or endorsed by Microsoft.

## License

This project is released under the MIT License. See [LICENSE](./LICENSE) for details.
