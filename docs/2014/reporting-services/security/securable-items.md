---
title: 安全对象项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- securable items [Reporting Services]
- roles [Reporting Services], securable items
- security [Reporting Services], securable items listed
- role-based security [Reporting Services], securable items
ms.assetid: 27f58d4c-5c7b-4947-af5b-0f1fa60faf5f
caps.latest.revision: 44
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 10755bd374698ba0f62aa278cb14cb7feec38983
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125794"
---
# <a name="securable-items"></a>安全对象
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用基于角色的安全性来控制对报表服务器上存储的项的访问权限。 通常通过创建一对角色分配来向用户授予对报表服务器的访问权限：  
  
-   在站点级  
  
-   在主文件夹，它是报表服务器文件夹层次结构的根节点  
  
 安全性可在报表服务器文件夹层次结构中继承。 可通过在站点级和主文件夹上创建角色分配来设置权限继承，该继承将扩展到报表服务器上所有项和操作。  
  
 您可以通过为各个项定义安全性来覆盖权限继承。 可以单独保护的项包括：  
  
-   文件夹  
  
-   报表  
  
-   报表模型  
  
-   Resources  
  
-   共享数据源  
  
-   共享数据集  
  
 其他构造（例如计划和订阅）不能明确地定义安全性。 计划和订阅是在报表的安全性之下运行的。  
  
## <a name="item-descriptions"></a>项说明  
 下表列出了安全对象并对其特征进行了说明：  
  
|项|特征|  
|----------|---------------------|  
|文件夹|文件夹的安全性应用于文件夹本身及其包含的项。 主文件夹是文件夹层次结构的根节点。 对这一文件夹设置的安全性为文件夹层次结构中的所有从属文件夹、报表、资源和共享数据源建立了初始安全设置。 有关详细信息，请参阅 [保护文件](secure-folders.md)。<br /><br /> “我的报表”是一种特殊用途的文件夹，通过基于专用角色的隐含角色分配来设置安全性。 有关详细信息，请参阅 [保护我的报表](secure-my-reports.md)。|  
|报表|您可以设置报表和链接报表的安全性，以控制用户可执行的操作的范围，如更改给定报表的属性。<br /><br /> 报表历史记录通过包含相应历史记录的报表来设置安全性。 您不能对报表历史记录中的单个快照设置安全性。<br /><br /> 有关报表安全的详细信息，请参阅 [保护报表和资源](secure-reports-and-resources.md)。|  
|报表模型|您可为整个或部分报表模型指定角色分配。 因为报表模型可能非常大，您可能会需要为映射到机密数据的模型项设置安全性。|  
|Resources|您可以设置资源的安全性，以控制对资源本身及其属性的访问。<br /><br /> 只有独立的资源才能作为单独的项设置安全性。 嵌入到报表中的资源不能独立于报表之外单独设置安全性。<br /><br /> 有关资源安全的详细信息，请参阅 [保护报表和资源](secure-reports-and-resources.md)。|  
|共享数据源|您可以设置共享数据源的安全性，以限制对该项及其属性页的访问。 有关详细信息，请参阅 [保护共享数据源项](secure-shared-data-source-items.md)。|  
|共享数据集|您可以设置共享数据集的安全性，以控制用户可执行的操作的范围，例如查看或更改定义，或者更改给定共享数据集的属性。<br /><br /> 有关详细信息，请参阅 [保护共享数据集项](secure-shared-dataset-items.md)。|  
  
## <a name="see-also"></a>请参阅  
 [授予对本机模式报表服务器的权限](granting-permissions-on-a-native-mode-report-server.md)   
 [创建、删除或修改角色 (Management Studio)](role-definitions-create-delete-or-modify.md)   
 [授予用户对报表服务器的访问权限（报表管理器）](grant-user-access-to-a-report-server.md)   
 [修改或删除角色分配（报表管理器）](role-assignments-modify-or-delete.md)  
  
  