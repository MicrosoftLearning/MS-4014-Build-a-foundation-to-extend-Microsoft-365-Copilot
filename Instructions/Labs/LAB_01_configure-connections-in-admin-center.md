# Practice Lab 0101: Configure the connections for your Microsoft Graph connector

## WWL Tenants - Terms of Use

If you're being provided with a tenant as a part of an instructor-led training delivery, note that the tenant is made available to support the hands-on labs in the instructor-led training.

Tenants shouldn't be shared or used for purposes outside of hands-on labs. The tenant used in this course is a trial tenant and can't be used or accessed after the class is over and aren't eligible for extension.

Tenants must not be converted to a paid subscription. Tenants obtained as a part of this course remain the property of Microsoft Corporation and we reserve the right to obtain access and repossess at any time.

## Summary

In this lab, you'll use the Microsoft 365 admin center to build a connection to customer files using the Microsoft File Share Connector.

Imagine you are a customer service manager at Contoso, a mid-sized company. Your team has been struggling with response times and overall efficiency when handling customer inquiries. You decide to leverage the Microsoft 365 Admin center to create a FileShare connection that allows your customer service agents to quickly access and reference customer files.

## Exercise 1: Configure the connections in the Microsoft 365 admin center

### Log in to the VM

Your lab-hosting provider provides a password for the MOD Administrator account, which is the default tenant administrator. For security purposes, Microsoft has configured your trial tenant so that all predefined users must change their password at their next sign-in. Log into **LON-CL1** as the local **Administrator** account that was created by your lab hosting provider with the password **Pa55w.rd**.

### Task 1: Grant permissions in the Azure portal

1. Go to the Azure portal and sign in with your admin credentials.
1. Select the dropdown menu icon on the left side of the screen to display the Portal menu. Select** **Microsoft Entra ID -> Manage -> App registrations**.
1. Select **New registration** from the top menu bar. The Register an application page displays. On this page, provide a name for the app; let's name this app _Contoso Fileshare_. Leave the default supported account types option as **Accounts in this organizational directory only (Contoso only - Single tenant).**
1. Select **Register.** Your application is created, and an application ID is assigned to it. You'll use this information when you create your Graph Connector Agent (GCA) in the following steps. Before we create the GCA, however, let's configure the necessary settings.

The next step is to grant permissions for the Graph connector agent:

1. Select **Manage -> API Permissions** option from the left-menu.
1. Select **Add a permission -> Microsoft - > Graph, Application -> Permissions**, and allow permissions to the following APIs:

    - ExternalItem.ReadWrite.All
    - ExternalConnection.ReadWrite.OwnedBy
    - Directory.Read.All

1. Select the **Add permissions** button.
1. Select **Grant admin consent for [TenantName]** and confirm by selecting **Yes**.

### Task 2: Install the GCA

1. Download the [Graph connector agent] (https://www.microsoft.com/en-us/download/details.aspx?id=104045). Select the **Download** button.
1. Open the GcaInstaller_3.1.1.0.msi file and follow the prompts in the Setup wizard.
1. Sign in and Register (sign in with the admin name and password) the GCA.
1. Open the Graph Connector Agent Installation app by selecting the icon in the bottom tool bar of the screen.
1. Register the GCA. Name this agent **ContosoFiles**.
1. Select the Azure portal Microsoft Edge tab (Should read **Contoso Fileshare - Microsoft Azure**), navigate to the **Overview** screen and copy the **Application (client) ID**. Paste it into the GCA installation app.

Next, you need to set a Client Secret for this app in the Azure portal.

1. Return to the Azure portal edge tab and navigate to **Certificates & secrets**.
1. Select **+ new client secret.** Add a **Description** by entering **Contoso Files**.

> [!IMPORTANT]
> Copy the value to the clipboard - the value won't be shown next time you're in the screen.

1. Return to the Graph connector agent app and paste the value into the Application password (client secret) field of the GCA installer app.
1. Select **Register.**
1. Close the Installer app.

### Task 3: Open the Microsoft admin center

1. Open a new Microsoft Edge browser tab. In your Microsoft Edge browser, go to the **Microsoft 365 Home** page by entering the following URL in the address bar: **<https://portal.office.com>**
1. In the **Sign in** dialog box, enter the **Administrative Username** provided by your lab hosting provider for your Microsoft 365 trial tenant. The username should be in the form of **<admin@xxxxxZZZZZZ.onmicrosoft.com>**, where xxxxxZZZZZZ is the tenant prefix assigned by your lab hosting provider. Select **Next**.

**Note:** In the lab instructions that appear in your Virtual Machine lab environment, your lab hosting provider may allow you to select a **Type text** (or equivalent) button next to resource data such as usernames, passwords, PowerShell commands, and other data that must be entered throughout the course of these labs. Other lab hosting providers may provide an alternative method, such as the ability to copy and paste in the information. Take advantage of this functionality to save yourself from having to manually enter the information.

1. In the **Enter password** dialog box, enter the predefined **Administrative Password** provided by your lab hosting provider and then select **Sign in**.
1. Your lab hosting provider may or may not have configured the Admin account to require a new password at sign-in. If they did, then an **Update your password** dialog box appears. Enter the **Administrative Password** provided by your lab hosting provider in the **Current password** field, and then enter the New Administrative Password in the **New password** and **Confirm password** fields and select **Sign in**.
1. The **Welcome to Microsoft 365** page appears in your Microsoft Edge browser in the **Home | Microsoft 365** tab. This page is the MOD Administrator's Microsoft 365 home page.
1. On the **Welcome to Microsoft 365** page, in the list of application icons that appear in the navigation pane, select **Admin**; this action opens the **Microsoft 365 admin center** in a new browser tab.
1. Select **… Show all** to display the full navigation menu. Select **Settings** -> **Search & intelligence.**
1. On the **Overview** tab that appears, scroll down. Select **Add your first connection** from the **Connectors** box.

From here, a list of available data sources is listed. We're configuring a connection using the File Share connector. This connector allows Microsoft 365 Copilot search to reference customer files within a Copilot search and allows for faster response times and more accurate responses as a customer service agent finds answers.

1. Select **File Share**, then select **Next**.
1. Enter the **Display Name**. The display name is a unique name that is displayed to users. Let's enter **Contoso Files** in the field.
1. Enter the **Folder path.** We have sample files configured at the following directory:

   **C:\Users\Administrator.ADATUM\Documents\Contoso Docs**

This path is the directory where the files are stored.

1. The GCA we created in the previous steps (ContosoFiles) defaults in the **Graph connector agent** field.
1. Select  **Windows** as the Authentication type, then enter the Administrative **Username** and **Password** for Windows authentication.
1. Select the check box to authorize Microsoft to create an index of third-party data in your tenant.
1. Select **Create**.

A success screen appears, and your connection syncs. You can enter the specific type of content, the departments in your organization who may benefit from its use, or examples of workflows in the **Connector description** box. For example:

**This connector contains information contained in the on-premises or on-premises file share server. It includes customer profiles and customer questions that may benefit the support desk in answering customer queries.**
