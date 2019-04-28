---
title: “数据集属性”对话框 ->“查询”（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10024"
ms.assetid: 75432318-0b00-4797-917c-0a2e74f9d951
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8a74bac81874eaeeecd9b9abcdcbfee27e07909c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62696568"
---
# <a name="dataset-properties-dialog-box-query-report-builder"></a>“数据集属性”对话框 -&gt;“查询”（报表生成器）
  选择 **“数据集属性”** 对话框中的 **“查询”** 可以从报表服务器选择共享数据集或创建嵌入数据集。 对于嵌入数据集，必须选择一个数据源并生成查询。  
  
 与 **“数据集属性”** 对话框相关的主题还有：  
  
-   [“数据集属性”对话框 ->“参数”（报表生成器）](../dataset-properties-dialog-box-parameters-report-builder.md)  
  
-   [“数据集属性”对话框 ->“字段”（报表生成器）](../dataset-properties-dialog-box-fields-report-builder.md)  
  
-   [“数据集属性”对话框 ->“选项”（报表生成器）](dataset-properties-dialog-box-options-report-builder.md)  
  
-   [“数据集属性”对话框 ->“筛选器”（报表生成器）](../dataset-properties-dialog-box-filters-report-builder.md)  
  
 有关详细信息，请参阅 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="options"></a>选项  
 **名称**  
 为数据集键入名称。 该名称不能与报表中的任何数据区域或组的名称相同。  
  
 **使用共享数据集**  
 选择此选项可以使用报表服务器中的预定义数据集。  
  
 **“浏览”**  
 找到报表服务器或 SharePoint 站点上的文件夹，然后选择一个共享数据集 (.rsd)。  
  
 **在我的报表中使用嵌入数据集**  
 选择此选项可以创建仅供此报表使用的数据集。  
  
 **数据源**  
 选择数据集要基于的数据源。 若要创建新的数据源，单击 **“新建”**。  
  
 **查询类型**  
 选择要用于数据集的命令或查询的类型。 选择 **Text** 可运行从数据库中检索数据的查询。 选择 **Table** 可使用 **的** TableDirect [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能选择表内的所有字段。 选择 **Stored Procedure** 可按名称运行存储过程。 默认情况下将选择**Text** ，该类型适用于大多数查询。 若要编辑选中的数据源查询，单击 **“查询设计器”**。  
  
> [!NOTE]  
>  不是任何数据源都支持所有查询类型。 例如，仅数据源类型 **OLE DB** 和 **ODBC** 支持 **Table**。  
  
 **“数据集属性”**  
 选中 **Text** 命令类型选项后将显示此选项。 需键入一个查询或通过单击“导入”来导入一个预先存在的查询。 单击“表达式” (*fx*) 按钮可编辑表达式。  
  
> [!NOTE]  
>  如果您已使用查询设计器生成了一个查询，则此对话框中将显示该查询的文本。  
  
 **表名**  
 需输入要用作数据集的表的名称。 选中 **“表”** 后会显示此选项。  
  
 **选择或输入存储过程名称**  
 需键入或选择要使用的存储过程的名称。 单击“表达式” (*fx*) 按钮可编辑表达式。 选中“存储过程”命令类型选项后会显示此选项。  
  
 **超时（以秒为单位）**  
 键入查询在多长时间后超时（秒）。默认值为 30 秒。 **“超时值”** 的值必须为空或大于零。 如果该值为空，则查询将不会超时。  
  
 **刷新字段**  
 运行查询命令来更新[“数据集属性”对话框 -&gt;“字段”](../dataset-properties-dialog-box-fields-report-builder.md) 页中的字段列表。  
  
## <a name="see-also"></a>请参阅  
 [向报表添加数据&#40;报表生成器和 SSRS&#41;](report-datasets-ssrs.md)   
 [用于对话框、窗格和向导的报表生成器帮助](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [查询设计器（报表生成器）](../query-designers-report-builder.md)  
  
  
