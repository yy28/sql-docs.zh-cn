---
title: 创建模型管理员 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], creating
ms.assetid: dae17afc-3b39-490e-b51f-2d8da26d429e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0d4a9e07006444cf85a6d453e6dc8e2956d55e78
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971817"
---
# <a name="create-a-model-administrator-master-data-services"></a>创建模型管理员 (Master Data Services)
  在中 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ，当你希望某个组或用户对一个或多个模型中的所有对象具有 "**更新**" 权限时，可以创建模型管理员。  
  
> [!TIP]  
>  为了简化管理，请创建一个 Windows 组或本地组并将其配置为模型管理员。 然后，您可以从该组中添加和删除用户，而无需访问 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-   您必须有权访问 **“用户和组权限”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
### <a name="to-create-a-model-administrator"></a>创建模型管理员  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“用户和组权限”**。  
  
2.  在 **“用户”** 或 **“组”** 页上，选择要编辑的用户或组所对应的行。  
  
3.  单击 **“编辑所选用户”**。  
  
4.  单击 **“模型”** 选项卡。  
  
5.  也可以从 **“模型”** 列表中选择某一模型。  
  
6.  单击 **“编辑”** 。  
  
7.  单击要授予对其权限的模型。  
  
8.  从菜单中选择 "**更新**"。  
  
9. 对希望组或用户成为其管理员的每个模型，完成步骤 7 和 8。  
  
10. 单击“ **保存**”。  
  
## <a name="remarks"></a>注解  
 不要分配对模型对象或层次结构成员的任何其他权限。 如果执行此操作，用户将不再是管理员，并且不能在**资源管理器**之外的任何功能区域中查看模型。  
  
 有一个例外：如果用户对**层次结构 "成员**" 选项卡上的层次结构**根**分配了 "**更新**" 权限，则该用户仍被视为模型管理员。  
  
## <a name="see-also"></a>另请参阅  
 [管理员 &#40;Master Data Services&#41;](administrators-master-data-services.md)   
 [&#40;Master Data Services 分配模型对象权限&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [将层次结构成员权限分配 &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [&#40;Master Data Services 的模型对象权限&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [层次结构成员权限 (Master Data Services)](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
