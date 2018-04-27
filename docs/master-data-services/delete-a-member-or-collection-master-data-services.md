---
title: 删除成员或集合 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- collections [Master Data Services], deleting
- leaf members [Master Data Services], deleting
- deleting members [Master Data Services]
- members [Master Data Services], deleting
- consolidated members [Master Data Services], deleting
ms.assetid: 519130a7-4226-4d71-9124-d2ee0ce7e5bd
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e5eab65acaac91a255aed5c9fa30e6e0508d8090
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="delete-a-member-or-collection-master-data-services"></a>删除成员或集合 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，当您不再需要某个成员或集合时，可以将其删除。 若要大批量删除成员，可以改用临时表。 有关详细信息，请参阅[导入表中数据 (Master Data Services)](../master-data-services/import-data-from-tables-master-data-services.md)  
  
> [!NOTE]  
>  如果某一成员用作另一个成员的基于域的属性值，则不能删除该成员。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-    您必须有权访问“资源管理器”功能区域。  
  
-   如果要删除成员，你必须至少具有此成员所在的叶模型对象的  “删除”权限。  
  
-   对于集合，您必须对要删除的叶集合对象至少具有 **“更新”** 权限。  
  
### <a name="to-delete-a-member-or-collection"></a>删除成员或集合  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 在  主页上，从“模型”列表中，选择模型。  
  
2.   从“版本”列表中，选择某一版本。  
  
3.  单击 **“资源管理器”**。  
  
4.  若要删除：  
  
    -   叶成员，请从菜单栏中指向 **“实体”** ，然后单击包含该成员的实体的名称。  
  
    -   合并成员，请从菜单栏中指向 **“层次结构”** ，然后单击包含该成员的层次结构的名称。 接着单击包含成员的层次结构中的节点。  
  
    -   集合，请从菜单栏中指向 **“集合”** ，然后单击包含该集合的实体的名称。  
  
5.  在网格中，单击要删除的成员或集合所对应的行。  
  
6.  单击 **“删除成员”**、 **“删除”**或 **“删除集合”**。  
  
7.  实体管理员还将会在实体版本中看到用来清除（硬删除）所有软删除成员的菜单选项。  
  
8.  在确认对话框中，单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [重新激活成员或集合 (Master Data Services)](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)   
 [成员 &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [集合 (Master Data Services)](../master-data-services/collections-master-data-services.md)  
  
  
