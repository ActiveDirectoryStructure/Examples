# Usage

All commands require the PowerShell Module:

```powershell
Import-Module ActiveDirectoryStructure
```

Additionally a RootPath to the Structure folder is required. The folder needs to stay as in the example:

```powershell
$RootPath = "C:\Temp\Structure"
```

# General

Inside the 'Structure.xml' is the Domain name specified (ADDC and ADDN).
These are used in all of the following commands. So changed them to your Domain before using.

# Create an export of the current AD

This command creates an XML report of the current AD to compare to the new, generated AD

```powershell
New-ADSReport -RootPath $RootPath -OutputPath $OutputPath
```

# Create an export of the defined AD

This command creates an XML report of the 'Structure.xml' with everything expand (e.g. variabls applied and GPOGroups expanded to their GPOs).
This can be used to test the generator and make sure the correct templates are generated.
Also you can use this to compare to the current AD and find the differences.

```powershell
New-ADSGeneratedReport -RootPath $RootPath -OutputPath $OutputPath
```

# Apply the changes to the AD

> **Warning**
> This can have significant impact on your AD. Make sure to run with -WhatIf and -Verbose first and check all changes.

This command applys the template to the AD.

```powershell
Confirm-ADSDefaultStructure -RootPath $RootPath -WhatIf
```

The command also has multiple parameters like -SkipOUDelete or -NoACL to further limit what exactly is done. Check them out before running.

> **Note**
> No matter if -SkipOUDelete is specified or not, the script only ever tries to delete empty OU's (e.g. no objects inside the OU)
