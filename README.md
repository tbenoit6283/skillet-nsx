# Automated configuration of NSX-V for Panorama

### Pre-Requisite :
- Panorama 8.1.X with one of the NSX plugin 2.0.X installed


### This skillet will automate these tasks for you on Panorama :
- create a Template Stack and a Template dedicated for NSX-V with DNS and NTP server configured with webpage variables.
- create a Device Group dedicated for NSX-V with the authcode configured with webpage variables.
- create a Service Definition and a Service Manager profile with a single Service Profile "Tenant" attached to the service Definition. 
- create an empty DAG with a TAG attached to it that will be pushed into NSX-Manager for demo as a Security Group.
- create 2 intrazone pre-rulebase firewall security rules for your tenant with Security Profiles, Log Forwarding Profile and a dedicated TAG for that tenant to filter both incoming and outgoing traffic of that Security Group members.
- automatically generate the NSX Manager Steering Rule Policies on panorama that fits the previous pre-rulebase.
- create an HTTP log forwarding profile on panorama to provide "automated quarantine" on NSX Manager in case of a virus detection in one of our VM series agent firewall.     

Notice that if you want a second ("Tenant"), you just need to launch the Skillet a second time and just modify the "Tenant" name variable at the end of the webpage with your second "Tenant" name 

## Variables
- STACK (Template Stack name for NSX)
- DEVICEGROUP (Device Group name for NSX)
- AUTHCODE (AuthCode VM series for NSX)
- URLOVA (URL where ovf/ova package is hosted)
- NSXLOGIN (NSX Manager login)
- NSXMANAGER (NSX Manager IP Address)
- NSXPASSWORD (NSX Manager password)
- DNS (DNS Server IP address)
- NTP (NTP Server IP address)
- TENANT (Tenant name for Zone creation)
- TAGCOLOR (Color of the TAG for your Tenant)

## Caution  
- That skillet will not deploy our VM agents on NSX manager nor configure it for deployment, it's panorama configuration only. 
- That skillet will create only one single Security Group into NSX Manager linked to one single DAG in panorama. Additional DAGs/Security Groups must be added manually after you apply the skillet if you need more on your setup.
- Generation of the certificate, signature of that certifcate, extraction and installation of that certificate into NSX Manager is not part of that skillet. That step need to be manually done after you launch the skillet to have that automated quarantine feature fully functional.  

## Support Policy

Have been tested with a single instance of panorama 8.1.X in panorama mode and plugin 2.0.X but should work as well with 9.0.X release.
Works with all the release of NSX-V that we support officially
Will not work if you use log collectors so logs must be stored in panorama locally. 

The code and templates in the repo are released under an as-is, best effort,
support policy. These scripts should be seen as community supported and
Palo Alto Networks will contribute our expertise as and when possible.
We do not provide technical support or help in using or troubleshooting the
components of the project through our normal support options such as
Palo Alto Networks support teams, or ASC (Authorized Support Centers)
partners and backline support options. The underlying product used
(the VM-Series firewall) by the scripts or templates are still supported,
but the support is only for the product functionality and not for help in
deploying or using the template or script itself. Unless explicitly tagged,
all projects or work posted in our GitHub repository
(at https://github.com/PaloAltoNetworks) or sites other than our official
Downloads page on https://support.paloaltonetworks.com are provided under
the best effort policy.