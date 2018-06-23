---
title: 创建模型管理员 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- administrators [Master Data Services], creating
ms.assetid: dae17afc-3b39-490e-b51f-2d8da26d429e
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 06f5acf3bf8c9c4f8df7282934c99b38480a1bd3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025713"
---
# <a name="create-a-model-administrator-master-data-services"></a>创建模型管理员 (Master Data Services)
  在[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]，当你想要具有的组或用户时创建模型管理员**更新**到一个或多个模型中的所有对象的权限。  
  
> [!TIP]  
>  为了简化管理，请创建一个 Windows 组或本地组并将其配置为模型管理员。 然后，您可以从该组中添加和删除用户，而无需访问 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程：  
  
-   您必须有权访问 **“用户和组权限”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
### <a name="to-create-a-model-administrator"></a>创建模型管理员  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“用户和组权限”**。  
  
2.  在 **“用户”** 或 **“组”** 页上，选择要编辑的用户或组所对应的行。  
  
3.  单击 **“编辑所选用户”**。  
  
4.  单击 **“模型”** 选项卡。  
  
5.  也可以从 **“模型”** 列表中选择某一模型。  
  
6.  单击 **“编辑”**。  
  
7.  单击要授予对其权限的模型。  
  
8.  从菜单中，选择**更新**。  
  
9. 对希望组或用户成为其管理员的每个模型，完成步骤 7 和 8。  
  
10. 单击 **“保存”**。  
  
## <a name="remarks"></a>Remarks  
 不要分配对模型对象或层次结构成员的任何其他权限。 如果这样做，用户不再是管理员且不能查看模型中任何功能区域以外**资源管理器**。  
  
 一种情况例外： 如果用户具有**更新**分配到层次结构权限**根**上**层次结构成员**选项卡上，该用户仍被视为一个模型管理员。  
  
## <a name="see-also"></a>请参阅  
 [管理员&#40;Master Data Services&#41;](administrators-master-data-services.md)   
 [分配模型对象权限&#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [分配层次结构成员权限&#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [模型对象权限&#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [层次结构成员权限&#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  