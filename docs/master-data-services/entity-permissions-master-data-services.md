---
title: "实体权限 (Master Data Services) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- entities [Master Data Services], permissions
- permissions [Master Data Services], entities
ms.assetid: 22785062-4faf-46ee-bffa-01cbd6d5a5b3
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 981c150415bed3470b33c29d34ab8e30e0dbf37e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="entity-permissions-master-data-services"></a>实体权限 (Master Data Services)
  实体权限应用到：  
  
-   叶成员和合并成员的所有实体属性，包括 **Name** 和 **Code**属性。  
  
-   实体的所有集合。  
  
-   显式层次结构成员身份和关系。  
  
 具有对实体的权限时，您可以添加和删除实体的成员、其显式层次结构和集合。  
  
> [!NOTE]  
>  这些权限仅应用到用户界面的“资源管理器”功能区域。  
  
|权限|Description|  
|----------------|-----------------|  
|**读取**|用户可以读取成员、属性、层次结构成员身份或集合成员身份。|  
|**创建**|用户可以创建成员，并在创建过程中指定属性值。|  
|**Update**|用户可以更新成员、属性、层次结构成员身份或集合成员身份。|  
|**删除**|用户可以删除成员。|  
|**拒绝**|拒绝对实体的所有访问。|  
  
 读取、创建、更新和删除权限可以彼此合并。 当分配创建、更新和删除权限时，将自动分配读取权限。  
  
## <a name="see-also"></a>另请参阅  
 [分配模型对象权限 &#40;Master Data Services &#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [模型对象权限 &#40;Master Data Services &#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [实体 (Master Data Services)](../master-data-services/entities-master-data-services.md)  
  
  
