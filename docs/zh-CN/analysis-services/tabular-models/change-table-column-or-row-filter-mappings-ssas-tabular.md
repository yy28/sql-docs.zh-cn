---
title: 更改表、 列或行筛选器映射 |Microsoft 文档
ms.custom: ''
ms.date: 02/21/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2124c526-5772-4f84-a019-9dd3e906e8dd
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d7c2ec71bb6fe0703e374c105bcb106785a28657
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
  
  
  
