---
title: 在层次结构中移动成员（Master Data Services） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Master Data Services], moving members
- explicit hierarchies, moving members
- derived hierarchies, moving members
- members [Master Data Services], moving
ms.assetid: 049c9a15-89c1-478c-8438-028fffc9e187
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 58b39d2dc660fd51d1ba21308ff056874a239731
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66054091"
---
# <a name="move-members-within-a-hierarchy-master-data-services"></a>在层次结构中移动成员 (Master Data Services)
  在[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，在层次结构中移动成员可以更改其位置或父分配。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   **** 您必须有权访问“资源管理器”功能区域。  
  
-   对于显式层次结构，你必须对该实体至少具有 "**更新**" 权限。  
  
-   对于派生层次结构，您必须对模型以及在层次结构中使用的任何基于域的属性进行最低**更新**。  
  
### <a name="to-move-members-within-a-hierarchy"></a>在层次结构中移动成员  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 在 **** 主页上，从“模型”列表中，选择模型。  
  
2.  **** 从“版本”列表中，选择某一版本。  
  
3.  单击 **“资源管理器”**。  
  
4.  从菜单栏中，指向 "**层次结构**"，然后单击 " *hierarchy_name*"。  
  
5.  在层次**结构窗格中**，层次结构显示为树结构，单击要移动的每个成员所对应的复选框。  
  
6.  在**层次结构**窗格的顶部，单击 "**剪切**"。  
  
7.  在 "**层次结构**" 窗格中，单击要将成员移动到的成员的复选框。  
  
8.  单击 "**粘贴**"。  
  
    > [!NOTE]  
    >  在派生层次结构中，您只能将成员移到同一个级别。 此外，不能更改成员的排序顺序。  
  
## <a name="see-also"></a>另请参阅  
 [使用 &#40;Master Data Services 的临时过程移动显式层次结构成员&#41;](add-update-and-delete-data-master-data-services.md)   
 [派生层次结构 &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)   
 [显式层次结构 (Master Data Services)](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
