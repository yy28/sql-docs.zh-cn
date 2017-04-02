---
title: "集合权限（主数据服务） | Microsoft Docs"
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
  - "集合 [Master Data Services], 权限"
  - "权限 [Master Data Services], 集合"
ms.assetid: 703e1bf5-4b4b-4830-8a5b-f979b09f677d
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# 集合权限（主数据服务）
  集合权限应用到实体的所有集合。 不能将权限授予特定集合，权限应用到所有集合。  
  
> [!NOTE]  
>  这些权限仅应用到用户界面的“资源管理器”功能区域。  
  
|权限|Description|  
|----------------|-----------------|  
|**读取**|用户可以读取集合成员和成员属性。|  
|**创建**|用户可以创建集合成员并分配属性值。|  
|**Update**|用户可以更新集合成员、属性和关系。|  
|**删除**|用户可以删除集合成员。|  
|**拒绝**|拒绝对集合成员的所有访问。|  
  
 读取、创建、更新和删除权限可以合并。 如果已分配创建、更新和删除权限，那么系统会自动分配读取权限。  
  
## 另请参阅  
 [分配模型对象权限 (Master Data Services)](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [集合 (Master Data Services)](../master-data-services/collections-master-data-services.md)   
 [模型对象权限 (Master Data Services)](../master-data-services/model-object-permissions-master-data-services.md)  
  
  