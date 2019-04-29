---
title: 移动成员在层次结构 (Master Data Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Master Data Services], moving members
- explicit hierarchies, moving members
- derived hierarchies, moving members
- members [Master Data Services], moving
ms.assetid: 049c9a15-89c1-478c-8438-028fffc9e187
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 96f3c1232f1124ef5f2cd9e77d89fa06607392c7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62923434"
---
# <a name="move-members-within-a-hierarchy-master-data-services"></a>在层次结构中移动成员 (Master Data Services)
  在[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，在层次结构中移动成员可以更改其位置或父分配。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-    您必须有权访问“资源管理器”功能区域。  
  
-   对于显式层次结构，必须具有最少**更新**对实体的权限。  
  
-   对于派生层次结构，必须具有最少**更新**对模型和层次结构中使用任何基于域的属性。  
  
### <a name="to-move-members-within-a-hierarchy"></a>在层次结构中移动成员  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 在  主页上，从“模型”列表中，选择模型。  
  
2.   从“版本”列表中，选择某一版本。  
  
3.  单击 **“资源管理器”**。  
  
4.  从菜单栏中，指向**层次结构**然后单击*hierarchy_name*。  
  
5.  在中**层次结构**窗格中，其中以树状结构显示层次结构，单击你想要移动的每个成员的复选框。  
  
6.  在顶部**层次结构**窗格中，单击**剪切**。  
  
7.  在中**层次结构**窗格中，单击你想要移动到成员的成员的复选框。  
  
8.  单击**粘贴**。  
  
    > [!NOTE]  
    >  在派生层次结构中，您只能将成员移到同一个级别。 此外，不能更改成员的排序顺序。  
  
## <a name="see-also"></a>请参阅  
 [使用临时过程移动显式层次结构成员&#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)   
 [派生层次结构 (Master Data Services)](../../2014/master-data-services/derived-hierarchies-master-data-services.md)   
 [显式层次结构 (Master Data Services)](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
