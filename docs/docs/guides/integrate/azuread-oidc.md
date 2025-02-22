---
title: Connect with AzureAD through OIDC
---

## AzureAD Tenant as Identity Provider for ZITADEL

This guides shows you how to connect an AzureAD Tenant to ZITADEL.

:::info
In ZITADEL you can connect an Identity Provider (IdP) like an AzureAD to your instance and provide it as default to all organizations or you can register the IdP to a specific organization only. This can also be done through your customers in a self-service fashion.
:::

### Prerequisite

You need to have access to an AzureAD Tenant. If you do not yet have one follow [this guide from Microsoft](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-create-new-tenant) to create one for free.

### AzureAD Configuration

#### Create a new Application

Browse to the [App registration menus create dialog](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/CreateApplicationBlade/quickStartType~/null/isMSAApp~/false) to create a new app.

![Create an Application](/img/guides/azure_app_register.png)

:::info
Mare sure to select `web` as application type in the `Redirect URI (optional)` section.
You can leave the second field empty since we will change this in the next step.
:::

![Create an Application](/img/guides/azure_app.png)

#### Configure Redirect URIS

For this to work you need to whitelist the redirect URIs from your ZITADEL Instance.
In this example our test instance has the domain `test-qcon0h.zitadel.cloud`. In this case we need to whitelist these two entries:

- `https://test-qcon0h.zitadel.cloud/ui/login/register/externalidp/callback`
- `https://test-qcon0h.zitadel.cloud/ui/login/login/externalidp/callback`

:::info
To adapt this for you setup just replace the domain
:::

![Configure Redirect URIS](/img/guides/azure_app_redirects.png)

#### Create Client Secret

To allow your ZITADEL to communicate with the AzureAD you need to create a Secret

![Create Client Secret](/img/guides/azure_app_secrets.png)

:::info
Please save this for the later configuration of ZITADEL
:::

#### Configure ID Token Claims

![Configure ID Token Claims](/img/guides/azure_app_token.png)

### ZITADEL Configuration

#### Create IdP

Use the values displayed on the AzureAD Application page in your ZITADEL IdP Settings.

- You can find the `issuer` for ZITADEL of your AzureAD Tenant in the `Endpoints submenu`
- The `Client ID` of ZITADEL corresponds to the `Application (client) ID`
- The `Client Secret` was generated during the `Create Client Secret` step

![Azure Application](/img/guides/azure_app.png)

![Create IdP](/img/guides/azure_zitadel_settings.png)

#### Activate IdP

Once you created the IdP you need to activate it, to make it usable for your users.

![Activate the AzureAD](/img/guides/azure_zitadel_activate.png)

![Active AzureAD](/img/guides/azure_zitadel_active.png)

### Test the setup

To test the setup use a incognito mode and browse to your login page. 
If you succeeded you should see a new button which should redirect you to your AzureAD Tenant.

![AzureAD Button](/img/guides/azure_zitadel_button.png)

![AzureAD Login](/img/guides/azure_login.png)
