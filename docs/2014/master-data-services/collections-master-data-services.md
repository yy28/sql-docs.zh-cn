---
title: 集合 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services]
- collections [Master Data Services], about collections
ms.assetid: 5aa1d1e0-b4e5-4897-8e74-01dcf418df73
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0dbf84d6fd3253a3b4d945693090fdad00d077ab
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483547"
---
# <a name="collections-master-data-services"></a>集合 (Master Data Services)
  集合是一组来自单个实体的叶成员和合并成员。 不需要完整层次结构并且想要查看不同的成员分组以便进行报告或分析时，或者需要创建分类时，使用集合。  
  
## <a name="what-collections-contain"></a>集合包含的内容  
 集合不限制可以包含的成员数或成员类型，只要这些成员在同一个实体中即可。 集合可以包含来自多个强制性显式层次结构和非强制性显式层次结构的叶成员和合并成员。  
  
 创建集合时，创建的不是分层结构，而是成员的平面列表。 从层次结构中选择某个节点并将其添加到集合时，您所选的合并成员是唯一添加到集合的成员。  
  
 集合还可以包含其他集合。 可以使用集合的集合来创建分类。  
  
 创建集合时，您将自动作为所有者列出。 如果您是管理员，则可以根据需要为您的集合创建其他属性。  
  
> [!NOTE]  
>  在创建集合前，必须为显式层次结构启用了实体。 有关详细信息，请参阅[为显式层次结构和集合启用实体&#40;Master Data Services&#41;](enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md)。  
  
## <a name="subscription-views-for-collections"></a>集合的订阅视图  
 显示集合的订阅视图有两种。 **集合属性** 格式显示集合列表以及与集合相关的任何属性（如说明或所有者）。 **“集合”** 格式显示所有集合中的所有成员以及每个成员权重和排序顺序。 有关详细信息，请参阅[导出数据&#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)。  
  
 如果为集合中的特定成员设置了权重值，则这些值在相关订阅视图中可用。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|为显式层次结构和集合启用实体。|[为显式层次结构和集合启用实体&#40;Master Data Services&#41;](enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md)|  
|创建新集合。|[创建集合 (Master Data Services)](../../2014/master-data-services/create-a-collection-master-data-services.md)|  
|向现有集合添加成员。|[将成员添加到集合 (Master Data Services)](../../2014/master-data-services/add-members-to-a-collection-master-data-services.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [显式层次结构 (Master Data Services)](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [将数据导出&#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)  
  
  
