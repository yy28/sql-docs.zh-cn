---
title: PowerPivot for SharePoint 2013 的最低权限配置示例 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: c1e09e6c-52d3-48ab-8c70-818d5d775087
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b79b9c6662b40b860cfacd85d77b09dbfb04117d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62703245"
---
# <a name="example-of-a-minimum-privilege-configuration-for-powerpivot-for-sharepoint-2013"></a>PowerPivot for SharePoint 2013 最低权限的配置示例
  本主题介绍具有最低权限的 PowerPivot for SharePoint 2013 配置示例。 该配置将不同的帐户用于三个组件中的每个组件，并且每个帐户都具有最低的权限级别。  
  
## <a name="summary-of-accounts"></a>帐户摘要  
 PowerPivot for SharePoint 2013 支持使用 Network Service 帐户来用于 Analysis Services 服务帐户。 Network Service 帐户不是针对 SharePoint 2010 的支持的方案。 有关服务帐户的详细信息，请参阅[配置 Windows 服务帐户和权限](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)(https://msdn.microsoft.com/library/ms143504.aspx)。  
  
 下表总结了在此最低权限配置示例中使用的三个帐户。  
  
|范围|“属性”|  
|-----------|----------|  
|SharePoint 管理员帐户|**SPAdmin**|  
|SharePoint 场帐户|**SPFarm**|  
|Analysis Services 服务帐户|**SPsvc**|  
  
### <a name="the-sharepoint-administrator-account-spadmin"></a>SharePoint 管理员帐户 (SpAdmin)  
 **SPAdmin** 是您用来安装和配置场的域帐户。 它是用于运行 SharePoint 配置向导以及适用于 SharePoint 2013 的 PowerPivot 配置工具的帐户**SPAdmin**帐户是唯一要求本地管理员权限的帐户。 在运行 PowerPivot 配置工具时之前, 授予**SPAdmin**帐户 SharePoint 在其中创建内容和配置数据库的 SQL Server 数据库实例的权限。 若要在最低权限情况下配置 SPAdmin 帐户，该帐户应该是角色 **securityadmin** 和 **dbcreator**的成员。  
  
### <a name="the-farm-account-spfarm"></a>场帐户 (SPFarm)  
 **SPFarm** 是 SharePoint Timer 服务以及用于管理中心的 Web 应用程序用来访问 SharePoint 内容数据库的域帐户。 该帐户无需是本地管理员。 SharePoint 配置向导在后端 SQL Server 数据库中授予正确的最低权限。最低 SQL Server 权限配置是角色 **securityadmin** 和 **dbcreator**中的成员身份。  
  
### <a name="the-service-account-for-powerpivot-service-spsvc"></a>用于 PowerPivot 服务的服务帐户 (SPsvc)  
 如果在运行 PowerPivot 配置工具前未配置新的 SharePoint 场，则默认情况下 PowerPivot 配置工具将创建以下内容：  
  
-   PowerPivot 服务应用程序。  
  
-   Excel Services 应用程序。  
  
-   安全存储区应用程序。  
  
 PowerPivot 配置工具将配置默认的应用程序池中的所有三个服务应用程序。 该应用程序池通常配置为以 SPFarm 帐户运行，该帐户有权访问服务帐户不需要的许多资源。为使环境成为最低权限环境，将新的域帐户配置为由相应的应用程序池和 Web 应用程序使用。  
  
 **创建要用作 SharePoint 服务帐户的新的域帐户 SPsvc：**  
  
1.  在 SharePoint 管理中心内，单击**安全**。  
  
2.  单击**配置服务帐户**  
  
3.  单击**注册新的托管帐户**。  
  
 **SPSvc** 帐户没有本地管理员权限，并且 SPsvc 在 SharePoint 数据库中将不具有任何权限。 SPsvc 要求的仅有的权限就是针对 Analysis Services 的 PowerPivot 实例的管理权限。  
  
 **将相应的应用程序池配置为使用 SPsvc 帐户：**  
  
1.  在 SharePoint 管理中心内，单击**安全**。  
  
2.  单击**服务帐户配置**。  
  
3.  选择 PowerPivot 服务应用程序使用的服务应用程序池。 然后选择 SPSvc 帐户。  
  
 **授予对具有 PowerShell 的 Web 应用程序的访问权限：**  
  
1.  使用管理员权限运行 SharePoint 2013 Management Shell。  
  
2.  运行以下 PowerShell 代码：  
  
    ```  
    $webApp = Get-SPWebApplication "http://<servername>"  
    $webApp.GrantAccessToProcessIdentity("DOMAIN\<ServiceAccountName>")  
  
    ```  
  
  
