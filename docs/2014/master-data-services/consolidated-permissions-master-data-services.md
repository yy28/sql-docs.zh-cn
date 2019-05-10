---
title: 合并的权限 (Master Data Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], consolidated member attribute permissions
- consolidated members [Master Data Services], attribute permissions
- permissions [Master Data Services], consolidated members
- members [Master Data Services], consolidated member permissions
ms.assetid: 084055a3-5fd3-43f3-b620-ac6afab42a3d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 86b20b7bbe0e9cf95805dd859c3c85bab60b61a9
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483516"
---
# <a name="consolidated-permissions-master-data-services"></a>合并的权限（主数据服务）
  合并权限应用到实体的所有合并成员的属性值。  
  
 合并的权限仅应用到为显式层次结构和集合启用的实体。  
  
 **说明：**  
  
-   叶权限仅应用到用户界面的 **“资源管理器”** 功能区域。  
  
-   不强制向 **Name** 和 **Code** 属性分配权限。  
  
|权限|Description|  
|----------------|-----------------|  
|**只读**|显示合并成员，但是用户不能添加、删除或更改它们。|  
|**Update**|显示合并成员，用户可以添加、删除和更改它们。|  
|**拒绝**|不显示实体的合并成员。|  
  
## <a name="attribute-permissions"></a>属性权限  
 属性权限应用到该属性用于特定实体的值。 具有仅属性权限的用户不能添加或删除成员。  
  
|权限|Description|  
|----------------|-----------------|  
|**只读**|显示属性，但是用户不能更改属性值。|  
|**Update**|显示属性，用户可以更改属性值。|  
|**拒绝**|不显示属性。<br /><br /> 注意：不能明确拒绝访问 Name 和 Code 属性。|  
  
## <a name="see-also"></a>请参阅  
 [分配模型对象权限 (Master Data Services)](assign-model-object-permissions-master-data-services.md)   
 [叶权限&#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)   
 [模型对象权限 (Master Data Services)](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [成员 &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [属性 (Master Data Services)](../../2014/master-data-services/attributes-master-data-services.md)  
  
  
