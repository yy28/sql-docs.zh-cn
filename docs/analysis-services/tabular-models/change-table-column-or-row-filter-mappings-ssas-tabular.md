---
title: 更改表、 列或行筛选器映射 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5583e0747806453f92fcd98001299b31bd4c0ef8
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="change-table-column-or-row-filter-mappings"></a>更改表、列或行筛选器映射 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  本文介绍如何通过更改表、 列或行筛选器映射**编辑表属性**中的对话框[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]。  
  
 根据您最初是通过从列表中选择表还是通过使用 SQL 查询导入数据的， **“编辑表属性”** 对话框中的选项将有所不同。 如果最初是通过从列表中选择数据来导入数据的，则 **“编辑表属性”** 对话框将显示“表预览”模式。 这种模式仅显示源表的一个子集，即前五十行。 如果最初是通过使用 SQL 语句来导入数据的，则 **“编辑表属性”** 对话框仅显示一条 SQL 语句。 通过使用 SQL 查询语句，您可以通过设计筛选器或手动编辑 SQL 语句来检索行的子集。  
  
 如果您将源更改为与当前表具有不同列的表，将显示一条消息以警告您列不相同。 然后，您必须选择要放在当前表中的列，并单击 **“保存”**。 您可以通过选中表左侧的复选框来替换整个表。  
  
> [!NOTE]  
>  如果表有多个分区，则无法使用“编辑表属性”对话框更改行筛选器映射。 若要更改具有多个分区的表的行筛选器映射，请使用分区管理器。 有关详细信息，请参阅[分区](../../analysis-services/tabular-models/partitions-ssas-tabular.md)。  
  
#### <a name="to-change-table-column-or-row-filter-mappings"></a>更改表、列或行筛选器映射  
  
1.  在模型设计器中，依次单击表、 **“表”** 菜单和 **“表属性”**。  
  
2.  在 **“编辑表属性”** 对话框中，找到包含筛选条件的列，然后单击列标题右侧的向下箭头。  
  
3.  在 **“自动筛选”** 菜单中，执行以下操作之一：  
  
    -   在列值的列表中，选择或清除作为筛选依据的一个或多个值，然后单击“确定”。  
  
         如果值的数目极多，则可能无法在列表中显示各个项。 此时您将看到消息“项过多，无法显示。”  
  
    -   单击“数字筛选器”或“文本筛选器”（根据列类型），然后单击比较运算符命令（如“等于”），或单击“自定义筛选器”。 在 **“自定义筛选器”** 对话框中，创建筛选器，然后单击 **“确定”**。  
  
         如果您执行了错误的操作并需要重新开始，请单击 **“清除行筛选器”**。  
  
  
  
