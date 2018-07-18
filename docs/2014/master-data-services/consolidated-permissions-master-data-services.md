---
title: 合并的权限 (Master Data Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], consolidated member attribute permissions
- consolidated members [Master Data Services], attribute permissions
- permissions [Master Data Services], consolidated members
- members [Master Data Services], consolidated member permissions
ms.assetid: 084055a3-5fd3-43f3-b620-ac6afab42a3d
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 45b5b6ac268dda2d0462c1a4ada895efe8f90171
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37283433"
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
|**拒绝**|不显示属性。<br /><br /> 注意：不能明确拒绝对 Name 和 Code 属性的访问权限。|  
  
## <a name="see-also"></a>请参阅  
 [分配模型对象权限&#40;Master Data Services&#41;](assign-model-object-permissions-master-data-services.md)   
 [叶权限&#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)   
 [模型对象权限&#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [成员 &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [属性&#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)  
  
  
