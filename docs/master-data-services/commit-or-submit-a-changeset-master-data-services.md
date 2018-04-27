---
title: 确认或提交变更集 (Master Data Services) | Microsoft Docs
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
ms.assetid: d323bbac-c8d4-4d2f-a7d2-a597e8b53e2d
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 149519f8072dc783747edb26ce449e4ade290685
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="commit-or-submit-a-changeset-master-data-services"></a>确认提交变更集 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  变更集是主数据的挂起更改的集合。 如果实体的更改不需要管理员审批，则你可以确认变更集。 如果实体的更改需要管理员审批，则你可以提交变更集以供审批。  
  
## <a name="prerequisites"></a>必备条件  
  
-    您必须有权访问“资源管理器”功能区域。 有关详细信息，请参阅[功能区域权限 (Master Data Services)](../master-data-services/functional-area-permissions-master-data-services.md)  
  
-   如果实体的更改不需要管理员审批，仅当你拥有变更集并且变更集状态为打开时，你才可以确认变更集。  
  
-   如果实体的更改需要管理员审批，仅当你拥有变更集并且变更集状态为打开或已拒绝时，你才可以提交变更集以供审批。  
  
## <a name="to-commit-a-local-changeset"></a>确认本地变更集  
 确认选项仅可用于实体管理员尚未启用审批需求的实体上的本地变更集。  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 主页中，选择模型和版本，然后单击“资源管理器” 。  
  
2.  单击“实体”菜单中的某个实体  。  
  
3.  在右窗格中，选择“变更集”，然后双击要确认的变更集。  
  
4.  单击“确认”。  
  
## <a name="to-submit-a-changeset"></a>提交变更集  
 提交选项仅可用在实体管理员启用了审批需求的实体上的变更集上。  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 主页中，选择模型和版本，然后单击“资源管理器” 。  
  
2.  单击“实体”菜单中的某个实体  。  
  
3.  在右窗格中，选择“变更集” ，然后双击要提交的变更集。  
  
4.  单击“提交”。  
  
## <a name="next-steps"></a>Next Steps  
 [批准或拒绝变更集 (Master Data Services)](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>另请参阅  
 [创建变更集 (Master Data Services)](../master-data-services/create-a-changeset-master-data-services.md)   
 [应用并更新变更集 &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [批准或拒绝变更集 (Master Data Services)](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
