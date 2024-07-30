## MVP 

1) Fork https://github.com/SharePoint/sp-dev-provisioning-templates
2) Create a new site and apply template (https://github.com/SharePoint/sp-dev-provisioning-templates/tree/master/tenant/contosoworks) to it. This can be on dev tenant vbtnd.onmicrosoft.com or your own. Provide link as response
3) Modify template to include the new years for Global Country Holiday, include ANZ public holidays.
4) Capture the site and push to forked RP with PR and merge
5) Create script to apply this template to 10000 sites. Remember title, description and URL will be different for each of these sites. Add this script as README.md to GitHub repo
6) Explain your approach for applying this template on demand via Azure
7) Explain Your approach for integrating a solution in step 6 into other systems

## SUMMARY 

This repository contains a modified contosoworks Sharepoint template. It can be applied using Powershell.

Found below is a copy of a script I have created that allows you to apply this template to multiple sites.

#### 5

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

#### 6

#### 7

## CONCLUSION
