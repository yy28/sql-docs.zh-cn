---
title: "备份和还原 Reporting Services SharePoint 服务应用程序 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dfb4ed77-90e5-4273-b690-89a945508ed2
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a4f320a1e806dce3411137abc74f2fe07bab7217
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="backup-and-restore-reporting-services-sharepoint-service-applications"></a>备份和还原 Reporting Services SharePoint 服务应用程序
  本主题说明如何使用 SharePoint 管理中心或 PowerShell 备份和还原 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序。 本主题包含：  
  
-   [限制和局限](#bkmk_Restrictions)  
  
-   [建议](#bkmk_recommendations)  
  
-   [备份服务应用程序](#bkmk_backup)  
  
-   [还原服务应用程序](#bkmk_restore)  
  
##  <a name="bkmk_BeforeYouBegin"></a> 开始之前  
  
###  <a name="bkmk_Restrictions"></a> 限制和局限  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序。 **需要执行其他步骤** ，本主题中介绍了这些步骤。 备份过程当前 **不** 备份无人参与的执行帐户 (UEA) 或对 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 数据库的 Windows 身份验证的加密密钥和凭据。  
  
###  <a name="bkmk_recommendations"></a> 建议  
  
-   启动 SharePoint 备份之前备份加密密钥。 如果您没有备份加密密钥，则在还原服务应用程序之后将无法访问加密的数据。 您将需要删除加密数据。  
  
-   验证您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序是正在使用 UEA 还是 Windows 身份验证来访问数据库。 如果正在使用其中一个，请验证正确的凭据，以便在还原过程之后可以正确地配置该服务应用程序。  
  
-   查看在与备份文件相同的文件夹中创建的 SharePoint 备份日志。 该文件通常名为 **spbackup.log**  
  
##  <a name="bkmk_backup"></a> 备份服务应用程序  
 请按顺序完成下列步骤：  
  
1.  备份加密密钥  
  
2.  备份服务应用程序  
  
3.  验证您的服务应用程序是使用 UEA 还是 Windows 身份验证来访问数据库。 如果确实使用这两种方法，请记下凭据，以便在还原服务应用程序之后，可以使用这些凭据配置服务应用程序。  
  
### <a name="backup-the-encryption-keys-using-central-administration"></a>使用管理中心备份加密密钥  
 有关备份 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 加密密钥的信息，请参阅 [管理 Reporting Services SharePoint 服务应用程序](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)的“加密密钥”部分。  
  
###  <a name="bkmk_centraladmin"></a> 使用 SharePoint 管理中心备份服务应用程序  
 若要备份服务应用程序，请完成以下步骤：  
  
1.  在 SharePoint 管理中心中，单击 **“备份和还原”** 组中的 **“执行备份”** 。  
  
2.  在 **“共享服务”** 节点下，展开 **“共享服务应用程序”** ，然后选择您的服务应用程序。 该应用程序将具有 **“SQL Server Reporting Services 服务应用程序”**类型。  
  
3.  单击“下一步” 。  
  
4.   键入 **“备份位置:”**的路径，然后单击“开始备份”  
  
5.  重复上述过程，而不是选择服务应用程序，展开 **“共享服务代理”** 节点，然后选择服务应用程序代理。 该应用程序将具有 **“SQL Server Reporting Services 服务应用程序代理”**类型。  
  
 有关详细信息，请参阅 SharePoint 文档中的以下主题：  
  
 [SharePoint 文档中的备份服务应用程序 (SharePoint Foundation 2010)](http://msdn.microsoft.com/library/ee748601.aspx)。  
  
 [备份服务应用程序 (SharePoint Server 2010)](http://technet.microsoft.com/library/ee428318.aspx)  
  
### <a name="verify-execution-account-and-database-authentication"></a>验证执行帐户和数据库身份验证  
 **执行帐户** ：验证您的服务应用程序是否正在使用执行帐户：  
  
1.  在 SharePoint 管理中心的 **“应用程序管理”** 组中，单击 **“管理服务应用程序”** 。  
  
2.  单击您的服务应用程序的名称，然后单击 SharePoint 功能区中的 **“管理”** 。  
  
3.  单击 **“执行帐户”**。  
  
4.  如果配置了执行帐户，则当需要还原服务应用程序备份时，您需要知道凭据。 在知道正确的凭据之前，请不要继续执行备份和还原过程。  
  
 **数据库身份验证** ：验证您的服务应用程序是否正在使用 Windows 身份验证来进行数据库身份验证：  
  
1.  在 SharePoint 管理中心的 **“应用程序管理”** 组中，单击 **“管理服务应用程序”** 。  
  
2.  单击您的服务应用程序的名称，然后单击 SharePoint 功能区中的 **“属性”** 。  
  
3.  查看“Reporting Services (SSRS) 服务数据库”部分。  
  
4.  如果配置了 Windows 身份验证，则您需要知道凭据，以便您可以在还原服务应用程序后对其进行配置。 在知道正确的凭据之前，请不要继续执行备份和还原过程。  
  
##  <a name="bkmk_restore"></a> 还原服务应用程序  
 请按顺序完成下列步骤：  
  
1.  还原 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序。  
  
2.  还原加密密钥  
  
3.  如果您的服务应用程序正在使用执行帐户或 Windows 身份验证来访问数据库，请配置凭据。  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>使用 SharePoint 管理中心还原服务应用程序  
  
1.  在 SharePoint 管理中心中，单击 **“备份和还原”** 组中的 **“从备份中还原”** 。  
  
2.  在 **“备份目录位置”** 框中键入指向备份文件的路径，然后单击 **“刷新”**。  
  
3.  从 **“顶部组件”** 列表中选择服务应用程序备份，然后单击 **“下一步”**。  
  
4.  选择您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序，然后单击 **“下一步”**。  
  
5.  在 **“登录名和密码”** 部分中，键入登录名的密码。 登录名框中应填充服务应用程序在备份之前使用的登录名。  
  
6.  单击 **“开始还原”**。  
  
7.  重复上述过程，而不是还原服务应用程序，展开 **“共享服务”** 节点，然后展开 **“共享服务应用程序”** 节点。  
  
 有关详细信息，请参阅 SharePoint 文档中的以下主题：  
  
 [还原服务应用程序 (SharePoint Foundation 2010)](http://msdn.microsoft.com/library/ee748615.aspx)。  
  
 [还原服务应用程序 (SharePoint Server 2010)](https://technet.microsoft.com/library/ee428305.aspx)。  
  
### <a name="restore-the-encryption-keys-using-central-administration"></a>使用管理中心还原加密密钥  
 有关还原 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 加密密钥的信息，请参阅 [管理 Reporting Services SharePoint 服务应用程序](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)的“加密密钥”部分。  
  
### <a name="configure-the-execution-account-and-database-authentication"></a>配置执行帐户和数据库身份验证  
 **执行帐户** ：如果您的服务应用程序正在使用执行帐户，请完成一些步骤对它进行配置：  
  
1.  在 SharePoint 管理中心的 **“应用程序管理”** 组中，单击 **“管理服务应用程序”** 。  
  
2.  单击您的服务应用程序的名称，然后单击 SharePoint 功能区中的 **“管理”** 。  
  
3.  单击 **“执行帐户”**。  
  
4.  键入帐户和密码，然后选中 **“指定执行帐户”** 框。  
  
5.  单击 **“确定”**。  
  
 **数据库身份验证** ：如果您的服务应用程序正在使用 Windows 身份验证来进行数据库身份验证，请完成以下步骤：  
  
1.  在 SharePoint 管理中心的 **“应用程序管理”** 组中，单击 **“管理服务应用程序”** 。  
  
2.  单击您的服务应用程序的名称，然后单击 SharePoint 功能区中的 **“属性”** 。  
  
3.  查看“Reporting Services (SSRS) 服务数据库”部分。  
  
4.  选择 **“Windows 身份验证”**。  
  
5.  键入帐户和密码。 如果适当，请选择 **“用作 Windows 凭据”** 。  
  
6.  单击 **“确定”**  
  
  
