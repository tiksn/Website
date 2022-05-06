---
title: SecretManagement.Keybase
summary: PowerShell SecretManagement extension for Keybase
tags:
  - powershell
date: '2020-05-10T00:00:00Z'
weight: 5
# Optional external URL for project (replaces project detail page).
# external_link: 'https://github.com/tiksn/SecretManagement.Keybase'

# image:
#   caption: Photo by rawpixel on Unsplash
#   focal_point: Smart

links:
  - icon: github
    icon_pack: fab
    name: Source Code
    url: https://github.com/tiksn/SecretManagement.Keybase
  - icon: download
    icon_pack: fas
    name: PowerShell Gallery
    url: https://www.powershellgallery.com/packages/SecretManagement.Keybase/
url_code: ''
url_pdf: ''
url_slides: ''
url_video: ''

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides:
---


# Keybase Secret Management Extension for PowerShell

![PowerShell Gallery](https://img.shields.io/powershellgallery/dt/SecretManagement.Keybase)

A PowerShell Secret Management extension that uses [Keybase](https://keybase.io/) KV store as a secure vault backend. This module extends the [PowerShell Secrets Management](https://www.powershellgallery.com/packages/Microsoft.PowerShell.SecretManagement/) framework to enable storing and retrieving secrets using Keybase's encrypted key-value store.

## Features

- **Full Secret Management Integration**: Implements all required Secret Management cmdlets (`Set-Secret`, `Get-Secret`, `Remove-Secret`, `Get-SecretInfo`, `Test-SecretVault`)
- **Multiple Secret Types**: Supports ByteArray, String, SecureString, PSCredential, and Hashtable
- **Keybase KV Store**: Leverages Keybase's encrypted, distributed key-value store for secure secret storage
- **Team Support**: Optional team-based vaults for collaborative secret management
- **Wildcard Filtering**: Query secrets using wildcard patterns in `Get-SecretInfo`
- **Type Preservation**: Automatically serializes and deserializes secrets while maintaining their original types
- **Secure Encryption**: SecureString and PSCredential secrets are encrypted with randomly generated keys before storage

## Prerequisites

- **PowerShell 7.0.0 or later** (PowerShell Core)
- **Microsoft.PowerShell.SecretManagement** module
- **Keybase CLI** installed and configured with a logged-in account
  - Download from [keybase.io](https://keybase.io/download)
  - Ensure `keybase` command is available in your PATH

## Installation

Install from PowerShell Gallery:

```PowerShell
Install-Module -Name SecretManagement.Keybase
```

Check out the package in [PS Gallery](https://www.powershellgallery.com/packages/SecretManagement.Keybase/).

## Quick Start

### Register a Vault

Register a vault for personal use:

```PowerShell
Register-KeybaseSecretVault -Name 'MyKeybaseVault' -Namespace 'my-namespace'
```

Register a vault for team use:

```PowerShell
Register-KeybaseSecretVault -Name 'TeamVault' -Namespace 'team-namespace' -Team 'myteam'
```

### Store and Retrieve Secrets

```PowerShell
# Store a string secret
Set-Secret -Name 'ApiKey' -Secret 'my-api-key-123' -Vault 'MyKeybaseVault'

# Retrieve a secret
$apiKey = Get-Secret -Name 'ApiKey' -Vault 'MyKeybaseVault'

# Remove a secret
Remove-Secret -Name 'ApiKey' -Vault 'MyKeybaseVault'
```

## Usage Examples

### Working with Different Secret Types

#### String Secrets

```PowerShell
# Store a string
Set-Secret -Name 'DatabaseConnectionString' -Secret 'Server=localhost;Database=MyDB' -Vault 'MyKeybaseVault'

# Retrieve as string
$connectionString = Get-Secret -Name 'DatabaseConnectionString' -Vault 'MyKeybaseVault'
```

#### SecureString Secrets

```PowerShell
# Create and store a SecureString
$password = ConvertTo-SecureString -String 'MySecurePassword123' -AsPlainText
Set-Secret -Name 'AdminPassword' -Secret $password -Vault 'MyKeybaseVault'

# Retrieve as SecureString
$storedPassword = Get-Secret -Name 'AdminPassword' -Vault 'MyKeybaseVault'
```

#### PSCredential Secrets

```PowerShell
# Create and store credentials
$securePassword = ConvertTo-SecureString -String 'UserPassword' -AsPlainText
$credential = New-Object System.Management.Automation.PSCredential('username', $securePassword)
Set-Secret -Name 'ServiceAccount' -Secret $credential -Vault 'MyKeybaseVault'

# Retrieve credentials
$storedCredential = Get-Secret -Name 'ServiceAccount' -Vault 'MyKeybaseVault'
$storedCredential.UserName
$storedCredential.Password
```

#### ByteArray Secrets

```PowerShell
# Create and store binary data
$buffer = [System.Byte[]]::new(256)
$random = [System.Random]::new()
$random.NextBytes($buffer)
Set-Secret -Name 'EncryptionKey' -Secret $buffer -Vault 'MyKeybaseVault'

# Retrieve binary data
$storedKey = Get-Secret -Name 'EncryptionKey' -Vault 'MyKeybaseVault'
```

#### Hashtable Secrets

```PowerShell
# Store a hashtable
$config = @{
    'ApiUrl' = 'https://api.example.com'
    'Timeout' = 30
    'RetryCount' = 3
}
Set-Secret -Name 'AppConfig' -Secret $config -Vault 'MyKeybaseVault'

# Retrieve hashtable
$storedConfig = Get-Secret -Name 'AppConfig' -Vault 'MyKeybaseVault'
$storedConfig.ApiUrl
```

### Querying Secrets

#### List All Secrets

```PowerShell
# Get information about all secrets
Get-SecretInfo -Vault 'MyKeybaseVault'
```

#### Filter Secrets with Wildcards

```PowerShell
# Find all secrets starting with "Api"
Get-SecretInfo -Filter 'Api*' -Vault 'MyKeybaseVault'

# Find secrets matching a pattern
Get-SecretInfo -Filter '*Password*' -Vault 'MyKeybaseVault'
```

#### Get Secret Information

```PowerShell
# Get metadata about a specific secret (without retrieving the value)
$secretInfo = Get-SecretInfo -Name 'ApiKey' -Vault 'MyKeybaseVault'
$secretInfo.Name      # Secret name
$secretInfo.Type      # Secret type (String, SecureString, etc.)
$secretInfo.VaultName # Vault name
```

### Vault Management

#### Test Vault Configuration

```PowerShell
# Verify vault is properly configured
Test-SecretVault -VaultName 'MyKeybaseVault'
```

#### List Registered Vaults

```PowerShell
# View all registered secret vaults
Get-SecretVault
```

#### Unregister a Vault

```PowerShell
# Remove a vault registration (does not delete secrets in Keybase)
Unregister-SecretVault -Name 'MyKeybaseVault'
```

## Secret Type Support

The module supports the following secret types with automatic serialization/deserialization:

- ✅ **ByteArray** - Binary data stored as Base64-encoded strings
- ✅ **String** - Plain text strings
- ✅ **SecureString** - Encrypted with a randomly generated key before storage
- ✅ **PSCredential** - Username and password pairs (password encrypted)
- ✅ **Hashtable** - Key-value pairs stored as JSON

## How It Works

### Architecture

This module implements the PowerShell Secret Management extension interface, providing:

- **Register-KeybaseSecretVault**: Registers a Keybase KV store as a secret vault
- **Set-Secret**: Stores secrets in Keybase KV store with type-aware serialization
- **Get-Secret**: Retrieves and deserializes secrets from Keybase KV store
- **Remove-Secret**: Deletes secrets from Keybase KV store
- **Get-SecretInfo**: Lists and queries secrets with wildcard support
- **Test-SecretVault**: Validates vault configuration

### Serialization

Secrets are serialized to JSON format before storage:

- **Strings**: Stored directly
- **ByteArrays**: Base64-encoded
- **Hashtables**: JSON-serialized
- **SecureStrings**: Encrypted with a random 32-byte key, then Base64-encoded
- **PSCredentials**: Username stored as plain text, password encrypted with a random 32-byte key

### Keybase Integration

The module uses the Keybase CLI (`keybase kvstore api`) to interact with Keybase's KV store. All operations are performed through Keybase's encrypted API, ensuring secrets are encrypted both in transit and at rest.

### Team Support

When registering a vault with the `-Team` parameter, secrets are stored in a team namespace, allowing team members with appropriate permissions to access shared secrets.

## Requirements

- **PowerShell Version**: 7.0.0 or later (PowerShell Core only)
- **Required Module**: Microsoft.PowerShell.SecretManagement
- **External Dependency**: Keybase CLI must be installed and authenticated

## Project Information

- **Author**: Tigran TIKSN Torosyan
- **Version**: 1.3.0
- **License**: See [LICENSE](LICENSE) file
- **Project Repository**: [GitHub](https://github.com/tiksn/SecretManagement.Keybase)
- **PowerShell Gallery**: [SecretManagement.Keybase](https://www.powershellgallery.com/packages/SecretManagement.Keybase/)

## Related Resources

- [PowerShell Secret Management Documentation](https://learn.microsoft.com/powershell/module/microsoft.powershell.secretmanagement/)
- [Keybase Documentation](https://book.keybase.io/docs)
- [Keybase KV Store API](https://book.keybase.io/docs/bots)

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests on the [GitHub repository](https://github.com/tiksn/SecretManagement.Keybase).
