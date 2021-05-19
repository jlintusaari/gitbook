# Powershell

```text
# File Documents\WindowsPowerShell\profile.ps1

# Bash style tab completions
Set-PSReadlineKeyHandler -Key Tab -Function Complete
# Close terminal with Ctrl+d
Set-PSReadlineKeyHandler -Chord Ctrl+d -Function DeleteCharOrExit
```

