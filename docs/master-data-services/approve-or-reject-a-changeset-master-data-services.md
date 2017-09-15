---
title: "批准或拒绝变更集 (Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 45bd01f9-ae15-4fc5-a2ba-eee565a26ef8
caps.latest.revision: 8
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 849e543ec67ea42dfbed2f8138e244ede56085e5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/07/2017

---
# <a name="approve-or-reject-a-changeset-master-data-services"></a>批准或拒绝变更集 (Master Data Services)
  变更集是主数据的挂起更改的集合。 如果实体更改则需要管理员批准并将变更集提交以供审核，可以查看，然后批准或拒绝该变更集。  
  
## <a name="prerequisites"></a>先决条件  
  
-    您必须有权访问“资源管理器”功能区域。 有关详细信息，请参阅[功能区域权限 (Master Data Services)](../master-data-services/functional-area-permissions-master-data-services.md)。  
  
-   你必须具有实体的管理员权限。  
  
-   实体更改必须经过管理员批准。  
  
-   如果变更集状态为挂起，可以查看，然后批准或拒绝该变更集。  
  
-   不允许用户批准其自身的更改。 如果你是实体管理员，则必须分配辅助管理员来批准你自己的变更集。  
  
## <a name="to-approve-or-reject-a-changeset"></a>批准或拒绝变更集  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 主页中，选择模型和版本，然后单击“资源管理器” 。  
  
2.  单击“实体”菜单中的某个实体  。  
  
3.  在右窗格中，选择“变更集”  ，然后双击你想要批准或拒绝的变更集。  
  
4.  单击“应用”  以应用变更集并查看挂起的更改。  
  
5.  单击“拒绝”  以拒绝变更集并将其发送回所有者。  
  
6.  单击“批准”  以批准变更集。 变更集自动提交。  
  
## <a name="see-also"></a>另请参阅  
 [创建变更集 (Master Data Services)](../master-data-services/create-a-changeset-master-data-services.md)   
 [应用并更新变更集 &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [确认或提交变更 (Master Data Services)](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
  
