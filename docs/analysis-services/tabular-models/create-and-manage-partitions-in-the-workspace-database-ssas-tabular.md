---
title: 创建和管理工作区数据库中的分区 |Microsoft 文档
ms.custom: ''
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.asvs.bidtoolset.partitionmgr.f1
ms.assetid: 0b3027d6-652b-4eb3-a197-58b25df65218
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 416181764e71d923a55b6a6dbd0b1448dc619476
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="create-and-manage-partitions-in-the-workspace-database"></a>创建和管理工作区数据库中的分区 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  分区将表分成多个逻辑部分。 然后，可单独处理（刷新）每个分区，也可与其他分区并行处理每个分区。 分区可以提高大型数据库的可扩展性和可管理性。 默认情况下，每个表都具有一个包含所有列的分区。 本主题中的任务说明如何创建和管理使用的模型工作区数据库中的分区**分区管理器**中的对话框[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
 在将模型部署到其他 Analysis Services 实例后，数据库管理员可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在（已部署）模型中创建和管理分区。 有关详细信息，请参阅[创建和管理表格模型分区](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)。  
  
> [!NOTE]  
>  使用“分区管理器”对话框不能在模型工作区数据库中合并分区。 通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，仅能在已部署的模型中合并分区。  
  
## <a name="tasks"></a>“任务”  
 若要创建和管理分区，您将使用 **“分区管理器”** 对话框。 若要查看 **“分区管理器”** 对话框，请在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，单击 **“表”** 菜单，然后单击 **“分区”**。  
  
###  <a name="bkmk_create_new"></a> 创建新分区  
  
1.  在模型设计器中，选择要为其定义分区的表。  
  
2.  单击 **“表”** 菜单，然后单击 **“分区”**。  
  
3.  在 **“分区管理器”**的 **“表”** 列表框中，验证或选择要分区的表，然后单击 **“新建”**。  
  
4.  在 **“分区名称”**中，键入分区的名称。 默认情况下，对于每个新建分区，默认分区的名称将为递增式编号。  
  
5.  通过使用表预览模式或使用通过查询编辑器模式创建的 SQL 查询，您可以选择包含在分区中的行和列。  
  
     若要使用表预览模式（默认），请单击预览窗口右上角附近的“表预览”按钮。 通过选中列名称旁边的复选框，选择要包含在分区中的列。 若要筛选行，右键单击一个单元值，然后单击 **“按所选的单元值筛选”**。  
  
     若要使用 SQL 语句，请单击预览窗口右上角附近的“查询编辑器”按钮，然后将 SQL 查询语句键入或粘贴到查询窗口中。 若要验证您的语句，请单击 **“验证”**。 若要使用查询设计器，请单击 **“设计”**。  
  
###  <a name="bkmk_copy"></a> 复制分区  
  
1.  在 **“分区管理器”**的 **“表”** 列表框中，验证或选择包含要复制的分区的表。  
  
2.  在 **“分区”** 列表中，选择要复制的分区，然后单击 **“复制”**。  
  
3.  在 **“分区名称”**中，键入分区的新名称。  
  
###  <a name="bkmk_delete"></a> 删除分区  
  
1.  在 **“分区管理器”**的 **“表”** 列表框中，验证或选择包含要删除的分区的表。  
  
2.  在 **“分区”** 列表中，选择要删除的分区，然后单击 **“删除”**。  
  
## <a name="see-also"></a>另请参阅  
 [分区](../../analysis-services/tabular-models/partitions-ssas-tabular.md)   
 [在工作区数据库中处理分区](../../analysis-services/tabular-models/process-partitions-in-the-workspace-databse-ssas-tabular.md)  
  
  
