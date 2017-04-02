---
title: "实体权限 (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "实体 [Master Data Services], 权限"
  - "权限 [Master Data Services], 实体"
ms.assetid: 22785062-4faf-46ee-bffa-01cbd6d5a5b3
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# 实体权限 (Master Data Services)
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
  
## 另请参阅  
 [分配模型对象权限 (Master Data Services)](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [模型对象权限 (Master Data Services)](../master-data-services/model-object-permissions-master-data-services.md)   
 [实体 (Master Data Services)](../master-data-services/entities-master-data-services.md)  
  
  