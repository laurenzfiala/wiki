Windows > PowerShell

## Changing PowerShell Display Path

Sometimes it can get really annoying to see the whole path of the working directory in powershell. In the following I explain how to change that.

### Usecases

- When you only see your current working directory in the PowerShell, but need to actually work

### What to do

1. Create a new plaintext file (and necessary parent folders) at `%userprofile%\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1`

2. Contents of the file should be:

   ```
   function prompt {
     $p = Split-Path -leaf -path (Get-Location)
     "$p> "
   }
   ```

3. Open PowerShell as administrator

4. Execute `Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy Unrestricted -Force` once

### Further information

`Set-ExecutionPolicy` disables security features for the current user, so the profile can be executed without an error. If a script originates directly from the internet, PowerShell is still asking for permission.

#### Helpful resources

[Stack Overflow (Profile Script)](https://superuser.com/questions/446827/configure-the-windows-powershell-to-display-only-the-current-folder-name-in-the)

[Stack Overflow (Permission)](https://superuser.com/questions/106360/how-to-enable-execution-of-powershell-scripts)