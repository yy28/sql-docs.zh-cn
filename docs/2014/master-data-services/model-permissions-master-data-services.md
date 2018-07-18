---
title: 模型权限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], permissions
- permissions [Master Data Services], models
ms.assetid: 210f440b-2cc1-4c49-94b1-3a97e2af7bc3
caps.latest.revision: 5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: b83229221afc84634689c70e29311fba7b2c1374
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37289103"
---
# <a name="model-permissions-master-data-services"></a>模型权限 (Master Data Services)
  模型权限应用到模型中存在的所有实体、派生层次结构、显式层次结构和集合。 对于任何单个对象，可以覆盖分配给模型的权限。  
  
> [!NOTE]  
>  如果用户是模型管理员，则在用户界面的所有功能区域显示该模型。 否则，仅在 **“资源管理器”** 功能区域显示该模型。 有关详细信息，请参阅[管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
|权限|Description|  
|----------------|-----------------|  
|**只读**|在中**资源管理器**，将显示模型，但用户不能添加或删除成员，也不能更新属性值、 层次结构成员身份或集合成员身份。|  
|**Update**|在中**资源管理器**，模型将显示并且用户可以添加和删除成员，可以更新属性值、 层次结构成员身份和集合成员身份。|  
|**拒绝**|不显示该模型。|  
  
 将权限分配给模型时，用户将获得对模型的所有版本的访问权限。 无法将权限分配给单独的版本。  
  
## <a name="see-also"></a>请参阅  
 [分配模型对象权限&#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [模型对象权限&#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [实体权限 &#40;Master Data Services&#41;](../../2014/master-data-services/entity-permissions-master-data-services.md)   
 [集合权限 &#40;Master Data Services&#41;](../../2014/master-data-services/collection-permissions-master-data-services.md)  
  
  
