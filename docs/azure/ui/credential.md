## Setting up Azure Credentials

Cloudbreak works by connecting your AZURE account through so called *Credentials*, and then uses these credentials to 
create resources on your behalf. The credentials can be configured on the **manage credentials** panel on the 
Cloudbreak Dashboard.

>Please read the [Provisioning prerequisites](azure.md#azure-application-setup-with-cloudbreak-deployer) where you 
can find the steps how can get the mandatory `Subscription ID`, `App ID`, `Password` and `App Owner Tenant ID` for 
your Cloudbreak credential.

To create a new AZURE credential you have two options:

- Interactive login
- App based
  
## Interactive login

**Before you can use interactive login, you have to provide your tenant ID and subscription ID in your Profile**

* `export AZURE_TENANT_ID=********-d98e-4c64-9301-**************`

* `export AZURE_SUBSCRIPTION_ID=********-8a1d-4ac9-909b-************`

#### Steps

1. Fill out the new credential `Name`
    * Only alphanumeric and lowercase characters (min 5, max 100 characters) can be applied
    
2. Copy your SSH public key to the `SSH public key` field
    * The SSH public key must be in OpenSSH format and it's private keypair can be used later to [SSH onto every instance](operations.md#ssh-to-the-hosts) of every cluster you'll create with this credential.
      - The **SSH username** for the AZURE instances is **cloudbreak**.
  
3. Click next. Then you will see a device code on the screen. Click on the 'Azure login' button and please enter the code on the azure portal. 

    ![](/azure/images/azure-device-code.png "Azure device code")
  
4. Select the account you wish to use 
    * This account must be in the same subscription and tenant what you previously provided in your Profile otherwise the credential creation will fail. 
    
    ![](/azure/images/azure-select-account.png "Select account") 
  
5. After that you should see a progress bar like on the image below 

    ![](/azure/images/azure-interactive-3.png)

## App based
   - Fill out the new credential `Name`
       * Only alphanumeric and lowercase characters (min 5, max 100 characters) can be applied
   - Copy your AZURE Subscription ID to the `Subscription Id` field

![](/azure/images/azure-subscription.png)
<sub>*Full size [here](/azure/images/azure-subscription.png).*</sub>

  - Copy your AZURE Active Directory Application:
    * ID to the `App Id` field
    * password to the `Password` field
    * `App Owner Tenant Id` field

![](/azure/images/azure-application.png)
<sub>*Full size [here](/azure/images/azure-application.png).*</sub>

  - Copy your SSH public key to the `SSH public key` field
    * The SSH public key must be in OpenSSH format and it's private keypair can be used later to [SSH onto every 
    instance](operations.md#ssh-to-the-hosts) of every cluster you'll create with this credential.
    - The **SSH username** for the AZURE instances is **cloudbreak**.

>Any other parameter is optional here.

>`Public in account` means that all the users belonging to your account will be able to use this credential to create 
clusters, but cannot delete it.

> Cloudbreak is supporting simple rsa public key instead of X509 certificate file after 1.0.4 version

![](/azure/images/azure-credentials.png)
<sub>*Full size [here](/azure/images/azure-credentials.png).*</sub>

## Infrastructure Templates

After your AZURE account is linked to Cloudbreak you can start creating resource templates that describe your clusters' 
infrastructure:

- templates
- networks
- security groups

When you create one of the above resources, **Cloudbreak does not make any requests to AZURE. Resources are only created
 on AZURE after the `create cluster` button has pushed.** These templates are saved to Cloudbreak's database and can be 
 reused with multiple clusters to describe the infrastructure.
