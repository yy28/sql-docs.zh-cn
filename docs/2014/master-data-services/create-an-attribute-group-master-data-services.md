---
title: 创建属性组 (Master Data Services) | Microsoft Docs
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
- attribute groups [Master Data Services], creating
- creating attribute groups [Master Data Services]
ms.assetid: 798c325e-e8d8-412a-b02e-118f2741d1c7
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0a063af91090ff2e8d5eb1145bb5968573d04523
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125437"
---
# <a name="create-an-attribute-group-master-data-services"></a>创建属性组 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，当您想要在 **“资源管理器”** 网格中的单独选项卡上显示属性时，创建属性组。  
  
> [!NOTE]  
>  创建属性组时，对除创建者之外的所有用户自动隐藏它。 有关使组可见的详细信息，请参阅[对用户进行属性组可见&#40;Master Data Services&#41;](make-an-attribute-group-visible-to-users-master-data-services.md)。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](../../2014/master-data-services/administrators-master-data-services.md)。  
  
-   必须至少存在一个属性。 有关详细信息，请参阅[创建文本属性 (Master Data Services)](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)。  
  
### <a name="to-create-an-attribute-group"></a>创建属性组  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  上**模型视图**页上，从菜单栏中，指向**管理**单击**属性组**。  
  
3.  从 **“模型”** 列表中，选择某一模型。  
  
4.  从 **“实体”** 列表中，选择某一实体。  
  
5.  单击 **“叶组”**、 **“合并组”** 或 **“集合组”** ，以便为叶成员、合并成员或集合相应创建属性组。  
  
6.  单击**添加属性组**。  
  
7.  在**叶组名称**框中，键入组的名称。 这是在选项卡上显示的名称**资源管理器**。  
  
    > [!NOTE]  
    >  如果你选择**合并组**或**集合组**在步骤 5 中，此框是**合并组名称**或**集合组名称**分别。  
  
8.  单击 **“保存组”**。  
  
9. 展开该组的文件夹。  
  
10. 单击 **“属性”**。  
  
11. 单击**编辑选定的项**。  
  
12. 单击中的特性**可用**框中，单击**添加**箭头。 若要全部添加，请单击 **“全部添加”** 箭头。  
  
13. （可选） 单击**向上**和**下**箭头可以更改特性的左到右的顺序。  
  
14. 单击 **“保存”**。  
  
## <a name="next-steps"></a>后续步骤  
  
-   [使属性组对用户可见&#40;Master Data Services&#41;](make-an-attribute-group-visible-to-users-master-data-services.md)  
  
## <a name="see-also"></a>请参阅  
 [属性组&#40;Master Data Services&#41;](../../2014/master-data-services/attribute-groups-master-data-services.md)   
 [属性&#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)   
 [更改属性组名称 &#40;Master Data Services&#41;](../../2014/master-data-services/change-an-attribute-group-name-master-data-services.md)   
 [删除属性组 &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-attribute-group-master-data-services.md)   
 [叶权限&#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)   
 [合并权限&#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-permissions-master-data-services.md)  
  
  