---
title: "保护共享的数据源项 |Microsoft 文档"
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
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
- security [Reporting Services], data sources
ms.assetid: 7299e498-0a1a-4821-a22a-5199bb773ce0
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e056f5577c2c569e333f2341060862c06d803f6b
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="secure-shared-data-source-items"></a>保护共享数据源项
  您可以设置共享数据源项的安全性，以允许或禁止对其进行访问。  
  
 如果用户对共享数据源拥有最基本的访问权限（例如，通过“浏览者”角色授予的访问权限）并且还为该用户授予了查看报表本身的权限，则该用户可以查看使用该项的报表的列表。  
  
 拥有其他访问权限的用户（例如，通过“内容管理员”角色授予的访问权限）可以查看和设置共享数据源的属性。  
  
 若要设置安全性，应创建相应的角色分配，以指定对共享数据源拥有访问权限的用户帐户或组帐户。 对共享数据源项具有访问权限的用户可以更改该项的名称、说明、连接字符串或凭据信息。  
  
## <a name="tasks-and-access-to-items"></a>任务以及对项的访问权限  
 在创建角色分配时，请使用包含以下任务的角色来为用户和组分配适当的权限：  
  
|选择此任务|授权用户以下权限|  
|----------------------|---------------------------------|  
|查看数据源|在文件夹层次结构中查看共享数据源项。 如果不包含此任务，则用户将无法查看项，用户可能无法了解数据源是否可用。|  
|管理数据源|查看用于指定名称、说明和连接信息的属性。 此任务还用于在文件夹层次结构中显示共享数据源项。 如果选择此任务，则可以省略“查看数据源”任务。|  
|设置项的安全性|创建和修改控制共享数据源访问权限的角色分配。 此任务必须与“查看数据源”或“管理数据源”任务一起使用。 否则，由于用户无法选择项，此任务将不会发挥任何作用。|  
  
## <a name="see-also"></a>另请参阅  
 [管理报表数据源](../../reporting-services/report-data/manage-report-data-sources.md)   
 [保护文件夹](../../reporting-services/security/secure-folders.md)   
 [保护报表和资源](../../reporting-services/security/secure-reports-and-resources.md)   
 [授予对本机模式报表服务器的权限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [在 Reporting Services 数据源中存储凭据](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
