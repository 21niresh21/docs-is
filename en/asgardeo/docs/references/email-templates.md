# Email templates

Asgardeo organizations use default email templates to send email notifications. You can customize the existing templates to match your organization’s requirements using the [Email Templates API](../apis/email-template.md).

## Email templates in Asgardeo

The following is a comprehensive list of email templates that are available in Asgardeo.

!!! note
    Some of the email templates below need to contain URLs. Learn how to generate these URLs in the [URLs in email templates](#urls-in-email-templates) section.

<table>
    <thead>
    <th>Template ID</th>
    <th>Description</th>
    </thead>
    <tbody>
        <tr>
            <td>LiteUserEmailConfirmation<br/><br/>
                ResendLiteUserEmailConfirmation
            </td>
            <td>These emails are generated when you create an account in Asgardeo.</td>
        </tr>
         <tr>
            <td>EmailConfirm<br/><br/>
            AccountConfirmation<br/><br/>
            ResendAccountConfirmation
                </ul>
            </td>
            <td>These emails are sent when a user creates an account in your Asgardeo organization. The email will prompt the user to confirm their account/email </td>
        </tr>
        <tr>
            <td>VerifyEmailOnUpdate</td>
            <td>This email is generated when the user changes the email associated with the account.</td>
        </tr>
        <tr>
            <td>AccountIdRecovery</td>
            <td>This email is generated when a user requests an account ID recovery. </td>
        </tr>
        <tr>
            <td>PasswordReset<br/><br/>
                resendPasswordReset<br/><br/>
                AdminForcedPasswordReset<br/><br/>
                resendAdminForcedPasswordReset<br/><br/>
            </td>
            <td>These emails involve password resets. Depending on whether the user or the administrator initiates the password reset, separate emails are generated. </td>
        </tr>
        <tr>
            <td>initiateRecovery</td>
            <td>This email is generated when a user initiates a password reset using security questions. </td>
        </tr>
        <tr>
            <td>passwordResetSuccess</td>
            <td>This email is generated when a user successfully resets the password. </td>
        </tr>
        <tr>
            <td>AdminForcedPasswordResetWithOTP<br/><br/>
                resendAdminForcedPasswordResetWithOTP
            </td>
            <td>These emails are generated when a user initiates password reset using OTP. The email template can display the OTP using the {{"{{ confirmation-code }}"}} literal.</td>
        </tr>
        <tr>
            <td>TemporaryPassword</td>
            <td>This email is generated when a user is offered a temporary password by the administrator. The email template can display the temporary using the {{"{{ temporary-password }}"}} literal.</td>
        </tr>
        <tr>
            <td>AccountLockAdmin<br/><br/>
                AccountUnlockAdmin<br/><br/>
                AccountEnable<br/><br/>
                AccountDisable<br/><br/>
            </td>
            <td>These emails are generated when a user account is enabled or disabled. </td>
        </tr>
        <tr>
            <td>AccountLockFailedAttempt</td>
            <td>This email is generated when a user account gets locked due to a specified number of failed login attempts. The email template can display the lock duration using the {{"{{ lock-duration }}"}} literal.</td>
        </tr>
        <tr>
            <td>AccountUnlockTimeBased</td>
            <td>This email is generated when a user account is unlocked automatically once the lock duration exceeds.</td>
        </tr>
        <tr>
            <td>UnseenDeviceLogin</td>
            <td>This email is generated when the logs in to using an unrecognized device. The email template can display the time of login using the {{"{{ login-time }}"}} literal.</td>
        </tr>
        <tr>
            <td>idleAccountReminder</td>
            <td>This email is generated when there is no activity in the user account for a specified amount of time.</td>
        </tr>
        <tr>
            <td>TOTP</td>
            <td>This email is generated when the user is given a TOTP to log in. The email template can display the token using the {{"{{ token }}"}} literal</td>
        </tr>
        <tr>
            <td>OneTimePassword</td>
            <td>This email is generated when a user is given a new password to log in. The email template can display the password using the {{"{{ otp-password }}"}} literal</td>
        </tr>
        <tr>
            <td>EmailOTP<br/><br/>
                ResendEmailOTP
            </td>
            <td>These emails are generated when a user is given a one-time password to sign in to an application. The email templates can display the password using the {{"{{ OTPCode }}"}} literal.</td>
        </tr>
        <tr>
            <td>magicLink
            </td>
            <td>This email is generated when a user logs in with a magic link. The application name and the expiry time of the link can be accessed by the literals {{"{{ application-name }}"}}, and {{"{{ expiry-time }}"}} respectively.</td>
        </tr>
        <tr>
            <td>AskPassword<br/><br/>
                resendAskPassword<br/><br/>
            </td>
            <td>These emails are generated when a user is asked to create a password for the newly created account. </td>
        </tr>
        <tr>
            <td>selfSignUpNotify<br/><br/>
                selfSignUpSuccess<br/><br/>
            </td>
            <td>These emails are generated when a user uses self sign-up to register in your organization.</td>
        </tr>
    </tbody>
</table>

## URLs in email templates

Some email templates in Asgardeo should contain URLs which users can click to complete an action. Explained below are those URLs and in which email templates these URLs should contain.

- URL to confirm a user account

    ```ts
    {{ "{{ account.recovery.endpoint-url }}"}}/confirmliteuserregistration.do?confirmation={{ "{{ confirmation-code }}"}}&callback=https://{{ "{{ server.placeholder.websiteHostName }}"}}/early-access
    ```

    This URL is used in the <code>LiteUserEmailConfirmation</code> and <code>ResendLiteUserEmailConfirmation</code> templates.

- URL to confirm an email address

    ```ts
    {{ "{{ account.recovery.endpoint-url }}"}}/confirmregistration.do?confirmation={{ "{{ confirmation-code }}"}}&userstoredomain={{ "{{ userstore-domain }}"}}&username={{ "{{ url:user-name }}" }}
    ```
    This URL is used in the <code>EmailConfirm</code> template.

- URL to confirm a user account

    ```ts
    {{ "{{ account.recovery.endpoint-url }}"}}/confirmregistration.do?confirmation={{ "{{ confirmation-code }}"}}&userstoredomain={{ "{{ userstore-domain }}"}}&username={{ "{{ url:user-name }}"}}&spId={{ "{{ spId }}" }}
    ```
    This URL is used in the <code>AccountConfirmation</code> and <code>ResendAccountConfirmation</code>.

- URL to verify an updated email address.

    ```ts
    {{ "{{ account.recovery.endpoint-url }}"}}/confirmregistration.do?confirmation={{ "{{ confirmation-code }}"}}&userstoredomain={{ "{{ userstore-domain }}"}}&amp;username={{ "{{ url:user-name }}" }}
    ```
    This URL is used in the <code>VerifyEmailOnUpdate</code> template.

- URL to reset a password

    ```ts
    {{ "{{ account.recovery.endpoint-url }}"}}/confirmrecovery.do?confirmation={{ "{{ confirmation-code }}"}}&userstoredomain={{ "{{ userstore-domain }}"}}&username={{ "{{ url:user-name }}"}}&callback={{ "{{ callback }}"}}&spId={{ "{{ spId }}"}}&type=reset
    ```

    This URL is used in the <code>PasswordReset</code> and <code>resendPasswordReset</code> templates.

- URL to reset a password (admin forced)

     ```ts
    {{ "{{ account.recovery.endpoint-url }}"}}/confirmrecovery.do?confirmation={{ "{{ confirmation-code }}"}}&userstoredomain={{ "{{ userstore-domain }}"}}&username={{ "{{ url:user-name }}"}}&type=reset
    ```

    This URL is used in the <code>AdminForcedPasswordReset</code> and <code>resendAdminForcedPasswordReset</code> templates.

- URL to generate a password for a newly created account

    ```ts
    {{ "{{ account.recovery.endpoint-url }}"}}/confirmrecovery.do?confirmation={{ "{{ confirmation-code }}"}}&userstoredomain={{ "{{ userstore-domain }}"}}&username={{ "{{ url:user-name }}"}}&type=invite
    ```

    This URL is used in the <code>AskPassword</code> and <code>resendAskPassword</code> templates.

- URL generate magic links

    ```ts
    {{ "{{ carbon.product-url }}"}}/commonauth?mlt={{ "{{ ma\Token }}" }}
    ```

    This URL is used in the <code>magicLink</code> template.

- URL to prompt the user to access My Account after a user self signs up.

    ```ts
    {{ "{{ authentication.endpoint-url }}"}}?client_id=MY_ACCOUNT&t={{ "{{ tenant-domain }}"}}&relyingParty=MY_ACCOUNT&type=oidc&sp=My+Account&isSaaSApp=true&authenticators=BasicAuthenticator:LOCAL
    ```

    This URL is used in the <code>selfSignUpNotify</code> and <code>selfSignUpSuccess</code> templates.

!!! note
    Be sure to use proper HTML URL encoding when including above URLs in email templates.

## Literals in email templates

Email templates use literals to display dynamic information on email templates. The following are the template literals that are accessible for all email templates in Asgardeo.

### General literals

The following literals about the user are accessible for all email templates.

<table>
    <thead>
        <th>Literal</th>
        <th>Description</th>
    </thead>
    <tbody>
        <tr>
            <td>{{"{{ user-name }}"}}</td>
            <td>Name of the user account.</td>
        <tr>
        <tr>
            <td>{{"{{ user.claim.givenname }}"}}</td>
            <td>Given name of the user.</td>
        <tr>
        <tr>
            <td>{{"{{ userstore-domain }}"}}</td>
            <td>Name of the user store.</td>
        <tr>
        <tr>
            <td>{{"{{ tenant-domain }}"}}</td>
            <td>Name of the organization.</td>
        </tr>
    </tbody>
</table>


### Branding literals

You can use the following literals and customize email templates to fit the branding of your organization.

You can configure the values of these literals from the Asgardeo Console. Refer to the [branding documentation](../guides/branding/configure-ui-branding.md) to learn more.

<table>
    <thead>
        <th>Literal</th>
        <th>Descriprion</th>
    </thead>
    <tbody>
        <tr>
            <td>{{"{{ organization.logo.img }}"}}</td>
            <td>Organization logo</td>
        </tr>
        <tr>
            <td>{{"{{ organization.logo.altText }}"}}</td>
            <td>Logo alternative text</td>
        </tr>
        <tr>
            <td>{{"{{ organization.copyright.text }}"}}</td>
            <td>Copyright text</td>
        </tr>
        <tr>
            <td>{{"{{ organization.support.mail }}"}}</td>
            <td>Support email</td>
        </tr>
        <tr>
            <td>{{"{{ organization.color.primary }}"}}</td>
            <td>Primary color</td>
        </tr>
        <tr>
            <td>{{"{{ organization.color.background }}"}}</td>
            <td>Email background color</td>
        </tr>
        <tr>
            <td>{{"{{ organization.font }}"}}</td>
            <td>Email font</td>
        </tr>
        <tr>
            <td>{{"{{ organization.font.color }}"}}</td>
            <td>Email body font color</td>
        </tr>
        <tr>
            <td>{{"{{ organization.button.font.color }}"}}</td>
            <td>Email button font color</td>
        </tr>
    </tbody>
</table>