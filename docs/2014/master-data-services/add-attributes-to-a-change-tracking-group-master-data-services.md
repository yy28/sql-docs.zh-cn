---
title: 向更改跟踪组添加属性 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- change tracking groups [Master Data Services]
- attributes [Master Data Services], change tracking groups
- change tracking groups [Master Data Services], adding attributes
ms.assetid: e153eb5f-70ca-4c6f-89d8-1f937ed3917d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e4457412f39b6dbaa86154dc6068527d7b2095d3
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972317"
---
# <a name="add-attributes-to-a-change-tracking-group-master-data-services"></a>向更改跟踪组添加属性 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，在您想要跟踪对属性值的更改时向更改跟踪组添加属性。  
  
> [!NOTE]  
>  在您向更改跟踪组添加属性后，在属性值发生更改时，该属性在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中将标记为“已更改”。 创建业务规则以便基于更改执行操作。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
-   要添加到更改跟踪组的属性必须存在。 有关详细信息，请参阅 [创建文本属性 (Master Data Services)](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)。  
  
### <a name="to-add-attributes-to-a-change-tracking-group"></a>向更改跟踪组添加属性  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在 "**模型资源管理器**" 页上，从菜单栏中指向 "**管理**"，然后单击 "**实体**"。  
  
3.  在 **“实体维护”** 页上，从 **“模型”** 列表中，选择某一模型。  
  
4.  为您要跟踪其属性值的实体选择行。  
  
5.  单击 **“编辑所选实体”**。  
  
6.  在 **“编辑实体”** 页上：  
  
    -   如果该属性是针对叶成员的，则在 "**叶属性**" 窗格中，选择该属性，然后单击 "**编辑叶属性**"。  
  
    -   如果属性是针对合并成员的，则在 "**合并属性**" 窗格中选择该属性，然后单击 "**编辑合并属性**"。  
  
    -   如果该属性是针对集合的，则在 "**集合属性**" 窗格中选择该属性，然后单击 "**编辑集合属性**"。  
  
7.  选中 **“启用更改跟踪”** 复选框。  
  
8.  在 **“更改跟踪组”** 框中，键入该组的编号。  
  
9. 单击 **“保存属性”**。  
  
10. 在 **“实体维护”** 页上，单击 **“保存实体”**。  
  
11. 对于您要在组中包括的所有属性重复此过程。 对于该组中的每个属性，使用相同的更改跟踪组编号。  
  
## <a name="next-steps"></a>后续步骤  
  
-   [基于属性值更改启动操作 (Master Data Services)](../../2014/master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)  
  
## <a name="see-also"></a>另请参阅  
 [Master Data Services 创建文本属性 &#40;&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)   
 [创建基于域的属性 (Master Data Services)](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  
