# azure

# Steps to enable WinRM
# Reference
Manually enable WinRM:  https://www.visualstudiogeeks.com/devops/how-to-configure-winrm-for-https-manually
Azure command line:  https://docs.microsoft.com/en-us/cli/azure/reference-index?view=azure-cli-latest
Script to enable WinRM:  https://github.com/ansible/ansible/blob/devel/examples/scripts/ConfigureRemotingForAnsible.ps1
Playbook to enable WinRM:  https://dev.to/cloudskills/provisioning-azure-resources-with-ansible-be2

In a Powershell window, run the following commands

New-SelfSignedCertificate -DnsName <YOUR_HOSTNAME>.internal.cloudapp.net -CertStoreLocation Cert:\LocalMachine\My

winrm create winrm/config/Listener?Address=*+Transport=HTTPS '@{Hostname="<YOUR_DNS_NAME>"; CertificateThumbprint="<COPIED_CERTIFICATE_THUMBPRINT>"}'

winrm get winrm/config
winrm e winrm/config/listener

Add a new firewall rule

port=5986
netsh advfirewall firewall add rule name="Windows Remote Management (HTTPS-In)" dir=in action=allow protocol=TCP localport=$port
