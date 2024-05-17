
# Customise command prompt and terminal settings in PowerShell 7:

A: Terminal 
Install-Module -Name Terminal-Icons -Repository PSGallery
Import-Module -Name Terminal-Icons

B: 
1. Define the Custom Prompt Script Block:
```pwsh
$CustomPrompt = {
    $host.UI.RawUI.WindowTitle = Microsoft.PowerShell.Management\Split-Path $pwd.ProviderPath -Leaf
    $Host.UI.RawUI.ForegroundColor = "White"
    $currentDirectory = (Get-Item -Path $pwd).Name
    Microsoft.PowerShell.Utility\Write-Host "$currentDirectory " -NoNewLine -ForegroundColor Green
    # Add any additional customizations here
    $happyPrompts = @('🍺'; '😀'; '🤜'; '🎉'; '🤟'; '✔'; '👌'; '🌈'; '❤'; '💯'; '🆗'; '🗨'; '🌍'; '🌎'; '🌏'; '🌐'; '🌊'; '🌋'; '🌤'; '⛅'; '🌥'; '🌦'; '☔')
    $prompt = $happyPrompts[(Get-Random -min 0 -max ($happyPrompts.Length))]
    Microsoft.PowerShell.Utility\Write-Host "`n$prompt " -NoNewLine -ForegroundColor "DarkGray"
    return " "
}
```
2. Assign the Custom Prompt to a Function:

`Set-Item -Path function:\custom_prompt -Value $CustomPrompt`

3. Set the custom_prompt Function as the Prompt:

`$function:prompt = $function:custom_prompt`


## One line code
$CustomPrompt = { $host.UI.RawUI.WindowTitle = Microsoft.PowerShell.Management\Split-Path $pwd.ProviderPath -Leaf ; $Host.UI.RawUI.ForegroundColor = "White" ; $currentDirectory = (Get-Item -Path $pwd).Name ;     Microsoft.PowerShell.Utility\Write-Host "$currentDirectory " -NoNewLine -ForegroundColor Green ; $happyPrompts = @('🍺'; '😀'; '🤜'; '🎉'; '🤟'; '✔'; '👌'; '🌈'; '❤'; '💯'; '🆗'; '🗨'; '🌍'; '🌎'; '🌏'; '🌐'; '🌊'; '🌋'; '🌤'; '⛅'; '🌥'; '🌦'; '☔') ; $prompt = $happyPrompts[(Get-Random -min 0 -max ($happyPrompts.Length))] ; Microsoft.PowerShell.Utility\Write-Host "`n$prompt " -NoNewLine -ForegroundColor "DarkGray" ; return " " ; } ; Set-Item -Path function:\custom_prompt -Value $CustomPrompt ; $function:prompt = $function:custom_prompt


## Undoing Custom Prompt in PowerShell:
To revert to the default prompt or remove the custom prompt setup:

1. Reset the Prompt to Default:

$function:prompt = $function:default

2. Remove the Custom Prompt Function:

Remove-Item function:\custom_prompt
