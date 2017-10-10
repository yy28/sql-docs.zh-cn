---
title: "备份和还原 Reporting Services SharePoint 服务应用程序 |Microsoft 文档"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: b6dcd64d6f9662ae592474053e6cc9bbce53a83e
ms.contentlocale: zh-cn
ms.lasthandoff: 10/06/2017

---
# <a name="back-up-and-restore-reporting-services-sharepoint-service-applications"></a>备份和还原 Reporting Services SharePoint 服务应用程序

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

本主题介绍如何备份和还原[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服务应用程序使用 SharePoint 管理中心或 PowerShell。

> [!NOTE]
> 与 SharePoint 的 reporting Services 集成 SQL Server 2016 之后将不再可用。

## <a name="before-you-begin"></a>开始之前

### <a name="limitations-and-restrictions"></a>限制和局限

> [!NOTE]
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服务应用程序可以部分备份和还原使用 SharePoint 备份和还原功能。 **需要执行其他步骤** ，本主题中介绍了这些步骤。 当前备份过程**不**备份加密密钥和无人参与的执行帐户 (UEA) 或 windows 身份验证的凭据[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]数据库。

### <a name="recommendations"></a>建议
  
-   启动 SharePoint 备份之前备份加密密钥。 如果你不备份加密密钥，然后你将无法访问加密的数据，在还原服务应用程序后。 您将需要删除加密数据。  
  
-   验证您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序是正在使用 UEA 还是 Windows 身份验证来访问数据库。 如果正在使用其中一个，请验证正确的凭据，以便在还原过程之后可以正确地配置该服务应用程序。  
  
-   查看为在备份文件所在的文件夹中创建的 SharePoint 备份日志。 该文件通常名为 **spbackup.log**  
  
## <a name="back-up-the-service-application"></a>备份服务应用程序

 请按顺序完成下列步骤：  
  
1.  备份加密密钥  
  
2.  备份服务应用程序  
  
3.  验证您的服务应用程序是使用 UEA 还是 Windows 身份验证来访问数据库。 如果确实使用这两种方法，请记下凭据，以便在还原服务应用程序之后，可以使用这些凭据配置服务应用程序。  

### <a name="back-up-the-encryption-keys-using-sharepoint-central-administration"></a>备份加密密钥使用 SharePoint 管理中心

有关备份 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 加密密钥的信息，请参阅 [管理 Reporting Services SharePoint 服务应用程序](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)的“加密密钥”部分。  

### <a name="back-up-the-service-application-using-sharepoint-central-administration"></a>备份服务应用程序使用 SharePoint 管理中心

若要备份服务应用程序，请完成以下步骤：  
  
1.  在 SharePoint 管理中心中，选择**执行备份**中**备份和还原**组。  
  
2.  在 **“共享服务”** 节点下，展开 **“共享服务应用程序”** ，然后选择您的服务应用程序。 该应用程序将具有 **“SQL Server Reporting Services 服务应用程序”**类型。  
  
3.  选择“下一步” 。  
  
4.  键入的路径**备份位置：**和选择**启动备份**  
  
5.  重复上述过程，而不是选择服务应用程序，展开 **“共享服务代理”** 节点，然后选择服务应用程序代理。 该应用程序将具有 **“SQL Server Reporting Services 服务应用程序代理”**类型。  
  
 有关详细信息，请参阅 SharePoint 文档中的以下主题：  
  
 [SharePoint 文档中的备份服务应用程序 (SharePoint Foundation 2010)](http://msdn.microsoft.com/library/ee748601.aspx)。  
  
 [备份服务应用程序 (SharePoint Server 2010)](http://technet.microsoft.com/library/ee428318.aspx)  
  
### <a name="verify-execution-account-and-database-authentication"></a>验证执行帐户和数据库身份验证

 **执行帐户** ：验证您的服务应用程序是否正在使用执行帐户：  
  
1.  在 SharePoint 管理中心内，选择**管理服务应用程序**中**应用程序管理**组。  
  
2.  选择服务应用程序的名称，然后选择**管理**SharePoint 功能区中。  
  
3.  选择**的执行帐户**。  
  
4.  如果配置了执行帐户，则当需要还原服务应用程序备份时，您需要知道凭据。 在知道正确的凭据之前，请不要继续执行备份和还原过程。  
  
 **数据库身份验证** ：验证您的服务应用程序是否正在使用 Windows 身份验证来进行数据库身份验证：  
  
1.  在 SharePoint 管理中心内，选择**管理服务应用程序**中**应用程序管理**组。  
  
2.  选择服务应用程序的名称，然后选择**属性**SharePoint 功能区中。  
  
3.  查看**Reporting Services (SSRS) 服务数据库**部分。  
  
4.  如果配置了 Windows 身份验证，则您需要知道凭据，以便您可以在还原服务应用程序后对其进行配置。 在知道正确的凭据之前，请不要继续执行备份和还原过程。  
  
## <a name="restore-the-service-application"></a>还原服务应用程序

 请按顺序完成下列步骤：  
  
1.  还原 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序。  
  
2.  还原加密密钥  
  
3.  如果您的服务应用程序正在使用执行帐户或 Windows 身份验证来访问数据库，请配置凭据。  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>还原服务应用程序使用 SharePoint 管理中心
  
1.  在 SharePoint 管理中心中，选择**从备份中还原**中**备份和还原**组。  
  
2.  键入备份文件中的路径**备份目录位置**框中，然后选择**刷新**。  
  
3.  选择从你服务应用程序备份**顶部组件**列表，然后选择**下一步**。  
  
4.  选择你[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]应用程序，然后选择**下一步**。  
  
5.  在 **“登录名和密码”** 部分中，键入登录名的密码。 登录名框中应填充服务应用程序已在备份之前使用向上的登录名。  
  
6.  选择**启动还原**。  
  
7.  重复上述过程，而不是还原服务应用程序，展开 **“共享服务”** 节点，然后展开 **“共享服务应用程序”** 节点。  
  
 有关详细信息，请参阅 SharePoint 文档中的以下主题：  
  
 [还原服务应用程序 (SharePoint Foundation 2010)](http://msdn.microsoft.com/library/ee748615.aspx)。  
  
 [还原服务应用程序 (SharePoint Server 2010)](https://technet.microsoft.com/library/ee428305.aspx)。  

### <a name="restore-the-encryption-keys-using-sharepoint-central-administration"></a>还原加密密钥使用 SharePoint 管理中心

 有关还原 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 加密密钥的信息，请参阅 [管理 Reporting Services SharePoint 服务应用程序](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)的“加密密钥”部分。  

### <a name="configure-the-execution-account-and-database-authentication"></a>配置执行帐户和数据库身份验证

 **执行帐户** ：如果您的服务应用程序正在使用执行帐户，请完成一些步骤对它进行配置：  
  
1.  在 SharePoint 管理中心内，选择**管理服务应用程序**中**应用程序管理**组。  
  
2.  选择服务应用程序的名称，然后选择**管理**SharePoint 功能区中。  
  
3.  选择**的执行帐户**。  
  
4.  键入帐户和密码，然后选中 **“指定执行帐户”** 框。  
  
5.  选择“确定”。  
  
 **数据库身份验证** ：如果您的服务应用程序正在使用 Windows 身份验证来进行数据库身份验证，请完成以下步骤：  
  
1.  在 SharePoint 管理中心中，选择**管理服务应用程序**中**应用程序管理**组。  
  
2.  选择服务应用程序的名称，然后选择**属性**SharePoint 功能区中。  
  
3.  查看**Reporting Services (SSRS) 服务数据库**部分。  
  
4.  选择 **“Windows 身份验证”**。  
  
5.  键入帐户和密码。 如果适当，请选择 **“用作 Windows 凭据”** 。  
  
6.  选择**确定**

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
