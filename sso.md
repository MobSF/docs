## SSO support in MobSF

MobSF now supports SSO using SAML2, starting with version 4.0.1.

There are three user roles:

1. `Admin`: This is the primary administrator account created during the initial setup. This role can manage users with other roles.
2. `Maintainer`: This role has permission to scan, suppress, and delete.
3. `Viewer`: This role is read-only and can only view the scan results.

For SSO integration, we only support `Maintainer` and `Viewer` roles.


!> When SSO is enabled, password authentication and `Admin` role is turned off by default. To allow password login or admin account, set the environment variable `MOBSF_SP_ALLOW_PASSWORD` to `1` before running MobSF.


### How to Setup Okta SSO?

The section covers how you can set up MobSF with Okta for SSO. 

To setup Okta SSO, you need the Assertion Consumer Service URL from MobSF

* **Assertion Consumer Service (ACS) URL** - This is where Okta sends the SAML assertion via HTTP POST. The ACS URL is `<http/https>://<mobsf_host>:<mobsf_port>/sso/acs/`. For example, if you have MobSF running in your local environment, the ACS URL will be `http://localhost:8000/sso/acs/`

To enable Okta SSO in MobSF, you need the Metadata URL from Okta.

* **Metadata URL** - This Okta URL contains metadata information required by MobSF, such as the entity ID, X509 Certificate, and SSO URL.

#### Okta Configuration

1. Log in to your Okta Admin account.
2. Under **Applications**, click on **Create App Integration**.
3. Choose **SAML 2.0** and click **Next**.
4. In the **General Settings**, configure the following:
    * **App Name**: `MobSF`
    * **App logo**: [Use the MobSF Logo](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/9925f41c-bd53-4ef5-a4e5-e6b18ce4ba6d)

<img width="1060" alt="MobSF App Integration" src="https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/fefcbe0f-3c4b-400d-9e88-dfd19e836e73">

5. In the next **Configure SAML** tab, configure the following:
    * **Single sign-on URL**: `<MobSF ACS URL>`
        * Check the box `Use this for Recipient URL and Destination URL`
    * **Audience URI (SP Entity ID)**: `<MobSF ACS URL>`
    * **Name ID format**: `EmailAddress`
    * **Application username**: `Email`
    * **Update application username on**: `Create and Update`
6. Under the **Attribute Statements (optional)** section, create a new attribute statement to send the user email to MobSF.
    * **Name**: `email`
    * **Name format**: `Unspecified`
    * **Value**: `user.email`
7. Under the **Group Attribute Statements (optional)** section, create a new attribute statement to send appropriate roles to MobSF.
    * **Name**: `role`
    * **Name format**: `Unspecified`
    * **Filter**: `Matches Regex`, `.*`

<img width="559" alt="SAML settings" src="https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/b7b9a2de-8d11-4f24-b8ac-1efe893ebafd">

8. In the next **Feedback** screen, tick the `This is an internal app that we have created` option and click **Finish** to create the MobSF Okta integration.

9. You must create at least two Okta groups for the MobSF roles `Maintainer` and `Viewer`. The group name should contain the string `maintainer` in it to be associated with the `Maintainer` role, and `viewer` to be associated with the `Viewer` role. Yoy can use SSO groups mapping whith environment variables `MOBSF_IDP_MAINTAINER_GROUP` and `MOBSF_IDP_VIEWER_GROUP` to map your custom Okta groups to MobSF `Maintainer` and `Viewer` roles. If you want to authorize SSO logged-in users without any suitable SSO groups you can use environment variable `MOBSF_IDP_DEFAULT_GROUP=Viewer` or `MOBSF_IDP_DEFAULT_GROUP=Maintainer` to authorize as `Viewer` or `Maintainer`

10. Go to the **Assignment** tab of the MobSF app and assign the groups corresponding to `Maintainer` and `Viewer` roles.

<img width="566" alt="Screenshot 2024-05-22 at 8 36 41 PM" src="https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/f419add2-66a5-47b7-93da-349a5d958cd2">


11. Now Go to the **Sign On** tab of the created app and copy the `Metadata URL`.
<img width="556" alt="Metadata URL" src="https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/9e193176-1c26-48ba-ad92-54950b050344">



#### MobSF Configuration

1. After you have created the Okta MobSF app integration, Set the environment variable `MOBSF_IDP_METADATA_URL` to the Okta `Metadata URL`.

2. Run MobSF, and now SSO with Okta is enabled.


### SSO FAQ

#### MobSF behind reverse proxy

When running MobSF behind a reverse proxy such as Nginx, ensure that the actual domain name reaches MobSF by setting headers such as `X-Forwarded-Host`, `X-Forwarded-Port` and
`X-Forwarded-For`.

**Example Nginx settings**

```
location / {
    proxy_set_header        X-Forwarded-Host    $host;
    proxy_set_header        X-Forwarded-Port    443;
    proxy_set_header        X-Forwarded-For     $proxy_add_x_forwarded_for;
    ....
}
```

Alternatively, you can directly set the hostname using the environment variable `MOBSF_SP_HOST`. Example: `MOBSF_SP_HOST=https://mobsf.yourdomain.com`


Errors such as `Invalid dict settings: sp_acs_url_invalid` is an indication that MobSF couldn't find the correct hostname.