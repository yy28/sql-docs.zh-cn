---
title: 导出数据 (Master Data Services) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- exporting data [Master Data Services]
- subscription views [Master Data Services]
- subscription views [Master Data Services], about subscription views
ms.assetid: 8b74409a-ea70-45f8-84c7-da6905e4901a
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 656578a35e70b8371056330e0edec69073816687
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026568"
---
# <a name="exporting-data-master-data-services"></a>导出数据 (Master Data Services)
  您可以通过创建订阅视图将 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据导出到订阅系统。 然后，任何订阅系统都可以在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中查看发布的数据。 有关视图的详细信息，请参阅 [视图](../relational-databases/views/views.md)。  
  
## <a name="subscription-view-formats"></a>订阅视图格式  
 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中创建某一视图时，从  提供的一组标准视图格式中进行选择。 可以使用这些格式创建显示以下内容的视图：  
  
-   所有叶成员及其属性。  
  
-   所有合并成员及其属性。  
  
-   所有集合及其属性。  
  
-   显式添加到集合的成员。  
  
-   派生层次结构中的成员，采用父子或级别格式。  
  
-   某一实体的所有显式层次结构中的成员，采用父子或级别格式。  
  
## <a name="subscription-views-can-become-out-of-date"></a>订阅视图可能会过期  
 在您创建针对某一实体或层次结构的订阅视图后，对关联的模型对象的更改不能自动反映在视图中。 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 您可能需要在中重新生成一个订阅视图，以便反映对模型对象的更改。 在对象模型更改时， **“导出”** 页上的 **“已更改”** 列将更新为 **True** 。 **True** 指示您应该编辑订阅视图并且保存它，这将重新生成该视图。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|创建主数据的订阅视图。|[创建订阅视图&#40;Master Data Services&#41;](create-a-subscription-view-to-export-data-master-data-services.md)|  
|删除现有订阅视图。|[删除订阅视图&#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-subscription-view-master-data-services.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [订阅视图格式&#40;Master Data Services&#41;](../../2014/master-data-services/subscription-view-formats-master-data-services.md)  
  
-   [视图](../relational-databases/views/views.md)  
  
  