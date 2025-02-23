# Uninstall-Software.ps1

## SYNOPSIS
Uninstall software based on the DisplayName of said software in the registry

## SYNTAX

```
Uninstall-Software [-DisplayName] <String> [[-Architecture] <String>] [[-HivesToSearch] <String[]>]
 [<CommonParameters>]
```

## DESCRIPTION
This script is useful if you need to uninstall software before installing or updating other software. 

Typically best used as a pre-script in most situations.

One example use case of this script with Patch My PC's Publisher is if you have previously re-packaged software installed
on your devices and you need to uninstall the repackaged software, and install using the vendor's native install media 
(provided by the Patch My PC catalogue).

The script searches the registry for installed software, matching the supplied DisplayName value in the -DisplayName parameter
with that of the DisplayName in the registry.
If one match is found, it uninstalls the software using the UninstallString. 

If a product code is not in the UninstallString, the whole value in UninstallString is used.

If more than one matches of the DisplayName occurs, uninstall is not possible.

If UninstallString is not present or null, uninstall is not possible.

## EXAMPLES

### EXAMPLE 1
```
Uninstall-Software.ps1 -DisplayName "Greenshot"
```

Uninstalls Greenshot if "Greenshot" is detected as the DisplayName in a key under either of the registry key paths:
    - SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall
    - SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

## PARAMETERS

### -DisplayName
The name of the software you wish to uninstall as it exactly appears in the registry as its DisplayName value.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Architecture
Choose which registry key path to search in while looking for installed software.
Acceptable values are:
    - "x86" will search in SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall on a 64-bit system.
    - "x64" will search in SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall.
    - "Both" will search in both key paths.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: Both
Accept pipeline input: False
Accept wildcard characters: False
```

### -HivesToSearch
Choose which registry hive to search in while looking for installed software.
Acceptabel values aref;
    - "HKLM" will search in hive HKEY_LOCAL_MACHINE which is typically where system-wide installed software is registered.
    - "HKCU" will search in hive HKEY_CURRENT_USER which is typically where user-based installed software is registered.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
Default value: HKLM
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).
