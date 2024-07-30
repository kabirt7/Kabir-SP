Import-Module PnP.PowerShell

$siteNumber = 5
$tenantURL = "https://example.sharepoint.com"
$siteUser = "example@example.onmicrosoft.com"
$credential = Get-Credential -UserName $siteUser -Message "Enter the password for the SharePoint site"
$template = "./template.pnp"

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
        Apply-PnPProvisioningTemplate -Path $template
    }
    catch {
        Write-Error "An error has occurred creating website ${i}"
    }
}
