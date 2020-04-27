---
title: 创建显式层次结构 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating explicit hierarchies [Master Data Services]
- explicit hierarchies, creating
ms.assetid: ba768393-6990-4eda-8cb0-d58cb3cfc2e2
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 5defabecf637a230571a954c306d207b0f1bbcfb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "65483309"
---
# <a name="create-an-explicit-hierarchy-master-data-services"></a>创建显式层次结构 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，在您需要其成员可在任何级别存在的不规则层次结构时，创建显式层次结构。 显式层次结构包含来自单个实体的成员。  
  
 创建显式层次结构后，可以在 **“资源管理器”** 功能区域中为该层次结构添加成员。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
-   必须为显式层次结构和集合启用了实体。 有关详细信息，请参阅为[显式层次结构和集合启用实体 &#40;Master Data Services&#41;](../../2014/master-data-services/enable-an-entity-for-explicit-hierarchies-and-collections-master-data-services.md)。  
  
### <a name="to-create-an-explicit-hierarchy"></a>创建显式层次结构  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在 **“模型视图”** 页上，从菜单栏中，指向 **“管理”** ，然后单击 **“实体”**。  
  
3.  在 **“实体维护”** 页上，从 **“模型”** 列表中，选择某一模型。  
  
4.  为您要为其创建显式层次结构的实体选择行。  
  
5.  单击 **“编辑所选实体”**。  
  
6.  在 "**编辑实体**" 页上的 "**显式层次结构**" 窗格中，单击 "**添加显式层次结构**"。  
  
7.  在 "**添加显式层次结构**" 页上的 "**显式层次结构名称**" 框中，键入层次结构的名称。  
  
8.  也可以取消选中“强制的层次结构”**** 复选框，以便将层次结构创建为非强制的层次结构。 有关层次结构类型的详细信息，请参阅 [显式层次结构 (Master Data Services)](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)。  
  
9. 单击 "**保存层次结构**"。  
  
10. 在 "**编辑实体**" 页上，单击 "**保存实体**"。  
  
## <a name="next-steps"></a>后续步骤  
  
-   [创建合并成员 (Master Data Services)](../../2014/master-data-services/create-a-consolidated-member-master-data-services.md)  
  
-   [在层次结构中移动 &#40;Master Data Services 的成员&#41;](../../2014/master-data-services/move-members-within-a-hierarchy-master-data-services.md)  
  
## <a name="see-also"></a>另请参阅  
 [显式层次结构 &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)   
 [具有显式大写字母 &#40;Master Data Services 的派生层次结构&#41;](../../2014/master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [更改显式层次结构名称 (Master Data Services)](../../2014/master-data-services/change-an-explicit-hierarchy-name-master-data-services.md)  
  
  
