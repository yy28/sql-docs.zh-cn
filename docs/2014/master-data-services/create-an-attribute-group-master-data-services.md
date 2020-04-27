---
title: 创建属性组 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services], creating
- creating attribute groups [Master Data Services]
ms.assetid: 798c325e-e8d8-412a-b02e-118f2741d1c7
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c832fe601eb7151e438d7f93c3e39e9b249ea246
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "65483325"
---
# <a name="create-an-attribute-group-master-data-services"></a>创建属性组 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，当您想要在 **“资源管理器”** 网格中的单独选项卡上显示属性时，创建属性组。  
  
> [!NOTE]  
>  创建属性组时，对除创建者之外的所有用户自动隐藏它。 有关使组可见的详细信息，请参阅 [使属性组对用户可见 (Master Data Services)](make-an-attribute-group-visible-to-users-master-data-services.md)选项卡上。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)。  
  
-   必须至少存在一个属性。 有关详细信息，请参阅 [创建文本属性 (Master Data Services)](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)。  
  
### <a name="to-create-an-attribute-group"></a>创建属性组  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在 "**模型视图**" 页上，从菜单栏中指向 "**管理**"，然后单击 "**属性组**"。  
  
3.  从 **“模型”** 列表中，选择某一模型。  
  
4.  从 **“实体”** 列表中，选择某一实体。  
  
5.  单击 **“叶组”**、 **“合并组”** 或 **“集合组”** ，以便为叶成员、合并成员或集合相应创建属性组。  
  
6.  单击 "**添加属性组**"。  
  
7.  在 "**叶组名称**" 框中，键入组的名称。 这是在 "**资源管理器**" 中的选项卡上显示的名称。  
  
    > [!NOTE]  
    >  如果在步骤5中选择了 "**合并组**" 或 "**集合组**"，则此框将分别为 "**合并组名称**" 或 "**集合组名称**"。  
  
8.  单击 **“保存组”**。  
  
9. 展开该组的文件夹。  
  
10. 单击 **“属性”**。  
  
11. 单击 "**编辑所选项**"。  
  
12. 单击 "**可用**" 框中的 "属性"，然后单击 "**添加**" 箭头。 若要全部添加，请单击 **“全部添加”** 箭头。  
  
13. 或者，单击 "**向上**" 和 "**向下**" 箭头可以更改属性的从左到右顺序。  
  
14. 单击“保存”  。  
  
## <a name="next-steps"></a>后续步骤  
  
-   [使属性组对用户可见 (Master Data Services)](make-an-attribute-group-visible-to-users-master-data-services.md)  
  
## <a name="see-also"></a>另请参阅  
 [属性组 &#40;Master Data Services&#41;](../../2014/master-data-services/attribute-groups-master-data-services.md)   
 [属性 &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)   
 [更改属性组名称 &#40;Master Data Services&#41;](../../2014/master-data-services/change-an-attribute-group-name-master-data-services.md)   
 [删除 &#40;Master Data Services 的属性组&#41;](../../2014/master-data-services/delete-an-attribute-group-master-data-services.md)   
 [叶权限 &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)   
 [&#40;Master Data Services 的合并权限&#41;](../../2014/master-data-services/consolidated-permissions-master-data-services.md)  
  
  
