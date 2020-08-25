---
title: Windows Virtual Desktop Sandbox - Azure
description: How to set up Windows Sandbox for Windows Virtual Desktop.
author: guscatal
ms.topic: how-to
ms.date: 08/24/2020
ms.author: guscatal
manager: costinh
---
# Setup Windows Sandbox in Windows Virtual Desktop

> [!IMPORTANT]
> Windows Sandbox for WVD is currently in public preview 
> This preview version is provided without a service level agreement, and we don't recommend using it for production workloads. Certain features might not be supported or might have constrained capabilities.
> For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This topic will walk you through how to publish Windows Sandbox for your users in a Windows Virtual Desktop environment.

## Requirements

Before you get started, here's what you need to configureWindows Sandbox in Windows Virtual Desktop:

- Access to the Windows Insider portal to obtain the version of Windows 10 multi-user with support for the Windows Sandbox in WVD.
- A functioning Windows Virtual Desktop deployment. To learn how to deploy Windows Virtual Desktop (classic), see [Create a tenant in Windows Virtual Desktop](./virtual-desktop-fall-2019/tenant-setup-azure-active-directory.md). To learn how to deploy Windows Virtual Desktop with Azure Resource Manager integration, see [Create a host pool with the Azure portal](./create-host-pools-azure-marketplace.md).

## Get the OS image

If you're a member of the Windows Insider program, you have the option to use the Windows Insider portal instead. You'll need a build after October 1st, 2020.

### Get the OS image from the Azure portal

To get the OS image from the Azure portal:

1. Open the [Azure portal](https://portal.azure.com) and sign in.

2. Go to **Create a virtual machine**.

3. In the **Basic** tab, select **Windows 10 enterprise multi-session, version 2009**.

4. Follow the rest of the instructions to finish creating the virtual machine.

### Get the OS image from the Windows Insider portal

To get the OS image from the Windows Insider Portal:

1. Open the [Windows Insider portal](https://www.microsoft.com/software-download/windowsinsiderpreviewadvanced?wa=wsignin1.0) and sign in.

     >[!NOTE]
     >You must be member of the Windows Insider program to access the Windows Insider portal. To learn more about the Windows Insider program, check out our [Windows Insider documentation](/windows-insider/at-home/).

2. Scroll down to the **Select edition** section and select **Windows 10 Insider Preview Enterprise (FAST) – Build 19041** or later.

3. Select **Confirm**, then select the language you wish to use, and then select **Confirm** again.

     >[!NOTE]
     >At the moment, English is the only language that has been tested with the feature. You can select other languages, but they may not display as intended.

4. When the download link is generated, select the **64-bit Download** and save it to your local hard disk.

## Prepare the VHD image for Azure

Next, you'll need to create a master VHD image. If you haven't created your master VHD image yet, go to [Prepare and customize a master VHD image](set-up-customize-master-image.md) and follow the instructions there.

After you've created your master VHD image, you must install Windows Sandbox feature. To install it enter the following commands:

```cmd
rem Install Windows Sandbox Feature

dism /online /Enable-Feature /FeatureName:Containers-DisposableClientVM 

```

>[!NOTE]
>This change will require that you restart the virtual machine.

Next, prepare the VM VHD for Azure and upload the resulting VHD disk to Azure. To learn more, see [Prepare and customize a master VHD image](set-up-customize-master-image.md).

Once you've uploaded the VHD to Azure, create a host pool that's based on this new image by following the instructions in the [Create a host pool by using the Azure Marketplace](create-host-pools-azure-marketplace.md) tutorial.

## Publish Windows Sandbox on your host pool

To publish Windows Sandbox to your host pool, go to the [Manage app groups](manage-app-groups.md) section:

1. Under "Application source" select "File Path"
2. Under "Application path" enter "C:\system32\WindowsSandbox.exe"
3. Enter "Windows Sandbox" in "Application Name"

That's it! Leave the rest of the options defaults. You should now have 

## Next steps

This feature isn't currently supported, but you can ask questions to the community at the [Windows Virtual Desktop TechCommunity](https://techcommunity.microsoft.com/t5/Windows-Virtual-Desktop/bd-p/WindowsVirtualDesktop).

You can also leave feedback for Windows Virtual Desktop at the [Windows Virtual Desktop feedback hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app).
