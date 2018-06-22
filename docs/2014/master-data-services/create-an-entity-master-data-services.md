---
title: 创建实体 (Master Data Services) | Microsoft Docs
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
- entities [Master Data Services], creating
- creating entities [Master Data Services]
ms.assetid: d9a6a51e-7b53-4785-a118-3baeb7ca2d48
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 23e267d78091895e5d0ec899835ce7aa09e8c9d3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015477"
---
# <a name="create-an-entity-master-data-services"></a>创建实体 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，创建一个实体以便包含成员及其属性。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
-   模型必须存在。 有关详细信息，请参阅[创建模型 (Master Data Services)](../../2014/master-data-services/create-a-model-master-data-services.md)。  
  
### <a name="to-create-an-entity"></a>创建实体  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在 **“模型视图”** 页上，从菜单栏中，指向 **“管理”** ，然后单击 **“实体”**。  
  
3.  在 **“实体维护”** 页上，从 **“模型”** 列表中，选择某一模型。  
  
4.  单击**将实体添加**。  
  
5.  在**实体名称**框中，键入实体的名称。  
  
6.  在**临时表的名称**框中，键入临时表的名称。  
  
    > [!TIP]  
    >  使用模型名称作为临时表名称的一部分，例如 Modelname_Entityname。 这便于在数据库中查找表。 有关临时表的详细信息，请参阅[数据导入&#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)。  
  
7.  可选。 选中 **“自动创建代码值”** 复选框。 有关详细信息，请参阅[自动创建代码 (Master Data Services)](../../2014/master-data-services/automatic-code-creation-master-data-services.md)。  
  
8.  从**启用显式层次结构和集合**列表中，选择以下选项之一：  
  
    -   **不**。 如果您无需为显式层次结构和集合启用实体，则选择此选项。 您可以根据需要在以后更改此项。  
  
    -   **是**。 如果您想要为显式层次结构和集合启用实体，则选择此选项。 在**显式层次结构名称**框中，键入一个名称。 （可选） 选择**强制层次结构 (已包括所有叶成员**进行强制的层次结构的显式层次结构。  
  
9. 单击**保存实体**。  
  
## <a name="next-steps"></a>后续步骤  
  
-   [创建文本属性&#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)  
  
-   [创建基于域的属性&#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
-   [创建文件属性&#40;Master Data Services&#41;](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
## <a name="see-also"></a>请参阅  
 [实体&#40;Master Data Services&#41;](../../2014/master-data-services/entities-master-data-services.md)   
 [显式层次结构&#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)   
 [更改实体名称&#40;Master Data Services&#41;](edit-an-entity-master-data-services.md)   
 [删除实体&#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-entity-master-data-services.md)  
  
  