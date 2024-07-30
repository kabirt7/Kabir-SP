## SUMMARY 

This repository contains a modified contosoworks Sharepoint template. It can be applied using Powershell.

Found below is a copy of a script I have created that allows you to apply this template to multiple sites.

5)

```ps

Import-Module PnP.PowerShell

$siteNumber = 5
$tenantURL = "https://example.sharepoint.com"
$credential = Get-Credential -UserName "example@example.onmicrosoft.com" -Message "Enter the password for SharePoint site"
$template = "./template.pnp"
$siteUser = "example@example.onmicrosoft.com"

Connect-PnPOnline -Url $tenantURL -Credential $credential

for ($i = 1; $i -le $siteNumber; $i++) {

    $siteURL = "$tenantURL/sites/website$i"
    $siteTitle = "website $i"
    $siteDescription = "this is a description about website $i"

    try {
        Write-Host "Website $siteURL is being created"
        New-PnPSite -Type CommunicationSite -Title $siteTitle -Url $siteURL -Owner $siteUser -Description $siteDescription
        Write-Host "Website $siteURL has been created"

        Write-Host "Website $siteURL is having template applied"
        Invoke-PnPSiteTemplate -siteUrl $siteURL -Path $template
    }
    catch {
        Write-Error "An error has occurred creating website ${i}"
    }
}
```

## PROBLEMS

* The Sharepoint module commands are not available for Mac hence you cannot use the `SPOS` commands. Easily worked around by using the `Connect-PnPOnline`

## FURTHER QUESTIONS

6)

7)

## CONCLUSION
