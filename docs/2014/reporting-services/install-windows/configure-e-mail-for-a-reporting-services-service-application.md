---
title: 为 Reporting Services 服务应用程序配置电子邮件（SharePoint 2010 和 SharePoint 2013） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6caa06af68eddfd85cb4f19ab2cfb8dd41bbdd95
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798107"
---
# <a name="configure-e-mail-for-a-reporting-services-service-application-sharepoint-2010-and-sharepoint-2013"></a>为 Reporting Services 服务应用程序配置电子邮件（SharePoint 2010 和 SharePoint 2013）
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 数据警报功能会在电子邮件中发送警报。 若要发送电子邮件，您可能需要配置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序，并可能需要修改该服务应用程序的电子邮件传递扩展插件。 如果您计划将电子邮件传递扩展插件用于 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 订阅功能，则也需要进行电子邮件设置。  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Sharepoint 模式 &#124; sharepoint 2010 和 sharepoint 2013。|  
  
### <a name="to-configure-e-mail-for-the-shared-service"></a>为共享服务配置电子邮件  
  
1.  在 SharePoint 管理中心中，单击 **“应用程序管理”**。  
  
2.  在 **“服务应用程序”** 组中，单击 **“管理服务应用程序”**。  
  
3.  在 **“名称”** 列表中，单击 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序的名称。  
  
4.  在“管理 Reporting Services 应用程序”页上，单击“电子邮件设置”********。  
  
5.  选择 **“使用 SMTP 服务器”**。  
  
6.  在 **“出站 SMTP 服务器”** 框中，键入 SMTP 服务器的名称。  
  
7.  在“发件人地址”框中，键入电子邮件地址****。  
  
     此地址为所有警报电子邮件的发件人。  
  
     **“发件人地址”** 中指定的用户帐户必须是您为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序配置应用程序池时指定的托管帐户。 如果您具有权限，则可以在 SharePoint 管理中心的“服务帐户”页上查看现有托管帐户的列表。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="ntlm-authentication"></a>NTLM 身份验证  
  
1.  如果您的电子邮件环境需要 NTLM 身份验证且不允许匿名访问，则需要修改 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序的电子邮件传递扩展插件配置。 将**SMTPAuthenticate**更改为使用值 "2"。 无法从用户界面更改此值。 以下 PowerShell 脚本示例更新了名为“SSRS_TESTAPPLICATION”的服务应用程序的报表服务器电子邮件传递扩展插件的完全配置。 请注意，此脚本中列出的某些节点（例如“发件人”地址）也可从用户界面进行设置。  
  
    ```powershell
    $app = Get-SPRSServiceApplication | Where {$_.name -like "SSRS_TESTAPPLICATION *"}  
    $emailCfg = Get-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" | Select -ExpandProperty ConfigurationXml
    $emailXml = [xml]$emailCfg
    $emailXml.SelectSingleNode("//SMTPServer").InnerText = "your email server name"  
    $emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
    $emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
    $emailXml.SelectSingleNode("//From").InnerText = "your FROM email address"  
    Set-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
    ```  
  
2.  如果需要验证服务应用程序的名称，请运行**get-sprsserviceapplication** cmdlet。  
  
    ```powershell
    Get-SPRSServiceApplication  
    ```  
  
3.  以下示例将返回名为“SSRS_TESTAPPLICATION”的服务应用程序的电子邮件扩展插件的当前值。  
  
    ```powershell
    $app = get-sprsserviceapplication | Where {$_.name -like "SSRSTEST_APPLICATION*"}  
    Get-SPRSExtension -Identity $app -ExtensionType "Delivery" -Name "Report Server Email" | Select -ExpandProperty ConfigurationXml  
    ```  
  
4.  以下示例将使用名为“SSRS_TESTAPPLICATION”的服务应用程序的电子邮件扩展插件的当前值创建名为“emailconfig.txt”的新文件  
  
    ```powershell
    $app = Get-SPRSServiceApplication | Where {$_.name -like "SSRS_TESTAPPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | Select -ExpandProperty ConfigurationXml | Out-File c:\emailconfig.txt  
    ```
