# Powershell

```text
# File Documents\WindowsPowerShell\profile.ps1

# Bash style tab completions
Set-PSReadlineKeyHandler -Key Tab -Function Complete
# Close terminal with Ctrl+d
Set-PSReadlineKeyHandler -Chord Ctrl+d -Function DeleteCharOrExit
```

## Setting Environment Variables

```text
# Setting environment variable PACKAGE_ROOT using current directory
$env:PACKAGE_ROOT=$pwd.Path+"\package_1_0"
```

