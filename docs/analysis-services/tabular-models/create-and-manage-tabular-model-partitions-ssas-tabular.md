---
title: 创建和管理表格模型分区 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7067449c0de9958e98a7a9dc5cc09c7f89f33fa9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472289"
---
# <a name="create-and-manage-tabular-model-partitions"></a>创建和管理表格模型分区
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  分区将表分成多个逻辑部分。 然后，每个分区可独立于其他分区进行处理（刷新）。 在已部署的模型中将重复在模型创作过程中为模型定义的分区。 部署完成后，您可以通过使用 **中的** “分区” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 对话框或使用脚本来管理这些分区。 本主题中提供的任务介绍如何为已部署的模型创建和管理分区。  
  
  > [!NOTE]  
>  在 1400年兼容性级别创建的表格模型中的分区使用 M 查询语句进行定义。 若要了解详细信息，请参阅[M 引用](https://msdn.microsoft.com/library/mt211003.aspx)。 
>
  
## <a name="tasks"></a>“任务”  
 若要为已部署的表格模型数据库创建和管理分区，您可以使用 **中的** “分区” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]对话框。 若要查看“分区”对话框，请在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中右键单击某一表，然后单击“分区”。  
  
###  <a name="bkmk_create_new"></a> 创建新分区  
  
1.  在 **“分区”** 对话框中，单击 **“新建”** 按钮。  
  
2.  在 **“分区名称”** 中，键入分区的名称。 默认情况下，对于每个新建分区，默认分区的名称将为递增式编号。  
  
3.  在中**查询语句**，键入或粘贴 SQL 或 M 查询语句定义的列和任何你想要包括到查询窗口在分区中的子句。  
  
4.  若要验证语句，请单击 **“检查语法”**。  
  
###  <a name="bkmk_copy"></a> 复制分区  
  
1.  在 **“分区”** 对话框的 **“分区”** 列表中，选择您要复制的分区，然后单击 **“复制”** 按钮。  
  
2.  在 **“分区名称”** 中，键入分区的新名称。  
  
3.  在中**查询语句**，编辑查询语句。  
  
###  <a name="bkmk_merge"></a> 合并两个或更多分区  
  
-   在中**分区**对话框中**分区**列表中，使用 Ctrl + 单击以选择你想要合并的分区，然后单击**合并**按钮。  
  
> [!IMPORTANT]  
>  合并分区不会更新分区元数据。 必须编辑所得分区以确保处理操作处理合并的分区中的所有数据的 SQL 或 M 语句。  
  
###  <a name="bkmk_delete"></a> 删除分区  
  
-   在 **“分区”** 对话框的 **“分区”** 列表中，选择您要删除的分区，然后单击 **“删除”** 按钮。  
  
## <a name="see-also"></a>另请参阅  
 [表格模型分区](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [处理表格模型分区](../../analysis-services/tabular-models/process-tabular-model-partitions-ssas-tabular.md)  
  
  
