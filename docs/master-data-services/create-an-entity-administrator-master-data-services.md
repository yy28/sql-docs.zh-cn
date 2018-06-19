---
title: 创建实体管理员 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 717be1e8-488e-4219-8d1e-ca9084b864cd
caps.latest.revision: 5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a7a779008ec0a069b77801b9f0958ac6e82808a8
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35328931"
---
# <a name="create-an-entity-administrator-master-data-services"></a>创建实体管理员 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，如果你希望某个组或用户具有一个或多个实体中所有对象的所有权限，或者有权批准挂起更改集，请创建一个实体管理员。  
  
> [!TIP]  
>  为了简化管理，请创建一个 Windows 组或本地组并将其配置为实体管理员。 然后，您可以从该组中添加和删除用户，而无需访问 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-   您必须有权访问 **“用户和组权限”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
## <a name="to-create-an-entity-administrator"></a>创建实体管理员  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“用户和组权限”**。  
  
2.  选择要编辑的用户或组所对应的行，然后单击“编辑所选用户” 。  
  
3.  单击  “模型”选项卡，（可选）从  “模型”列表中选择一个模型，然后单击“编辑” 。  
  
4.  单击你想要授予权限的实体，然后单击菜单上的“管理员”  。  
  
5.  对希望组或用户成为其管理员的每个实体，完成步骤 4。  
  
6.  单击 **“保存”**。  
  
## <a name="see-also"></a>另请参阅  
 [管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)   
 [分配模型对象权限 (Master Data Services)](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [分配层次结构成员权限 (Master Data Services)](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [模型对象权限 (Master Data Services)](../master-data-services/model-object-permissions-master-data-services.md)   
 [层次结构成员权限 (Master Data Services)](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
