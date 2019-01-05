# VSTS Auto Deployment for SPFx package using SharePoint App ID Secret

1. Create a SharePoint App ID and Secret using the url https://tenant.sharepoint.com/sites/sitename/_layouts/appregnew.aspx
2. Save the App ID and Secret 
3. Grant Full Control Permission to the app on the site (for site collection levels apps)/ Tenant App catalog site (for tenant level apps)		
	1. Go to https://tenant.sharepoint.com/sites/sitename/_layouts/appinv.aspx
	2. Enter App ID saved in step no. 2 and hit lookup
	3. Enter permission xml from the permissionxml file          
  	4. Click Ok	
4. Got to VSTS Pipelines
5. Create Release Pipeline
6. Remove existing tasks and add 2 powershell tasks
7. For 1st task add commands to Install Pnp module
8. For second powershell Task add the following Inline task
	1. Connect-PnPOnline  -AppId $AppId -AppSecret $AppSecret -Url $SiteUrl
	2. Add-PnPApp -Path $packagePath -Scope Site -Publish -Overwrite 'OR'
	3. Add-PnPApp -Path $packagePath -Publish -Overwrite
9. Save the Pipeline.
