---
title: 向用户和警报管理员授予权限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 166808e1-ada7-48d2-bda8-8f7c017fb3aa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 48311ccaa22878fb5b17be75c3f12c64cb4a67e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109062"
---
# <a name="grant-permissions-to-users-and-alerting-administrators"></a>向用户和警报管理员授予权限
  用户和警报管理员必须首先被授予 SharePoint 权限，然后才能创建、编辑、删除和查看数据警报。 没有用于使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 数据警报功能的特殊权限，你将使用内置的 SharePoint 权限。  
  
 **信息工作者** - 权限必须包括“创建警报”和“查看项”等 SharePoint 权限。 名为“设计”、“参与讨论”、“读取”和“仅查看”的内置 SharePoint 权限级别包括“创建警报”和“查看项”SharePoint 权限。 您还可以创建自定义权限级别，该级别具有支持创建、编辑、运行和查看数据警报的用户所需的权限。  
  
 **警报管理员** - 权限必须包括“管理警报”SharePoint 权限。 默认情况下，对于使用“工作组网站”站点模板创建的站点，只有“完全控制”权限级别包括此权限。 如果您使用其他站点模板，您将看到不同的默认 SharePoint 组列表。 您可以将“管理警报”权限添加到内置权限级别之一，或者创建具有支持查看和删除数据警报的警报管理员所需权限的自定义权限级别。  
  
 若要了解有关 SharePoint 权限的详细信息，请参阅 [用户权限和权限级别 (SharePoint Server 2010)](https://technet.microsoft.com/library/cc721640.aspx)。  
  
### <a name="to-grant-permissions"></a>授予权限  
  
1.  转到要授予权限的 SharePoint 站点。  
  
2.  在工具栏上，单击 **“网站操作”** ，然后单击 **“网站权限”** 。  
  
     如果未看到此选项，则表明您没有向他人授予权限所需的足够权限。  
  
3.  单击 **“授予权限”** 。  
  
4.  在“用户/组”中，键入要授予权限的用户名、组名或电子邮件地址  。  
  
5.  选择 **“向 SharePoint 组添加用户”** 或 **“直接授予用户权限”** 选项。 根据您是选择 **“向 SharePoint 组添加用户”** 还是选择 **“直接授予用户权限”** ，执行下列操作之一：  
  
    -   如果选择了“向 SharePoint 组添加用户”，则在下拉列表中选择某一权限级别  。  
  
    -   如果您选择了 **“直接授予用户权限”** ，则选择某一权限级别。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [在 SharePoint 站点上为报表服务器项设置权限（SharePoint 集成模式下的 Reporting Services）](security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Reporting Services 数据警报](../ssms/agent/alerts.md)  
  
  
