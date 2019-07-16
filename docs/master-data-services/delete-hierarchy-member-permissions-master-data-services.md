---
title: 删除层次结构成员权限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting member permissions [Master Data Services]
- members [Master Data Services], deleting permissions
- permissions [Master Data Services], deleting member permissions
ms.assetid: 7f22d5e2-70c1-422c-99c2-e995a47d812a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bdb6a9b2c7e42406443b802803723fae4c60a7c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906288"
---
# <a name="delete-hierarchy-member-permissions-master-data-services"></a>删除层次结构成员权限 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，删除模型对象权限可以删除已进行的任何分配。  
  
## <a name="prerequisites"></a>系统必备  
 若要执行此过程：  
  
-   您必须有权访问 **“用户和组权限”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
### <a name="to-delete-hierarchy-member-permissions"></a>删除层次结构成员权限  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“用户和组权限”** 。  
  
2.  在 **“用户”** 或 **“组”** 页上，选择要编辑的用户或组所对应的行。  
  
3.  单击 **“编辑所选用户”** 。  
  
4.  单击 **“层次结构成员”** 选项卡。  
  
5.  从 **“模型”** 列表中，选择某一模型。  
  
6.   从“版本”列表中，选择某一版本。  
  
7.  单击 **“编辑”** 。  
  
8.  在“层次结构成员权限”面板中查找具有该权限的树节点。   
  
9. 单击该树节点，然后在上下文菜单中单击“无”。   
  
    > [!NOTE]  
    >  如果权限继承自一个组，则不能从用户删除该权限。 而是必须从该组删除该权限。  
  
10. 单击“保存”  。  
  
## <a name="see-also"></a>请参阅  
 [层次结构成员权限 (Master Data Services)](../master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [分配层次结构成员权限 (Master Data Services)](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
  
