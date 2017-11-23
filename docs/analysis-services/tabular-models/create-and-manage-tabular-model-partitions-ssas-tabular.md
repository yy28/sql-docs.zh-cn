---
title: "创建和管理表格模型分区 (SSAS 表格) |Microsoft 文档"
ms.custom: 
ms.date: 05/31/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dab72cf0-95bc-4b63-95dc-505b5cd881c1
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dcf049205f00cf10f4c8dda308911b202c3a3728
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="create-and-manage-tabular-model-partitions"></a>创建和管理表格模型分区

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  分区将表分成多个逻辑部分。 然后，每个分区可独立于其他分区进行处理（刷新）。 在已部署的模型中将重复在模型创作过程中为模型定义的分区。 部署完成后，您可以通过使用 **中的** “分区” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 对话框或使用脚本来管理这些分区。 本主题中提供的任务介绍如何为已部署的模型创建和管理分区。  
  
  > [!NOTE]  
>  创建在 1400年兼容性级别的表格模型中的分区的使用 M 查询语句定义。 若要了解详细信息，请参阅[M 引用](https://msdn.microsoft.com/library/mt211003.aspx)。 
>
  
## <a name="tasks"></a>“任务”  
 若要为已部署的表格模型数据库创建和管理分区，您可以使用 **中的** “分区” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]对话框。 若要查看“分区”对话框，请在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中右键单击某一表，然后单击“分区”。  
  
###  <a name="bkmk_create_new"></a> 创建新分区  
  
1.  在 **“分区”** 对话框中，单击 **“新建”** 按钮。  
  
2.  在 **“分区名称”**中，键入分区的名称。 默认情况下，对于每个新建分区，默认分区的名称将为递增式编号。  
  
3.  在**查询语句**，键入或粘贴 SQL 或 M 查询语句，用于定义列和任何你想要包含在分区到查询窗口的子句。  
  
4.  若要验证语句，请单击 **“检查语法”**。  
  
###  <a name="bkmk_copy"></a> 复制分区  
  
1.  在 **“分区”** 对话框的 **“分区”** 列表中，选择您要复制的分区，然后单击 **“复制”** 按钮。  
  
2.  在 **“分区名称”**中，键入分区的新名称。  
  
3.  在**查询语句**，编辑查询语句。  
  
###  <a name="bkmk_merge"></a> 合并两个或更多分区  
  
-   在**分区**对话框中，在**分区**列表，按下 Ctrl + 单击以选择你想要合并的分区，然后单击**合并**按钮。  
  
> [!IMPORTANT]  
>  合并分区不会更新分区元数据。 你必须编辑所得分区以确保处理操作处理合并分区中的所有数据的 SQL 或 M 语句。  
  
###  <a name="bkmk_delete"></a> 删除分区  
  
-   在 **“分区”** 对话框的 **“分区”** 列表中，选择您要删除的分区，然后单击 **“删除”** 按钮。  
  
## <a name="see-also"></a>另请参阅  
 [表格模型分区](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [处理表格模型分区](../../analysis-services/tabular-models/process-tabular-model-partitions-ssas-tabular.md)  
  
  
