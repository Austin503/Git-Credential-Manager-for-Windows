# Git Helper Library for Visual Studio Online

This is a library for developing Git for Windows helpers.

## VSO Credential Helper
The VSO Credential Helper is fairly simple. It stores and retrieves credentials for accessing Git resources on VSO to and from a secure container.

There is full support for simple credentials (i.e. username + password), as well as for Microsoft Accounts (MSA), and Azure Directory Accounts (AAD).

Support for MSA and AAD based authentication relies on the VSO Personal Access Tokens (PAT) service.

Support for Git hosts other than VSO is limited to simple credentials.

### Configuring Git to Use the VSO Credential Helper

To set up use of a credential helper in Git you can use the following command `git config --global credential.helper !'<path_to_helper>'` or you can edit the config file directly via `git config --global --edit`.

Per web options can be added by specifying a URL without the protocol header and appending the option. Example `git config --global credential.visualstudio.com.helper.authority MSA`.

```
usage: git-credential-man <command> [<args>]

Configuration Options:
 * **authority** Defines the type of authentication to be used. Supportd Basic, AAD, and MSA. Default is Basic.
 * **clientid** Defines the client identifier for the authority. Defaults to visualstudio.com. Only used by AAD authority.
 * **resource** Defines the resource identifier for the authority. Defaults to visualstudio.com. Only used by AAD authority.
 * **interactive** Specifies if user can be prompted for credentials or not. Supports Auto, Always, or Never. Defaults to Auto. Only used by AAD authority.
 * **validate** Causes validation of credentials before supplying them to Git. Invalid credentials are attemped to refreshed before failing. Incurs some minor overhead. Defaults to TRUE. Ignore by Basic authority.

Example configuration
```
[credential "mseng.visualstudio.com"]
	authority = AAD
[credential "visualstudio.com"]
	authority = MSA
[credential]
	helper = !'C:\\Git\\Tools\\git-credential-man.exe'
```