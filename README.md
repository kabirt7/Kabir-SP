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

## BUILD STEPS

1. Set up SharePoint Account
2. Have Powershell downloaded and up to date
3. Make a local copy of this repository
4. Adjust variables in powershell script to specified requirements

## QUESTION 5

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

#### QUESTION 6

I would create an Azure Function that would contain my adjusted Powershell script. I would then configure it such that it is triggered by an HTTP request (coming from either the application of the script)

#### QUESTION 7

I would first need to determine in what way the Function is integrated into this new system be it HTTP reqeusts or an API. Assuming that I go with the API approach, I would use an API gateway to integrate in this Function. I have experience with AWS, GCP and Azure. The rest of the set up is fairly straightforward between Cloud Computing Platforms involving setting up endpoints for the function, authorisation, security and testing.

## CONCLUSION

This has been a really rewarding assignment. I've enjoyed getting stuck into Powershell and learning about Microsoft SharePoint. Please don't hesitate to get in contact if you had any questions :)
