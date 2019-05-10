---
title: 创建基于域的属性 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- domain-based attributes [Master Data Services], creating
- creating domain-based attributes [Master Data Services]
- attributes [Master Data Services], creating domain-based attributes
ms.assetid: 11c31c9f-e6cc-47b7-b76a-d691f84c93c6
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f0760ef2d2a29540b126235d6328af1fbfad39ce
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483421"
---
# <a name="create-a-domain-based-attribute-master-data-services"></a>创建基于域的属性 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，创建基于域的属性以便使用来自某一实体的成员填充属性值。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
-   要用作属性值的源的实体必须存在。 例如，若要基于 Color 实体创建基于域的属性，您必须首先创建 Color 实体。 有关详细信息，请参阅[创建实体 (Master Data Services)](../../2014/master-data-services/create-an-entity-master-data-services.md)。  
  
-   要为其创建属性的实体必须存在。 有关详细信息，请参阅[创建实体 (Master Data Services)](../../2014/master-data-services/create-an-entity-master-data-services.md)。  
  
### <a name="to-create-a-domain-based-attribute"></a>创建基于域的属性  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在 **“模型视图”** 页上，从菜单栏中，指向 **“管理”** ，然后单击 **“实体”**。  
  
3.  在 **“实体维护”** 页上，从 **“模型”** 列表中，选择某一模型。  
  
4.  为您要为其创建属性的实体选择行。  
  
5.  单击 **“编辑所选实体”**。  
  
6.  在 **“编辑实体”** 页上：  
  
    -   如果属性是针对叶成员的，则在 **“叶成员属性”** 窗格中，单击 **“添加叶属性”**。  
  
    -   如果属性是针对合并成员的，则在 **“合并成员属性”** 窗格中，单击 **“添加合并属性”**。  
  
    -   如果属性是针对集合的，则在 **“集合属性”** 窗格中，单击 **“添加集合属性”**。  
  
7.  上**添加属性**页上，选择**基于域的**选项。  
  
8.  在 **“名称”** 框中，键入属性的名称。 该名称不必与您用于属性值的源的实体名称相同。  
  
9. 在 **“显示像素宽度”** 框中，键入要在 **“资源管理器”** 网格中显示的属性列的宽度。  
  
10. 从**实体**列表中，选择要用于填充属性值的实体。  
  
11. 可选。 选择 **Enable change tracking** 可以跟踪对属性值的更改。 有关详细信息，请参阅[向更改跟踪组添加属性 (Master Data Services)](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)。  
  
12. 单击 **“保存属性”**。  
  
13. 在 **“实体维护”** 页上，单击 **“保存实体”**。  
  
## <a name="see-also"></a>请参阅  
 [基于域的属性 (Master Data Services)](../../2014/master-data-services/domain-based-attributes-master-data-services.md)   
 [创建派生层次结构 (Master Data Services)](../../2014/master-data-services/create-a-derived-hierarchy-master-data-services.md)   
 [更改属性名称&#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [删除属性 (Master Data Services)](../../2014/master-data-services/delete-an-attribute-master-data-services.md)  
  
  
