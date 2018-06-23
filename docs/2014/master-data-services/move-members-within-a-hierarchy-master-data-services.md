---
title: 层次结构 (Master Data Services) 中移动成员 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- hierarchies [Master Data Services], moving members
- explicit hierarchies, moving members
- derived hierarchies, moving members
- members [Master Data Services], moving
ms.assetid: 049c9a15-89c1-478c-8438-028fffc9e187
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: d5e8bf5a041458614422b3c89666ea3ffc9f5a86
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027914"
---
# <a name="move-members-within-a-hierarchy-master-data-services"></a>在层次结构中移动成员 (Master Data Services)
  在[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，在层次结构中移动成员可以更改其位置或父分配。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程：  
  
-    您必须有权访问“资源管理器”功能区域。  
  
-   对于显式层次结构，你必须具有最少**更新**对实体的权限。  
  
-   对于派生层次结构，你必须具有最少**更新**对模型和层次结构中使用任何基于域的属性。  
  
### <a name="to-move-members-within-a-hierarchy"></a>在层次结构中移动成员  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 在  主页上，从“模型”列表中，选择模型。  
  
2.   从“版本”列表中，选择某一版本。  
  
3.  单击 **“资源管理器”**。  
  
4.  从菜单栏中，指向**层次结构**单击*hierarchy_name*。  
  
5.  在**层次结构**窗格中，其中在树结构中显示的层次结构，单击你想要移动的每个成员复选框。  
  
6.  在顶部**层次结构**窗格中，单击**剪切**。  
  
7.  在**层次结构**窗格中，单击你想要移动到成员的成员的复选框。  
  
8.  单击**粘贴**。  
  
    > [!NOTE]  
    >  在派生层次结构中，您只能将成员移到同一个级别。 此外，不能更改成员的排序顺序。  
  
## <a name="see-also"></a>请参阅  
 [通过使用临时过程移动显式层次结构成员&#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)   
 [派生层次结构&#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)   
 [显式层次结构&#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  