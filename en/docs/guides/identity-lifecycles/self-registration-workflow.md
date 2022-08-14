# User Self-Registration

You can configure WSO2 Identity Server (WSO2 IS) to allow user self-registration. When this option is enabled, users can self-register from the My Account portal or any of the applications registered with WSO2 IS.

## Set up notifications

WSO2 Identity Server should first be configured to send email notifications to users. Apply the following configurations:

-   [Configure the email sender]({{base_path}}/deploy/configure-email-sending) of WSO2 Identity Server.

    !!! tip
        Typically, the **AccountConfirmation** template is used to send email notifications.

        You can edit and customize the email template. For more information
        on how to do this, see [Customizing Automated
        Emails]({{base_path}}/guides/tenants/customize-automated-mails/).

-   If you have migrated from a previous WSO2 IS version, ensure that
the `IdentityMgtEventListener` with the ` orderId=50 ` is set to
**false** and that the identity listeners with ` orderId=95 ` and `orderId=97 ` are set to **true** in the `<IS_HOME>/repository/conf/deployment.toml ` file.
    
    !!! Note 
        If there are no such entries for `event.default_listener.xxx` in the `deployment.toml` file, you can skip this configuration.
    
    ``` toml
    [event.default_listener.identity_mgt]
    priority= "50"
    enable = false
    [event.default_listener.governance_identity_mgt]
    priority= "95"
    enable = true
    [event.default_listener.governance_identity_store]
    priority= "97"
    enable = true
    ```

## Enable self-registration

Follow the steps given below to enable self-registration:

1.  Sign in to the Management Console.
2.  Go to **Main** > **Identity Providers** -> **Resident** and expand **User Onboarding**.
3.  Expand **Self Registration** and configure the following values:
    
    <!--![user-self-registration]({{base_path}}/assets/img/guides/user-self-registration.png)-->
    
    <table>
    <thead>
    <tr class="header">
    <th>Field</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>User self registration</td>
    <td>Enable self registration.</td>
    </tr>
    <tr class="even">
    <td>Lock user account on creation</td>
    <td>Enable account lock during self registration. The account will be unclocked upon confirmation.</td>
    </tr>
    <tr class="odd">
    <td>Manage notifications sending internally</td>
    <td>
    <p>
    Select to configure WSO2 identity server to send confirmation emails to the user.
    If the client application handles notification sending already, clear it. 
    </p>
    </td>
    </tr>
    <tr class="even">
    <td>Prompt reCaptcha</td>
    <td>Select to enable reCAPTCHA for self-registration. See <a href="{{base_path}}/guides/password-mgt/recaptcha-challenge-question-attempts/">Configuring Google reCAPTCHA for Security-Question Based Password Recovery</a> for more information.</td>
    </tr>
    <tr class="odd">
    <td>User self registration verification link expiry time</td>
    <td><div class="content-wrapper">
    <p>Number of minutes that the confirmation link would be valid. The confirmation link will expire 
    after the specified time has elapsed.</p>
    <div class="admonition note">
    <p class="admonition-title">Note</p>
    <p>Alternatively, you can configure the expiry time from the <code>deployment.toml</code>  file.</p>
    <div class="code panel pdl" style="border-width: 1px;">
    <div class="codeContent panelContent pdl">
    <div class="sourceCode" id="cb1" data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence" data-theme="Confluence" style="brush: java; gutter: false; theme: Confluence"><pre class="sourceCode java"><code class="sourceCode java"><a class="sourceLine" id="cb1-1" title="1">[identity_mgt.user_self_registration]</a>
    <a class="sourceLine" id="cb1-2" title="2">allow_self_registration= true </a>
    <a class="sourceLine" id="cb1-3" title="3">expiry_time="1440"</a></code></pre></div> 
    </div>
    </div></div> 
    </div></td>
    </tr>
    </tbody>
    </table>

4.  If you wish to send an account unlocked email when the user activates the account via the confirmation email, do the following:
    
    1. Go to **Main** > **Identity Providers** > **Resident** and expand **Login Attempts Security**.
    2. Expand **Account Lock** and select **Lock user accounts**.  
               
        !!! info
            Learn more about [account locking]({{base_path}}/guides/identity-lifecycles/lock-accounts-by-failed-login-attempts/).
    
        ![account-locking]({{base_path}}/assets/img/guides/account-locking.png)

Now you have set up self registration. Next, let's see how you can
configure self-registration consent purposes.

## Configure consent purposes

Follow the instructions below to configure self-registration consent
purposes and appropriate user attributes:

1.  Sign in to the Management Console.

2.  Go to **Main** -> **Identity** -> **Identity Providers** -> **Resident** -> **User Onboarding** -> **Self Registration** section. 

3.  Select `Click here` to configure self-registration consent purposes. 

    !!! info
        This displays the **Consent Purposes: SELF-SIGNUP** screen that allows you to add consent purposes.

    ![self-registration]({{base_path}}/assets/img/guides/account-policies.png)   

4.  Click **Add New Purpose** and specify appropriate values for the **Purpose** and **Description**. 

5.  Then, click **Add PII Category** to add the user attributes required for obtaining user consent.

    !!! tip
        You can add one or more user attributes to obtain consent for a particular purpose.
    
    ![user-attributes-for-consent]({{base_path}}/assets/img/guides/user-attributes-for-consent.png) 

6.  If you want consent on a specific user attribute to be mandatory, select the **Mandatory** check box for that attribute.

    !!! tip
        -   When you configure consent purposes for self-registration, the
            attributes that you specify for a particular purposes are the
            only attributes for which users are prompted to provide consent.
        -   If a user attribute is set as **Mandatory**, a user has to
            provide consent for that attribute to proceed with
            self-registration.
        -   If a user does not provide consent for any of the non-mandatory
            attributes, WSO2 Identity Server will not store those
            attributes.

7.  Click **Finish** to complete the registration.

Now you have configured required self-registration purposes and user
attributes for which you require user consent.

Next, you can try out self-registration.

## Try it out

Let's try out self-registration. You can use either the My Account portal or the REST API.

### Use the My Account portal

Let's try to self-register using the My Account portal.

1.  Access the WSO2 Identity Server's [My Account portal]({{base_path}}/guides/my-account/my-account).
2.  Click **Create Account** and then enter the new user's username.

    !!! info "Register Users for a Tenant"
        If you want to self-register to a specific tenant, you need to
        provide the **Username** in the following format:
        `            <USERNAME>@<TENAND_DOMAIN>           `

        For example, if you have a tenant domain as
        `           foo.com          `, the username needs to be
        `           kim@foo.com          `

    ![register-users-for-tenant]({{base_path}}/assets/img/guides/register-users-for-tenant.png) 

3.  Fill in the user details, provide consent to share the requested
    information and then click **Register**.

    !!! Info
        The attributes that show up on the self-sign-up page are WSO2 [local dialect claims]({{base_path}}/guides/dialects/add-claim-mapping/) claims that have the **Supported by Default** configuration enabled. The claims that have the **Mandatory** configuration enabled are indicated as mandatory on the self-sign-up screen as shown above.

        <!--![self-signup-required-claim-config]({{base_path}}/assets/img/guides/self-signup-required-claim-config.png)-->
    
    ![Self sign up form]({{base_path}}/assets/img/guides/self-signup-form.png)
    
4.  Access the user's email and see that the confirmation email is received.

5.  Click **Confirm Registration** in the email or copy the link in the
    email to your browser to confirm the account.  
    
As per the configuration you enabled on WSO2 IS, once you confirm the account, the account will be unlocked.

<!--
!!! info "Want to resend the confirmation email?"

    If you did not receive the confirmation mail or if the mail expired, click the **Re-Send** link to resend the email.  
    
    ![resend-link]({{base_path}}/assets/img/guides/resend-link.png) 

    The email template used to resend the confirmation email notification is the **ResendAccountConfirmation** template.
        
    You can edit and customize the email template. For more information on how to do this, see [Customizing Automated Emails]({{base_path}}/guides/tenants/customize-automated-mails).
-->

### Use the REST API

Let's try to self-register using the Self-Register API. See the [Self-Registration API documentation]({{base_path}}/apis/use-the-self-sign-up-rest-apis) for details on using this API.

**Request**

```curl 
curl -X POST -H "Authorization: Basic <Base64Encoded_username:password>" -H "Content-Type: application/json" -d '{"user": {"username": "<username>","realm": "<user_store>", "password": "<password>","claims": [{"uri": "<claim_URI>","value": "<claim_value>" },{"uri": "<claim_URI2>","value": "<claim_value2>"},{"uri": "<claim_URI3>","value": "<claim_value3>"},{"uri": "<claim_URI4>","value": "<claim_value4>"} ] },"properties": []}' "https://localhost:9443/api/identity/user/v1.0/me"
```

!!! abstract ""
    **Sample Request**
    ```curl
    curl -X POST -H "Authorization: Basic YWRtaW46YWRtaW4=" -H "Content-Type: application/json" -d '{"user": {"username": "kim","realm": "PRIMARY", "password": "Password12!","claims": [{"uri": "http://wso2.org/claims/givenname","value": "kim" },{"uri": "http://wso2.org/claims/emailaddress","value": "kim.anderson@gmail.com"},{"uri": "http://wso2.org/claims/lastname","value": "Anderson"},{"uri": "http://wso2.org/claims/mobile","value": "+947721584558"} ] },"properties": [{"key":"callback","value": "https://localhost:9443/authenticationendpoint/login.do"}]}' "https://localhost:9443/api/identity/user/v1.0/me"
    ```
    ---
    **Sample Response**
    ```curl
    "HTTP/1.1 201 Created"
    ```


!!! info "Related topics"
    - [Guide: Create new user from the Management Console]({{base_path}}/guides/identity-lifecycles/admin-creation-workflow) 
    - [Guide: Invite users to join]({{base_path}}/guides/identity-lifecycles/invitation-workflow) 
    - [Guide: User self-registration]({{base_path}}/guides/identity-lifecycles/self-registration-workflow)
    - [Guide: Lite user registrtion]({{base_path}}/guides/identity-lifecycles/lite-user-registration)
    - [Guide: Bulk import users]({{base_path}}/guides/identity-lifecycles/bulk-import-users)
    - [Guide: Configure reCAPTCHA for user registration]({{base_path}}/guides/identity-lifecycles/configure-recaptcha-for-self-registration)
