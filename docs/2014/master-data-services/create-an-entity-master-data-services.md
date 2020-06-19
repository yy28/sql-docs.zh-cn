---
title: 创建实体 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], creating
- creating entities [Master Data Services]
ms.assetid: d9a6a51e-7b53-4785-a118-3baeb7ca2d48
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 50cf10a9a745b3a111deb5db6be356d10d204d4a
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971712"
---
# <a name="create-an-entity-master-data-services"></a>创建实体 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，创建一个实体以便包含成员及其属性。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
-   模型必须存在。 有关详细信息，请参阅[创建模型 (Master Data Services)](../../2014/master-data-services/create-a-model-master-data-services.md)。  
  
### <a name="to-create-an-entity"></a>创建实体  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在 **“模型视图”** 页上，从菜单栏中，指向 **“管理”** ，然后单击 **“实体”**。  
  
3.  在 **“实体维护”** 页上，从 **“模型”** 列表中，选择某一模型。  
  
4.  单击 "**添加实体**"。  
  
5.  在 "**实体名称**" 框中，键入实体的名称。  
  
6.  在 "**临时表的名称**" 框中，键入临时表的名称。  
  
    > [!TIP]  
    >  使用模型名称作为临时表名称的一部分，例如 Modelname_Entityname**。 这便于在数据库中查找表。 有关临时表的详细信息，请参阅[数据导入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)。  
  
7.  可选。 选中 **“自动创建代码值”** 复选框。 有关详细信息，请参阅[&#41;&#40;Master Data Services 自动创建代码](../../2014/master-data-services/automatic-code-creation-master-data-services.md)。  
  
8.  从 "**启用显式层次结构和集合**" 列表中，选择下列选项之一：  
  
    -   “否”  。 如果您无需为显式层次结构和集合启用实体，则选择此选项。 您可以根据需要在以后更改此项。  
  
    -   **是** 如果您想要为显式层次结构和集合启用实体，则选择此选项。 在 "**显式层次结构名称**" 框中，键入名称。 还可以选择 "**强制层次结构" （包括所有叶成员**，使显式层次结构成为强制层次结构。  
  
9. 单击 "**保存实体**"。  
  
## <a name="next-steps"></a>后续步骤  
  
-   [创建文本属性 (Master Data Services)](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)  
  
-   [创建基于域的属性 (Master Data Services)](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
-   [创建文件属性 (Master Data Services)](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
## <a name="see-also"></a>另请参阅  
 [实体 &#40;Master Data Services&#41;](../../2014/master-data-services/entities-master-data-services.md)   
 [显式层次结构 &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)   
 [更改实体名称 &#40;Master Data Services&#41;](edit-an-entity-master-data-services.md)   
 [删除实体 (Master Data Services)](../../2014/master-data-services/delete-an-entity-master-data-services.md)  
  
  
