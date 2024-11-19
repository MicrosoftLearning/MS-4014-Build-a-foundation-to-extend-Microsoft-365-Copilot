# Practice Lab 1: Configure the connections for your Microsoft Graph connector

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

1. Navigate to the Azure portal **https://www.portal.azure.com** and sign in with your Administrative credentials. Do not save the password, and select **Yes** to **Stay signed in?**.
2. On the **Welcome to Microsoft Azure** screen, select **Cancel**.
1. Select the dropdown menu icon on the left side of the screen to display the Portal menu. Select **Microsoft Entra ID -> Manage -> App registrations**.
1. Select **New registration** from the top menu bar. The **Register an application page** displays. On this page, provide a name for the app; let's name this app **Contoso Fileshare**. Leave the default supported account types option as **Accounts in this organizational directory only (Contoso only - Single tenant).** Do not select an optional **Redirect URI**.
1. Select **Register.** Your application is created, and an application ID is assigned to it. You'll use this information when you create your Graph Connector Agent (GCA) in the following steps. Before we create the GCA, however, let's configure the necessary settings.

The next step is to grant permissions for the Graph connector agent in the Azure Portal:

1. Select **Manage -> API Permissions** option from the left-menu.
1. Select **Add a permission -> Microsoft Graph -> Application permissions**, and allow permissions to the following APIs:

    - Directory -> Directory.Read.All
    - ExternalConnection -> ExternalConnection.ReadWrite.OwnedBy
    - ExternalItem -> ExternalItem.ReadWrite.All
      
1. Select the **Add permissions** button.
1. Select **Grant admin consent for Contoso** and confirm by selecting **Yes**.

**Note:** Do not close this Edge browser tab. The following tasks require that you copy and paste information from the Azure portal.

### Task 2: Install the GCA

1. Open a new Microsoft Edge browser tab. Navigate to the following URL to download the Graph Connector Agent: **https://www.microsoft.com/en-us/download/details.aspx?id=104045**. Select the **Download** button. 
1. Open the **GcaInstaller_3.1.1.0.msi** file and follow the prompts in the Setup wizard. 
2. In the **Search** bar at the bottom of the screen, enter **Graph connector agent config** and select the app from the menu when it appears.
3. Allow the app to make changes to the device by selecting **Yes**.
4. Sign in and Register the GCA using the **MOD Administrative** account. A confirmation that authentication is complete appears in the Edge browser. You can close this window.
5. Open the GCA app by selecting the icon at the bottom of the screen.
1. Name this agent **ContosoFiles**.
1. Select the Azure portal Microsoft Edge tab (should read **Contoso Fileshare - Microsoft Azure**), navigate to the **Overview** screen and copy the **Application (client) ID**. Paste it into the GCA installation app.

Next, you need to set a Client Secret for this app in the Azure portal.

1. Return to the Azure portal edge tab and navigate to **Certificates & secrets**.
1. Select **+ New client secret.** Add a **Description** by entering **Contoso Files**. You can leave the expiration field set to the default 180 days.
2. Select **Add**.
3. Copy the **Value** field of the silent secret.
1. Return to the Graph connector agent app and paste the value into the **Application password (client secret)** field of the GCA installer app.
1. Select **Register.**
1. Once the registration is completed, close the Installer app.

### Task 3: Download the resource files from Github

To configure the connector using the GCA, you'll need files that are local to your system. 

1. Open a new Edge browswer and enter **https://github.com/MicrosoftLearning/MS-4014-Build-a-foundation-to-extend-Microsoft-365-Copilot/tree/master/ResourceFiles** in the address bar.
2. Select the first file in the folder, **Contoso Chai Tea market trends 2023.xls** to open it.
3. Select the **elipsis (more file actions)** button at the top-right of the screen, then select **Download**.
4. Repeat step 3 for each of the remaining files.
5. You can close this window once the downloads are complete.
6. Use the file explorer and navigate to the C:\ directory. Create a new folder named **ResourceFiles**.
7. Open a new file explorer window and navigate to the **Download** folder to access the Contoso files you've downloaded from GitHub. Copy these files into the **C:\ResourceFiles** directory.

You'll use these files as the source content for the connection you create in the Microsoft admin center.

### Task 4: Open the Microsoft admin center

1. Open a new Microsoft Edge browser tab. In your Microsoft Edge browser, go to the **Microsoft 365 Home** page by entering the following URL in the address bar: **https://portal.office.com**
1. If you are prompted to sign in, enter the LON-CL1 **Username** and **Password** provided by your lab hosting provider for your Microsoft 365 trial tenant. The username should be in the form of **<admin@xxxxxZZZZZZ.onmicrosoft.com>**, where xxxxxZZZZZZ is the tenant prefix assigned by your lab hosting provider. 
1. The **Welcome to Microsoft 365** page appears in your Microsoft Edge browser in the **Home | Microsoft 365** tab. This page is the MOD Administrator's Microsoft 365 home page.
1. Select **Admin** from the list of application icons that appear in the navigation pane; this action opens the **Microsoft 365 admin center** in a new browser tab.
1. Select **… Show all** to display the full navigation menu. Select **Settings** -> **Search & intelligence.**
1. On the **Overview** tab that appears, scroll down. Select **Add your first connection** from the **Connectors** box.

From here, a list of available data sources is listed. We're configuring a connection using the File Share connector. This connector allows Microsoft 365 Copilot search to reference customer files within a Copilot search and allows for faster response times and more accurate responses as a customer service agent finds answers.

1. Select **File Share**, then select **Next**.
1. Enter the **Display Name**. The display name is a unique name that is displayed to users. Let's enter **Contoso Files** in the field.
1. Enter the **Folder path.** We have sample files configured at the following directory:

   **C:\ResourceFiles**

This path is the directory where the files are stored.

1. Select the GCA we created in the previous steps (ContosoFiles) in the **Graph connector agent** field if it isn't the default option.
1. Select  **Windows** as the Authentication type, then enter the LON-CLI **Username** and **Password** for Windows authentication.
1. Select the check box to authorize Microsoft to create an index of third-party data in your tenant.
1. Select **Create**.  A success screen appears, and your connection begins to sync. You can enter the specific type of content, the departments in your organization who may benefit from its use, or examples of workflows in the **Connector description** box. For example:

    **This connector contains information contained in the on-premises file share server. It includes customer profiles and customer questions that may benefit the support desk in answering customer queries.**
1. Select **Done**. Your connection now appears on the **Search & intelligence** tab of the Microsoft 365 admin center, and can be referenced in your search results or as you build a Microsoft 365 Copilot agent.
