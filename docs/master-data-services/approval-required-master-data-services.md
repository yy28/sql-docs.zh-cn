---
title: "需要审批 (Master Data Services) |Microsoft 文档"
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
ms.assetid: b475a53d-269d-49f3-bb42-965c555f80be
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f73510c38944126f65567dcb0e6a8b97ec2498e0
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="approval-required-master-data-services"></a>需要审批 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，管理员可以将实体设置为“需要审批”。 对此类实体所做的全部更改都需要由一位实体管理员进行审阅和审批。  
  
> [!NOTE]  
>  对叶成员所做的更改需要进行审批。 对弃用的显式层次结构和集合所做的更改不需要进行审批。  
>   
>  由临时表进程所做的更改不需要进行审批。  
>   
>  由业务规则所做的更改不需要进行审批。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   你必须有权访问“系统管理”功能区域  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
-   实体必须存在。 有关详细信息，请参阅[创建实体 (Master Data Services)](../master-data-services/create-an-entity-master-data-services.md)  
  
## <a name="to-enable-approval-required-for-an-entity"></a>为实体启用“需要审批”  
  
1.  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，单击 **“系统管理”**。  
  
2.  在“管理模型”  页上，从网格中选择一个模型，然后单击“实体” 。  
  
3.  在“管理实体”  页上，从网格中选择要为其启用“需要审批”   的实体所在的行。  
  
4.  单击“编辑” ，选择“需要审批” ，然后单击“保存” 。  
  
## <a name="see-also"></a>另请参阅  
 [变更集 (Master Data Services)](../master-data-services/changesets-master-data-services.md)  
  
  
