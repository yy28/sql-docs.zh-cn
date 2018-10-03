---
title: 创建和管理表格模型分区 (SSAS 表格) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: dab72cf0-95bc-4b63-95dc-505b5cd881c1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a2e06d49f22180ae99bf5f41bb4007fda1e03f84
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48113597"
---
# <a name="create-and-manage-tabular-model-partitions-ssas-tabular"></a>创建和管理表格模型分区（SSAS 表格）
  分区将表分成多个逻辑部分。 然后，每个分区可独立于其他分区进行处理（刷新）。 在已部署的模型中将重复在模型创作过程中为模型定义的分区。 部署完成后，您可以通过使用 **中的** “分区” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 对话框或使用脚本来管理这些分区。 本主题中提供的任务介绍如何为已部署的模型创建和管理分区。  
  
 本主题包括以下任务：  
  
-   [创建新分区](#bkmk_create_new)  
  
-   [复制分区](#bkmk_copy)  
  
-   [合并两个或更多分区](#bkmk_merge)  
  
-   [删除分区](#bkmk_delete)  
  
## <a name="tasks"></a>“任务”  
 若要为已部署的表格模型数据库创建和管理分区，您可以使用 **中的** “分区” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]对话框。 若要查看“分区”对话框，请在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中右键单击某一表，然后单击“分区”。  
  
###  <a name="bkmk_create_new"></a> 创建新分区  
  
1.  在 **“分区”** 对话框中，单击 **“新建”** 按钮。  
  
2.  在 **“分区名称”** 中，键入分区的名称。 默认情况下，对于每个新建分区，默认分区的名称将为递增式编号。  
  
3.  在 **“SQL 语句”** 中，将定义您想要在分区中包含的列和任何子句的 SQL 查询语句键入或粘贴到查询窗口中。  
  
4.  若要验证语句，请单击 **“检查语法”**。  
  
###  <a name="bkmk_copy"></a> 复制分区  
  
1.  在 **“分区”** 对话框的 **“分区”** 列表中，选择您要复制的分区，然后单击 **“复制”** 按钮。  
  
2.  在 **“分区名称”** 中，键入分区的新名称。  
  
3.  在 **“SQL 语句”**，编辑 SQL 查询语句。  
  
###  <a name="bkmk_merge"></a> 合并两个或更多分区  
  
-   在中**分区**对话框中**分区**列表中，使用 Ctrl + 单击以选择你想要合并的分区，然后单击**合并**按钮。  
  
> [!IMPORTANT]  
>  合并分区不会更新分区元数据。 管理员必须为所得分区更改 SQL 语句，以确保处理操作处理合并分区中的所有数据。  
  
###  <a name="bkmk_delete"></a> 删除分区  
  
-   在 **“分区”** 对话框的 **“分区”** 列表中，选择您要删除的分区，然后单击 **“删除”** 按钮。  
  
## <a name="see-also"></a>请参阅  
 [表格模型分区&#40;SSAS 表格&#41;](partitions-ssas-tabular.md)   
 [处理表格模型分区&#40;SSAS 表格&#41;](process-tabular-model-partitions-ssas-tabular.md)  
  
  
