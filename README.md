# MFA, Conditional Access & Identity Protection (In Process)

![MFA - Conditional Access - Identity Protection](https://github.com/0xbythesecond/MFA-Conditional-Access/assets/23303634/c333d377-7103-48b1-91e0-f3cd723683f0)

## Excercise 1: Deploy an Azure VM by using an Azure Resource Manager template

<details>
  
<summary><h3>Task 1: Deploy an Azure VM by using an Azure Resource Manager template</h3></summary>  
  
In this task, you will learn how to deploy an Azure virtual machine (VM) using an Azure Resource Manager (ARM) template.

Sign in to the Azure portal using an account with the Owner or Contributor role in the Azure subscription and the Global Administrator role in the associated Azure AD tenant.

In the Azure portal, use the search bar at the top to search for "Deploy a custom template" or select "Template Deployment (deploy using custom templates)" from the Marketplace list.

On the Custom deployment blade, choose the "Build your own template in the editor" option.

On the Edit template blade, click "Load file" and browse to locate the az-500-04_azuredeploy.json file from the path \Allfiles\Labs\04\. Click "Open" to load the template.

Review the content of the template, which deploys an Azure VM hosting Windows Server 2019 Datacenter.

Click "Save" on the Edit template blade.

Back on the Custom deployment blade, click "Edit parameters."

On the Edit parameters blade, click "Load file" and browse to locate the az-500-04_azuredeploy.parameters.json file from the path \Allfiles\Labs\04\. Click "Open" to load the parameters file.

Review the content of the parameters file, noting the adminUsername and adminPassword values.

Click "Save" on the Edit parameters blade.

Ensure the following settings are configured on the Custom deployment blade (leave others with their default values):

Subscription: Select the name of the Azure subscription you will use for this lab.
Resource group: Click "Create new" and enter the name "AZ500LAB04."
Location: Select "East US."
Vm Size: Select "Standard_D2s_v3."
Vm Name: Enter "az500-04-vm1."
Admin Username: Enter "Student."
Admin Password: Create a unique password that meets the complexity requirements (at least 12 characters long, including 1 lower case character, 1 upper case character, 1 number, and 1 special character). Make a note of the password.
Virtual Network Name: Enter "az500-04-vnet1."
Click "Review + create" and then click "Create." Do not wait for the deployment to complete.

</details>

## Exercise 2: Implement Azure MFA

<details>
  
  <summary><h3>Task 1: Create a new Azure AD tenant</h3></summary>    
  
In this task, you will create a new Azure Active Directory (AD) tenant.

Open the Azure portal and sign in using your Azure account.

In the search bar at the top of the portal, type "Azure Active Directory" and select it from the search results.

On the Overview page of your current Azure AD tenant, click "Manage tenants."

On the Tenants page, click "+ Create" to create a new Azure AD tenant.

On the Basics tab of the Create a tenant blade, select "Azure Active Directory" and click "Next: Configuration >."

On the Configuration tab, configure the following settings:

Organization name: Enter "AdatumLab500-04."
Initial domain name: Enter a unique name consisting of a combination of letters and digits.
Country or region: Select "United States."
Note: Record the initial domain name for later use.

Click "Review + Create" and then click "Create" to create the new Azure AD tenant.

Wait for the new tenant to be created. You can monitor the deployment status using the Notification icon in the Azure portal.

</details>  

<details>
  
<summary><h3>Task 2: Activate Azure AD Premium P2 trial</h3></summary>  
  
In this task, you will sign up for the Azure AD Premium P2 free trial.

In the Azure portal, click the Directory + Subscription icon in the toolbar.

In the Directory + Subscription blade, select the newly created tenant "AdatumLab500-04" and click the "Switch" button to set it as the current directory.

Note: If the "AdatumLab500-04" entry doesn't appear, you may need to refresh the browser window.

In the Azure portal, type "Azure Active Directory" in the search bar and select it from the search results. Navigate to the "Licenses" section in the "AdatumLab500-04" Azure AD blade.

On the Licenses | Overview blade, click "All products" in the Manage section, and then click "+ Try / Buy."

On the Activate blade, click "Free Trial" in the Azure AD Premium P2 section, and then click "Activate" to start the trial.

</details>

<details>
  
<summary><h3>Task 3: Create Azure AD users and groups</h3></summary>    

In this task, you will create three Azure AD users: aaduser1 (Global Admin), aaduser2 (user), and aaduser3 (user).

Navigate back to the "AdatumLab500-04" Azure Active Directory blade.

In the Manage section, click "Users" to go to the Users blade.

On the Users blade, click "+ New User" and select "Create new user."

On the New user blade, configure the following settings (leave others with their default values) and click "Create":

User principal name: Enter "aaduser1"
Name: Enter "aaduser1"
Password: Select the option to auto-generate the password and click "Show Password"
Groups: Keep it as "0 groups selected"
Roles: Select "User" and then select "Global administrator"
Usage Location: Select "United States"

  >**Note**: Record the full user name and password for later use.

Repeat steps 3-4 to create two more users:

User principal name: Enter "aaduser2"
Name: Enter "aaduser2"
Password: Select the option to auto-generate the password
Usage Location: Select "United States"

User principal name: Enter "aaduser3"
Name: Enter "aaduser3"
Password: Select the option to auto-generate the password
Usage Location: Select "United States"

  >**Note**: Record the full user names and passwords for aaduser2 and aaduser3.
  
</details>

<details>
  
<summary><h3>Task 4: Assign Azure AD Premium P2 licenses to Azure AD users</h3></summary>  

In this task, you will assign Azure AD Premium P2 licenses to the Azure AD users.

On the Users blade, click the entry representing your user account.

On the user properties blade, click "Edit properties." Verify that the "Usage Location" is set to "United States." If not, set the usage location and click "Save."

Navigate back to the "AdatumLab500-04" Azure Active Directory blade.

In the Manage section, click "Licenses" to go to the Licenses blade.

On the Licenses | Overview blade, click "All products" and select the checkbox for "Azure Active Directory Premium P2." Then click "+ Assign."

On the Assign license blade, click "+ Add users and groups."

On the Users blade, select "aaduser1," "aaduser2," "aaduser3," and your user account, and click "Select."

Back on the Assign licenses blade, click "Assignment options" and ensure all options are enabled.

Click "Review + assign" and then click "Assign."

Sign out from the Azure portal and sign back in using the same account. This step is necessary for the license assignment to take effect.

  >**Note**: At this point, you have assigned Azure AD Premium P2 licenses to all the user accounts.

</details>

<details>
  
  <summary><h3>Task 5: Configure Azure MFA settings</h3></summary>  

In this task, you will configure Azure Multi-Factor Authentication (MFA) settings and enable MFA for aaduser1.

Navigate to the "AdatumLab500-04" Azure Active Directory tenant blade.

In the Manage section, click "Security" to go to the Security blade.

On the Security | Getting started blade, click "Multifactor authentication" in the Manage section.

On the Multi-Factor Authentication | Getting started blade, click the "Additional cloud-based multifactor authentication settings" link.

Note: This will open a new browser tab displaying the Multifactor authentication page.

On the Multifactor authentication page, click the "Service settings" tab and review the verification options. Ensure that "Text message to phone," "Notification through mobile app," and "Verification code from mobile app or hardware token" are enabled. Click "Save" and then click "Close."

Switch to the "Users" tab on the Multifactor authentication page. Click the entry for "aaduser1," click the "Enable" link, and confirm the action when prompted.

Notice that the "Multi-Factor Auth status" column for "aaduser1" is now "Enabled."

Click on "aaduser1" and observe that you also have the "Enforce" option.

Note: Changing the user status from "Enabled" to "Enforced" impacts only legacy Azure AD integrated apps that don't support Azure MFA. Once the status changes to "Enforced," these apps require the use of app passwords.

With the "aaduser1" entry selected, click "Manage user settings" and review the available options.

Click "Cancel" and switch back to the browser tab displaying the Multi-Factor Authentication | Getting started blade in the Azure portal.

In the Settings section, click "Fraud alert."

On the Multi-Factor Authentication | Fraud alert blade, configure the following settings:

Allow users to submit fraud alerts: Set it to "On"
Automatically block users who report fraud: Set it to "On"
Code to report fraud during the initial greeting: Set it to "0"
Click "Save."
Note: At this point, you have enabled MFA for "aaduser1" and set up fraud alert settings.

Navigate back to the "AdatumLab500-04" Azure Active Directory tenant blade.

In the Manage section, click "Properties," then click the "Manage Security defaults" link at the bottom of the blade.

On the "Enable Security Defaults" blade, click "No" to disable security defaults.

Select "My Organization is using Conditional Access" as the reason and click "Save."

Note: Make sure you are signed in to the "AdatumLab500-04" Azure AD tenant with a user account that has the Global Administrator role.

</details>

<details>
  
<summary><h3>Task 6: Validate MFA configuration</h3></summary>  

In this task, you will validate the MFA configuration by testing the sign-in of the "aaduser1" user account.

Open an InPrivate browser window.

Navigate to the Azure portal and sign in using the "aaduser1" user account.

Note: To sign in, you need to provide the fully qualified name of the "aaduser1" user account, including the Azure AD tenant DNS domain name, which you recorded earlier in this lab. The user name should be in the format "aaduser1@<your_tenant_name>.onmicrosoft.com," where "<your_tenant_name>" is the placeholder representing your unique Azure AD tenant name.

When prompted, click "Next" in the "More information required" dialog box.

Note: The browser session will be redirected to the "Additional security verification" page.

On the "Keep your account secure" page, select the "I want to set up a different method" link. In the "Which method would you like to use?" drop-down list, select "Phone," and click "Confirm."

On the "Keep your account secure" page, select your country or region, enter your mobile phone number in the "Enter phone number" field, ensure that the "Text me a code" option is selected, and click "Next."

On the "Keep your account secure" page, enter the code you received via text message on your mobile phone, and click "Next."

On the "Keep your account secure" page, ensure that the verification was successful, and click "Next."

On the "Keep your account secure" page, click "I want to use a different method," select "Email" from the drop-down list, click "Confirm," provide the email address you intend to use, and click "Next." Once you receive the corresponding email, identify the code in the email body, provide it, and then click "Done."

When prompted, change your password. Make sure to record the new password.

Verify that you successfully signed in to the Azure portal.

Sign out as "aaduser1" and close the InPrivate browser window.
  
</details>  
  
## Exercise 3: Implement Azure AD Conditional Access Policies

  <details>
  <summary><h3>Task 1: Configure a conditional access policy</h3></summary>

Navigate to the Azure portal and go to the "AdatumLab500-04" Azure Active Directory tenant blade.

In the Manage section, click on "Security" to access the Security settings.

On the Security | Getting started blade, under the Protect section, click on "Conditional Access."

On the Conditional Access | Policies blade, click the "+ New policy" button and select "Create new policy" from the drop-down list.

On the New blade, configure the following settings:

Name: Enter "AZ500Policy1"
Users and groups: Select "aaduser2" from the list
Cloud apps or actions: Select "Microsoft Azure Management" from the list
Conditions: Leave the default settings for Sign-in risk and Device platforms
Locations: Review the location options without making any changes
Access controls: Under Grant, select the "Require multi-factor authentication" checkbox
Set the "Enable policy" toggle to "On."

Click "Create" to create the policy.
</details>
  
<details>
  <summary><h3>Task 2: Test the conditional access policy</h3></summary>

Open a new InPrivate Microsoft Edge window.

In the InPrivate window, navigate to the Azure portal and sign in using the "aaduser2" user account.

When prompted, click "Next" in the "More information required" dialog box.

Follow the prompts to set up MFA using your preferred method (e.g., phone).

Change your password when prompted and make sure to record the new password.

Verify that you successfully signed in to the Azure portal.

Sign out as "aaduser2" and close the InPrivate browser window.

Navigate back to the "AdatumLab500-04" Azure Active Directory tenant blade.

In the Manage section, click on "Security" to access the Security settings.

On the Security | Getting started blade, under the Protect section, click on "Conditional Access."

On the Conditional Access | Policies blade, locate the "AZ500Policy1" policy, click the ellipsis (...) next to it, and select "Delete." Confirm the deletion when prompted.
  
</details> 

## Exercise 4: Deploy risk-based policies in Conditional Access

<details>
<summary><h3>Task 1: View Azure AD Identity Protection options in the Azure portal</h3></summary>

Sign in to the Azure portal (https://portal.azure.com/) if needed.

Make sure you are signed in to the "AdatumLab500-04" Azure AD tenant with a user account that has the Global Administrator role.

Navigate to the Azure AD tenant settings by clicking on the Azure Active Directory blade.

In the Azure Active Directory blade, under the Security section, click on "Identity Protection."

Explore the options and features available in Azure AD Identity Protection.
  </details>  
  
<details>
  <summary><h3>Task 2: Configure a user risk policy</h3></summary>

In the Azure portal, go to the "AdatumLab500-04" Azure AD tenant blade.

In the Security section, click on "Conditional Access" to access the Conditional Access policies.

Click on "New policy" to create a new policy.

Enter the name "AZ500Policy2" for the policy.

Under Assignments, select the users you want to include and exclude from the policy. For example, include "aaduser2" and "aaduser3" and exclude "aaduser1".

Under Cloud apps or actions, select "All cloud apps" to apply the policy to all applications.

Under Conditions, set Configure User risk to "Yes" and select "High" as the risk level.

Under Access controls, enable "Require multifactor authentication" and "Require password change."

Under Session, select "Sign-in frequency" and ensure "Every time" is enabled.

Set the "Enable policy" toggle to "Report-only" to test the policy.

Click "Create" to create the policy.
  </details>
  
<details>  
  <summary><h3>Task 3: Configure a sign-in risk policy</h3></summary>

In the Conditional Access policies blade, click on "New policy" to create another policy.

Enter the name "AZ500Policy3" for the policy.

Configure the policy assignments, including users to include and exclude.

Under Cloud apps or actions, select "All cloud apps" to apply the policy to all applications.

Under Conditions, set Configure Sign-in risk to "Yes" and select "High" and "Medium" as the risk levels.

Under Access controls, enable "Require multifactor authentication."

Under Session, select "Sign-in frequency" and ensure "Every time" is enabled.

Set the "Enable policy" toggle to "Report-only" to test the policy.

Click "Create" to create the policy.
  </details>
   
<details>
  <summary><h3>Task 4: Simulate risk events against the Azure AD Identity Protection policies</h3></summary>

In the Azure AD Identity Protection blade, go to the "Risk detections" section.

Click on "Simulate risk detections" to simulate risk events for testing.

Follow the prompts to simulate various risk events and observe how the policies respond.
  </details>

<details>
  <summary><h3>Task 5: Review the Azure AD Identity Protection reports</h3></summary>

In the Azure AD Identity Protection blade, navigate to the "Reports" section.

Explore the various reports available, such as risk events, user risk, and sign-in risk.

Review the reports to gain insights into the risk posture of your environment.

</details>
