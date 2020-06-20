---
title: 创建和管理工作区数据库中的分区（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.partitionmgr.f1
ms.assetid: 0b3027d6-652b-4eb3-a197-58b25df65218
author: minewiskan
ms.author: owend
ms.openlocfilehash: ef8a03920b20adadc19072f184a0629885d4a3fb
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939798"
---
# <a name="create-and-manage-partitions-in-the-workspace-database-ssas-tabular"></a>创建和管理工作区数据库中的分区（SSAS 表格）
  分区将表分成多个逻辑部分。 然后，可单独处理（刷新）每个分区，也可与其他分区并行处理每个分区。 分区可以提高大型数据库的可扩展性和可管理性。 默认情况下，每个表都具有一个包含所有列的分区。 本主题中的任务说明如何使用中的 "**分区管理器**" 对话框在模型工作区数据库中创建和管理分区。[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
 在将模型部署到其他 Analysis Services 实例后，数据库管理员可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]在（已部署）模型中创建和管理分区。 有关详细信息，请参阅[创建和管理表格模型分区（SSAS 表格）](partitions-ssas-tabular.md)。  
  
 本主题包括以下任务：  
  
-   [创建新分区](#bkmk_create_new)  
  
-   [复制分区](#bkmk_copy)  
  
-   [删除分区](#bkmk_delete)  
  
> [!NOTE]  
>  使用“分区管理器”对话框不能在模型工作区数据库中合并分区。 通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，仅能在已部署的模型中合并分区。  
  
## <a name="tasks"></a>任务  
 若要创建和管理分区，您将使用 **“分区管理器”** 对话框。 若要查看 **“分区管理器”** 对话框，请在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，单击 **“表”** 菜单，然后单击 **“分区”**。  
  
###  <a name="to-create-a-new-partition"></a><a name="bkmk_create_new"></a>创建新分区  
  
1.  在模型设计器中，选择要为其定义分区的表。  
  
2.  单击 **“表”** 菜单，然后单击 **“分区”**。  
  
3.  在 **“分区管理器”** 的 **“表”** 列表框中，验证或选择要分区的表，然后单击 **“新建”**。  
  
4.  在 **“分区名称”** 中，键入分区的名称。 默认情况下，对于每个新建分区，默认分区的名称将为递增式编号。  
  
5.  通过使用表预览模式或使用通过查询编辑器模式创建的 SQL 查询，您可以选择包含在分区中的行和列。  
  
     若要使用表预览模式（默认），请单击预览窗口右上角附近的“表预览”按钮。**** 通过选中列名称旁边的复选框，选择要包含在分区中的列。 若要筛选行，右键单击一个单元值，然后单击 **“按所选的单元值筛选”**。  
  
     若要使用 SQL 语句，请单击预览窗口右上角附近的“查询编辑器”按钮，然后将 SQL 查询语句键入或粘贴到查询窗口中。**** 若要验证您的语句，请单击 **“验证”**。 若要使用查询设计器，请单击 **“设计”**。  
  
###  <a name="to-copy-a-partition"></a><a name="bkmk_copy"></a>复制分区  
  
1.  在 **“分区管理器”** 的 **“表”** 列表框中，验证或选择包含要复制的分区的表。  
  
2.  在 **“分区”** 列表中，选择要复制的分区，然后单击 **“复制”**。  
  
3.  在 **“分区名称”** 中，键入分区的新名称。  
  
###  <a name="to-delete-a-partition"></a><a name="bkmk_delete"></a>删除分区  
  
1.  在 **“分区管理器”** 的 **“表”** 列表框中，验证或选择包含要删除的分区的表。  
  
2.  在 **“分区”** 列表中，选择要删除的分区，然后单击 **“删除”**。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSAS 表格&#41;分区](partitions-ssas-tabular.md)   
 [&#40;SSAS 表格中处理工作区数据库中的分区&#41;](process-partitions-in-the-workspace-database-ssas-tabular.md)  
  
  
