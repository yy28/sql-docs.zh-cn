---
title: 模型对象权限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- permissions [Master Data Services], model objects
- models [Master Data Services], object permissions
ms.assetid: fab6335b-4cae-47de-ae7c-6c4743e0680f
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e0e6e04de7c7ed4a483585e6a4228682f0e3a354
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014091"
---
# <a name="model-object-permissions-master-data-services"></a>模型对象权限 (Master Data Services)
  模型对象权限是必需的。 这些权限确定用户在用户界面的 **“资源管理器”** 功能区域中可以访问哪些属性。  
  
 例如，如果向某个用户分配对 Product 实体的 **“更新”** 权限，则该用户可以更新 Product 实体的所有属性。 如果分配对单个属性的 **“更新”** 权限，则该用户只能更新该属性。  
  
 若要确定通过每个属性值分配的安全设置，可以将模型对象权限与层次结构成员权限组合，从而确定用户可以访问哪些成员。  
  
 以外的功能区域使用户能够访问**资源管理器**，用户必须是模型管理员，也会涉及分配模型对象权限。 有关详细信息，请参阅[管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
 模型对象权限是在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 用户界面 (UI) 中分配的，即“模型”选项卡上的“用户和组权限”功能区域。在此选项卡上，模型表示为树状结构。 将权限分配给树中的对象时，下面的所有对象都将继承该权限。 可以通过为单个对象分配权限来覆盖此类继承。  
  
 你可以分配**只读**，**更新**，或**拒绝**对模型对象的权限。 如果没有在 **“模型”** 选项卡上分配任何权限，用户就不能在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中查看任何模型或数据。  
  
## <a name="best-practice"></a>最佳实践  
 一般情况下，你应该分配**更新**权限的模型对象，然后对其下对象显式分配权限。 如果没有分配对模型对象之下对象的权限，将继承权限且用户作为管理员。  
  
## <a name="see-also"></a>请参阅  
 [分配模型对象权限&#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [模型权限 &#40;Master Data Services&#41;](../../2014/master-data-services/model-permissions-master-data-services.md)   
 [功能区域权限 &#40;Master Data Services&#41;](../../2014/master-data-services/functional-area-permissions-master-data-services.md)   
 [层次结构成员权限&#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [如何确定权限&#40;Master Data Services&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  