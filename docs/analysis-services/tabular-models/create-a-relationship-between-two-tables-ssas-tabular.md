---
title: "创建两个表 (SSAS 表格) 之间的关系 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.createrelatdb.f1
- sql13.asvs.bidtoolset.managereldb.f1
ms.assetid: 052d77b7-7922-408a-a200-786016ee4d15
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7580e80413bc84d67ae6cc65c9a6c3d86f3f1603
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="create-a-relationship-between-two-tables-ssas-tabular"></a>创建两个表之间的关系（SSAS 表格）
  如果数据源中的表没有现有关系，或如果添加新表，则可以使用模型设计器中的工具创建新关系。 有关如何在表格模型中使用关系的详细信息，请参阅 [关系（SSAS 表格）](../../analysis-services/tabular-models/relationships-ssas-tabular.md)。  
  
## <a name="create-a-relationship-between-two-tables"></a>创建两个表之间的关系  
  
#### <a name="to-create-a-relationship-between-two-tables-in-diagram-view-click-and-drag"></a>在关系图视图中创建两个表之间的关系（单击并拖动）  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，依次单击 **“模型”** 菜单、 **“模型视图”**和 **“关系图视图”**。  
  
2.  单击（并按住）表中的列，然后将光标拖到相关查找表中的相关查找列上，然后释放光标。 将自动按正确的顺序创建关系。  
  
#### <a name="to-create-a-relationship-between-two-tables-in-diagram-view-right-click"></a>在关系图视图中创建两个表之间的关系（右键单击）  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，依次单击 **“模型”** 菜单、 **“模型视图”**和 **“关系图视图”**。  
  
2.  右键单击表标题或列，然后单击“创建关系”。  
  
3.  在 **“创建关系”** 对话框中，对于 **“表”**单击向下箭头，然后从下拉列表中选择某个表。  
  
     在“一对多”关系中，此表应位于“多”方。  
  
4.  对于 **“列”**，选择包含与 **“相关查找列”**有关的数据的列。 如果您右键单击要创建关系的列，则系统会自动选中该列。  
  
5.  对于 **“相关查找表”**，选择至少有一列数据与您刚为 **“表”**选择的表相关的表。  
  
     在“一对多”关系中，此表应位于“一”方，这表示所选列中的值不包含重复值。 如果尝试按错误的顺序创建关系（一对多而非多对一），将在“相关查找列”字段旁边显示一个图标。 颠倒顺序以创建有效的关系。  
  
6.  对于 **“相关查找列”**，选择一列，此列具有与您为 **“列”**选择的列中值匹配的唯一值。  
  
7.  单击 **“创建”**。  
  
#### <a name="to-create-a-relationship-between-two-tables-in-data-view"></a>在数据视图中创建两个表之间的关系  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，单击 **“表”** 菜单，再单击 **“创建关系”**。  
  
2.  在 **“创建关系”** 对话框中，对于 **“表”**单击向下箭头，然后从下拉列表中选择某个表。  
  
     在“一对多”关系中，此表应位于“多”方。  
  
3.  对于 **“列”**，选择包含与 **“相关查找列”**有关的数据的列。  
  
4.  对于 **“相关查找表”**，选择至少有一列数据与您刚为 **“表”**选择的表相关的表。  
  
     在“一对多”关系中，此表应位于“一”方，这表示所选列中的值不包含重复值。 如果尝试按错误的顺序创建关系（一对多而非多对一），将在“相关查找列”字段旁边显示一个图标。 颠倒顺序以创建有效的关系。  
  
5.  对于 **“相关查找列”**，选择一列，此列具有与您为 **“列”**选择的列中值匹配的唯一值。  
  
6.  单击 **“创建”**。  
  
## <a name="see-also"></a>另请参阅  
 [删除关系（SSAS 表格）](../../analysis-services/tabular-models/delete-relationships-ssas-tabular.md)   
 [关系（SSAS 表格）](../../analysis-services/tabular-models/relationships-ssas-tabular.md)  
  
  
