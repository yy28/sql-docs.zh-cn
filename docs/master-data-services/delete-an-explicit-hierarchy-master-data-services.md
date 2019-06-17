---
title: 删除显式层次结构 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- explicit hierarchies, deleting
- deleting explicit hierarchies [Master Data Services]
ms.assetid: 4ce177b0-9884-47a2-9cea-212e845dd762
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 27f2da08eb5b1f9f7027d3e9747c7de8cab0ec1b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478203"
---
# <a name="delete-an-explicit-hierarchy-master-data-services"></a>删除显式层次结构 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，当不再需要显式层次结构时可将其删除。  
  
> [!WARNING]  
>  当删除显式层次结构时，还将删除该层次结构中的所有合并成员。 如果您删除某一实体的所有显式层次结构，则还将删除此实体的所有集合，并且不再为显式层次结构和集合启用此实体。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
### <a name="to-delete-an-explicit-hierarchy"></a>删除显式层次结构  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”** 。  
  
2.  在“管理模型”  页上，从网格中选择一个模型，然后单击“实体”  。  
  
3.  在“管理实体”  页上，从网格中选择包含要删除的显式层次结构的实体所在的行。  
  
4.  单击“显式层次结构”  。  
  
5.  在“管理显式层次结构”  页上，单击要删除的显式层次结构。  
  
6.  单击 **“编辑”** 。  
  
7.  在确认对话框中，单击 **“确定”** 。  
  
## <a name="see-also"></a>请参阅  
 [创建显式层次结构 (Master Data Services)](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [显式层次结构 (Master Data Services)](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
