---
title: 模型对象权限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Master Data Services], model objects
- models [Master Data Services], object permissions
ms.assetid: fab6335b-4cae-47de-ae7c-6c4743e0680f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 94ad81913071a3bbd4aad33515c27c68b9e268e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482676"
---
# <a name="model-object-permissions-master-data-services"></a>模型对象权限 (Master Data Services)
  模型对象权限是必需的。 这些权限确定用户在用户界面的 **“资源管理器”** 功能区域中可以访问哪些属性。  
  
 例如，如果向某个用户分配对 Product 实体的 **“更新”** 权限，则该用户可以更新 Product 实体的所有属性。 如果分配对单个属性的 **“更新”** 权限，则该用户只能更新该属性。  
  
 若要确定通过每个属性值分配的安全设置，可以将模型对象权限与层次结构成员权限组合，从而确定用户可以访问哪些成员。  
  
 若要让用户访问功能区域以外**资源管理器**，用户必须是模型管理员，这也会涉及分配模型对象权限。 有关详细信息，请参阅 [管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
 模型对象权限是在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 用户界面 (UI) 中分配的，即“模型”  选项卡上的“用户和组权限”  功能区域。在此选项卡上，模型表示为树状结构。 将权限分配给树中的对象时，下面的所有对象都将继承该权限。 可以通过为单个对象分配权限来覆盖此类继承。  
  
 可以将分配**只读**，**更新**，或**拒绝**对模型对象的权限。 如果没有在 **“模型”** 选项卡上分配任何权限，用户就不能在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中查看任何模型或数据。  
  
## <a name="best-practice"></a>最佳实践  
 一般情况下，应将分配**更新**权限的模型对象，然后显式分配对其下对象的权限。 如果没有分配对模型对象之下对象的权限，将继承权限且用户作为管理员。  
  
## <a name="see-also"></a>请参阅  
 [分配模型对象权限 (Master Data Services)](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [模型权限 (Master Data Services)](../../2014/master-data-services/model-permissions-master-data-services.md)   
 [功能区域权限 &#40;Master Data Services&#41;](../../2014/master-data-services/functional-area-permissions-master-data-services.md)   
 [层次结构成员权限 (Master Data Services)](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [如何确定权限 (Master Data Services)](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
