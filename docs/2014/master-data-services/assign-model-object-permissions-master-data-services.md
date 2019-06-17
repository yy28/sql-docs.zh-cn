---
title: 分配模型对象权限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], assigning object permissions
- permissions [Master Data Services], assigning model object permissions
ms.assetid: 4b80148d-2318-415c-9479-28c240e48bcd
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a1477f934dfa8a23fa5498124b74c9a150b24a33
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480075"
---
# <a name="assign-model-object-permissions-master-data-services"></a>分配模型对象权限 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，当您需要授予用户或组在 **的** “资源管理器” [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]功能区域中访问数据的权限时，或者当您需要将用户或组指定为管理员时，可以向模型对象分配权限。  
  
> [!NOTE]  
>  将权限分配给模型时，针对所有其他模型的权限被隐式拒绝。 如果未分配模型对象权限，则用户或组将无法在 **“资源管理器”** 中访问任何数据。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“用户和组权限”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
### <a name="to-assign-model-object-permissions"></a>分配模型对象权限  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“用户和组权限”** 。  
  
2.  在 **“用户”** 或 **“组”** 页上，选择要编辑的用户或组所对应的行。  
  
3.  单击 **“编辑所选用户”** 。  
  
4.  单击 **“模型”** 选项卡。  
  
5.  也可以从 **“模型”** 列表中选择某一模型。  
  
6.  单击 **“编辑”** 。  
  
7.  展开树，单击要向其分配权限的模型对象。  
  
8.  从菜单中选择**只读**，**更新**，或**拒绝**。  
  
9. 单击“保存”  。  
  
## <a name="next-steps"></a>后续步骤  
  
-   （可选）[分配层次结构成员权限 (Master Data Services)](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
## <a name="see-also"></a>请参阅  
 [删除模型对象权限 (Master Data Services)](../../2014/master-data-services/delete-model-object-permissions-master-data-services.md)   
 [模型对象权限 (Master Data Services)](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [创建模型管理员 (Master Data Services)](../../2014/master-data-services/create-a-model-administrator-master-data-services.md)  
  
  
