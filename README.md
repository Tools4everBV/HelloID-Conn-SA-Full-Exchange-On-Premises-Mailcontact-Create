# HelloID-Conn-SA-Full-Exchange-On-Premises-Mailcontact-Create

| :information_source: Information                                                                                                                                                                                                                                                                                                                                                          |
| :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| This repository contains the connector and configuration code only. The implementer is responsible for acquiring the connection details such as username, password, certificate, etc. You might even need to sign a contract or agreement with the supplier before implementing this connector. Please contact the client's application manager to coordinate the connector requirements. |

## Description

_HelloID-Conn-SA-Full-Exchange-On-Premises-Mailcontact-Create_ is a template designed for use with HelloID Service Automation (SA) Delegated Forms. It can be imported into HelloID and customized according to your requirements.

By using this delegated form, you can create mail contacts in Exchange On-Premises. The following workflow is available:

1.  Enter the details for the new mail contact (first name, initials, last name, display name, alias, and external email address)
2.  The form validates that the display name is unique and not already in use
3.  The form validates that the alias is unique and not already in use
4.  The form validates that the external email address is unique and not already in use
5.  Upon successful validation, the mail contact is created in Exchange On-Premises
6.  The mail contact address list visibility is configured based on the selected option

## Getting started

### Requirements

- **Exchange On-Premises Server**:<br>
  A functioning Exchange On-Premises environment with PowerShell remote management enabled. The Exchange server must be accessible from the HelloID agent.
- **Active Directory Organizational Unit**:<br>
  An organizational unit (OU) in Active Directory where mail contacts will be created. The service account must have permissions to create objects in this OU.
- **PowerShell Remoting**:<br>
  PowerShell remoting must be enabled on the Exchange server. The Exchange Management Shell must be accessible via remote PowerShell session.
- **Service Account Permissions**:<br>
  A service account with sufficient permissions to create and manage mail contacts in Exchange On-Premises. The account must have access to the Exchange Management Shell cmdlets and the specified organizational unit.

### Connection settings

The following user-defined variables are used by the connector.

| Setting               | Description                                             | Mandatory |
| --------------------- | ------------------------------------------------------- | --------- |
| ExchangeConnectionUri | The URI to the Exchange On-Premises PowerShell endpoint | Yes       |
| ExchangeAdminUsername | The username for the Exchange administrator account     | Yes       |
| ExchangeAdminPassword | The password for the Exchange administrator account     | Yes       |
| ADMailContactsOU      | The organizational unit where mail contacts are created | Yes       |

## Remarks

### Authentication Method

The connector uses Default authentication instead of Kerberos for better compatibility across different Exchange configurations. Ensure that the service account has appropriate permissions and that the Exchange server accepts Default authentication.

### Session Security Settings

The connector sets `SkipCACheck`, `SkipCNCheck`, and `SkipRevocationCheck` to `$false` for enhanced security. If your environment uses self-signed certificates or has certificate validation issues, you may need to adjust these settings, though this is not recommended for production environments.

### Validation Approach

The connector uses three separate datasources to validate uniqueness:

- **Display Name Validation**: Checks if the display name or name already exists for any mail contact
- **Alias Validation**: Verifies that the alias (mailNickname) is not used by any recipient, including all mailbox types and mail-enabled objects
- **Email Address Validation**: Ensures the external email address is not already assigned to any recipient in the Exchange organization, checking both primary SMTP addresses and proxy addresses

### Organizational Unit Requirement

Mail contacts must be created in a specific organizational unit defined by the `ADMailContactsOU` variable. Ensure this OU exists in Active Directory and that the service account has create permissions on this OU.

### Command Import Strategy

The connector explicitly imports only the required Exchange cmdlets (`New-MailContact`, `Set-MailContact`, `Get-Recipient`, `Get-Mailcontact`) to minimize session overhead and improve performance.

## Development resources

### API endpoints

The connector uses Exchange On-Premises PowerShell cmdlets:

| Cmdlet          | Description                               |
| --------------- | ----------------------------------------- |
| New-MailContact | Creates a new mail contact in Exchange    |
| Set-MailContact | Configures mail contact properties        |
| Get-Recipient   | Queries recipients to validate uniqueness |
| Get-Mailcontact | Queries mail contacts for validation      |

### API documentation

- [Exchange Server PowerShell](https://learn.microsoft.com/en-us/powershell/exchange/exchange-management-shell)
- [Connect to Exchange Servers using remote PowerShell](https://learn.microsoft.com/en-us/powershell/exchange/connect-to-exchange-servers-using-remote-powershell)
- [New-MailContact](https://learn.microsoft.com/en-us/powershell/module/exchange/new-mailcontact)
- [Set-MailContact](https://learn.microsoft.com/en-us/powershell/module/exchange/set-mailcontact)
- [Get-Recipient](https://learn.microsoft.com/en-us/powershell/module/exchange/get-recipient)

## Getting help

> :bulb: **Tip:**  
> _For more information on Delegated Forms, please refer to our [documentation](https://docs.helloid.com/en/service-automation/delegated-forms.html) pages_.

## HelloID docs

The official HelloID documentation can be found at: https://docs.helloid.com/
