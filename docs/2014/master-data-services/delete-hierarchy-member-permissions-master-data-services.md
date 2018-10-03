---
title: 删除层次结构成员权限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting member permissions [Master Data Services]
- members [Master Data Services], deleting permissions
- permissions [Master Data Services], deleting member permissions
ms.assetid: 7f22d5e2-70c1-422c-99c2-e995a47d812a
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: ca4e921f5bff1f9870b812958baa63df1caedc32
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48093717"
---
# <a name="delete-hierarchy-member-permissions-master-data-services"></a>删除层次结构成员权限 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，删除模型对象权限可以删除已进行的任何分配。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程：  
  
-   您必须有权访问 **“用户和组权限”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
### <a name="to-delete-hierarchy-member-permissions"></a>删除层次结构成员权限  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“用户和组权限”**。  
  
2.  在 **“用户”** 或 **“组”** 页上，选择要编辑的用户或组所对应的行。  
  
3.  单击 **“编辑所选用户”**。  
  
4.  单击 **“层次结构成员”** 选项卡。  
  
5.  从 **“模型”** 列表中，选择某一模型。  
  
6.   从“版本”列表中，选择某一版本。  
  
7.  在中**层次结构成员权限摘要**窗格中，选择你想要删除的权限的行。  
  
8.  单击**删除所选的权限**。  
  
    > [!NOTE]  
    >  如果权限继承自一个组，则不能从用户删除该权限。 而是必须从该组删除该权限。  
  
## <a name="see-also"></a>请参阅  
 [层次结构成员权限&#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [分配层次结构成员权限&#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
  
