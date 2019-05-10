---
title: 层次结构成员权限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members [Master Data Services], permissions
- permissions [Master Data Services], members
ms.assetid: b3880eed-1bf6-4f65-ab23-b08c194cc858
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 371c7c605b5415654c01f3faa66fbd0801202785
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65482956"
---
# <a name="hierarchy-member-permissions-master-data-services"></a>层次结构成员权限 (Master Data Services)
  层次结构成员权限是可选的，仅当您希望某个用户对特定成员具有受限的访问权限时才应使用。 如果您未在 **“层次结构成员”** 选项卡上分配权限，则用户的权限仅基于在 **“模型”** 选项卡上分配的权限。  
  
 在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 用户界面 (UI) 的“层次结构成员”选项卡中的“用户和组权限”功能区域中分配层次结构成员权限。这些权限确定用户在用户界面的 **“资源管理器”** 功能区域中可以访问哪些成员。  
  
 在 **“层次结构成员”** 选项卡上，每个层次结构均表示为一个树形结构。 将权限分配给树中的节点时，所有子节点都将继承该权限，除非在更低级别显式分配权限。  
  
> [!NOTE]  
>  如果向层次结构中的节点分配权限，则处于同一级别或更高级别的其他节点中的所有成员都将被隐式拒绝。  
  
 在 **“资源管理器”** 中，将成员权限应用到显示成员的任何位置。 例如，使用成员**只读**权限是在其所属任何实体、 层次结构和集合以只读的。  
  
 层次结构权限应用于您向其分配权限的模型版本，并应用于版本的任何将来副本。 它们不应用于比您向其分配权限的版本更早的版本。  
  
|权限|Description|  
|----------------|-----------------|  
|**只读**|显示成员，但是用户不能更改它们。 用户也无法在成员所属的任何显式层次结构或集合中移动成员。<br /><br /> 注意：如果将分配**只读**权**根**下的成员**根**是只读的; 但是，在显式层次结构和集合中，用户可以将成员移到**根**，并可以添加到新成员**根**。|  
|**Update**|显示成员，用户可以更改它们。 用户还可以在成员所属的任何显式层次结构或集合中移动成员。|  
|**拒绝**|不显示成员。|  
  
 在 **“层次结构成员”** 选项卡上，分配的权限不立即生效。 应用该权限的频率取决于 **数据库中“系统设置”表的** “成员安全处理间隔设置” [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 。 可以按照[立即应用成员权限 & #40;Master Data Services & #41;](immediately-apply-member-permissions-master-data-services.md)中的以下步骤立即应用成员权限。  
  
> [!NOTE]  
>  不能将层次结构成员权限分配给递归层次结构、具有显式顶端的派生层次结构和具有隐藏级别的层次结构。  
  
## <a name="possible-overlapping-permissions"></a>可能重叠的权限  
 给成员分配权限时，必须解决重叠的权限问题。  
  
### <a name="when-a-member-belongs-to-multiple-hierarchies"></a>成员属于多个层次结构时  
 两个或多个层次结构可以包含同一成员。  
  
-   如果给一个层次结构节点分配**更新**分配权限，另一个**只读**，则在节点中的成员**只读**。  
  
-   如果给一个层次结构节点分配**更新**或**只读**分配权限，另一个节点**拒绝**，则不显示节点中的成员。  
  
## <a name="see-also"></a>请参阅  
 [分配层次结构成员权限 (Master Data Services)](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [如何确定权限 (Master Data Services)](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)   
 [成员 &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [层次结构 (Master Data Services)](../../2014/master-data-services/hierarchies-master-data-services.md)   
 [立即应用成员权限 (Master Data Services)](immediately-apply-member-permissions-master-data-services.md)  
  
  
