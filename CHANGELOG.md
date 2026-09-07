# Changelog

All notable changes to this project will be documented in this file. The format is based on [Keep a Changelog](https://keepachangelog.com/), and this project adheres to [Semantic Versioning](https://semver.org/).

## [2.0.0] - 2026-08-21

### Added

- Added three separate validation datasources for improved validation granularity:
  - `Exchange-On-Premises-Check-Alias-Unique` to validate mailbox alias uniqueness
  - `Exchange-On-Premises-Check-DisplayName-Unique` to validate display name uniqueness
  - `Exchange-On-Premises-Check-EmailAddress-Unique` to validate email address uniqueness
- Added new global variable `ADMailContactsOU` to specify the organizational unit for mail contacts
- Added comprehensive try-catch-finally error handling blocks with detailed error messages
- Added inline documentation links to Microsoft Exchange PowerShell documentation
- Added `actionMessage` variable for consistent error tracking throughout scripts
- Added property selection to limit memory usage and improve performance
- Added explicit command imports in session management (`New-MailContact`, `Set-MailContact`, `Get-Recipient`)
- Added `HiddenFromAddressListsEnabled` configuration via `Set-MailContact` cmdlet
- Added additional form category "Exchange Administration"
- Added disconnect audit logging in finally block

### Changed

- Refactored validation logic from two combined datasources into three specialized datasources
- Improved authentication method from Kerberos to Default for better compatibility
- Enhanced security by setting `SkipCACheck`, `SkipCNCheck`, and `SkipRevocationCheck` to `$false` instead of `$true`
- Updated session management with explicit command imports using `-CommandName` parameter
- Improved error handling with line number reporting and detailed error messages
- Renamed global variable from `ADContactsOU` to `ADMailContactsOU` for consistency
- Updated form category from "Exchange On-Premise" to "Exchange Administration" and "Exchange On-Premises"
- Enhanced TLS configuration to use `[System.Net.ServicePointManager]::SecurityProtocol` with TLS 1.2
- Improved logging with more detailed information messages and audit logs
- Standardized variable naming conventions throughout all scripts
- Changed datasource output format to include "Valid" or "Invalid" prefix for better form feedback
- Updated task name from "Exchange on-premise - Create Mailcontact" to "Exchange On-Premises - Mailcontact - Create"
- Enhanced recipient filtering logic with more comprehensive filter expressions

### Fixed

- Corrected session option parameters to improve connection reliability
- Fixed credential object creation with proper parameter syntax
- Improved session cleanup with proper error handling in finally block
- Fixed validation to check all recipient types using `Get-Recipient` instead of only specific types

## [1.0.0] - 2023-08-17

Initial release of HelloID-Conn-SA-Full-Exchange-On-Premises-Mailcontact-Create.

### Added

- Initial release for creating Exchange On-Premises Mail Contacts
- Form validation for external email address availability
- Boolean datasource for email address validation
- Basic Exchange On-Premises connectivity
