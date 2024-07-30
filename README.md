## Summary 

This repository contains a modified contosoworks Sharepoint template (/contosoworks/source/template.xml). It can be applied using Powershell.

Found below is a copy of a script I have created that allows you to apply this template to multiple sites.

## Build Steps

1. Set up SharePoint Account
2. Have Powershell downloaded and up to date
3. Make a local copy of this repository
4. Adjust variables in powershell script to specified requirements

## Question 5

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

## Problems

* The Sharepoint module commands are not available for Mac hence you cannot use the `SPOS` commands. Easily worked around by using the `Connect-PnPOnline`

## Future Improvements

* CSV file integration to allow for more precise personalisation
* Hosted on Azure

## Further Questions

#### QUESTION 6

I would create an Azure Function that would contain my adjusted Powershell script. I would then configure it such that it is triggered by an HTTP request (coming from either an API or the script).

#### Question 7

I would first need to determine in what way the Function is integrated into this new system be it HTTP reqeusts or an API. Assuming that I go with the API approach, I would use an API gateway to integrate in this Function. I have experience with AWS, GCP and Azure. The rest of the set up is fairly straightforward between Cloud Computing Platforms involving setting up endpoints for the function, authorisation, security and testing.

## Conclusion

This has been a really rewarding assignment. I've enjoyed getting stuck into Powershell and learning about Microsoft SharePoint. Please don't hesitate to get in contact if you had any questions.
