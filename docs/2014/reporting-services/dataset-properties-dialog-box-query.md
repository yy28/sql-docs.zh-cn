---
title: "\"数据集属性\" 对话框-> \"查询\" |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10160"
- sql12.rtp.rptdesigner.datasetproperties.query.f1
ms.assetid: 1fa34a4b-7de0-4e92-99fa-bc28a206773f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aead5d8e5c85b67333f10bee4e73e2bb1a8633ab
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109366"
---
# <a name="dataset-properties-dialog-box-query"></a>“数据集属性”对话框 -&gt;“查询”
  在 "**数据集属性**" 对话框中选择 "**查询**" 可以选择数据源并创建查询。  
  
 与 **“数据集属性”** 对话框相关的主题还有：  
  
-   [“数据集属性”对话框 -&gt;“参数”](report-data/dataset-properties-dialog-box-parameters.md)  
  
-   [“数据集属性”对话框 -&amp;gt;“字段”](../../2014/reporting-services/dataset-properties-dialog-box-fields.md)  
  
-   [“数据集属性”对话框 -&amp;gt;“选项”](../../2014/reporting-services/dataset-properties-dialog-box-options.md)  
  
-   [“数据集属性”对话框 -&amp;gt;“筛选器”](report-data/dataset-properties-dialog-box-filters.md)  
  
## <a name="options"></a>选项  
 **名称**  
 为数据集键入名称。 该名称不能与报表中的任何数据区域或组的名称相同。  
  
 **数据源**  
 选择数据集要基于的数据源。 若要创建新的数据源，单击 **“新建”**。  
  
 **查询类型**  
 选择要用于数据集的命令或查询的类型。 选择 **Text** 可运行从数据库中检索数据的查询。 选择 **Table** 可使用 **的** TableDirect [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能选择表内的所有字段。 选择 **Stored Procedure** 可按名称运行存储过程。 默认情况下将选择**Text** ，该类型适用于大多数查询。 若要编辑选中的数据源查询，单击 **“查询设计器”**。  
  
> [!NOTE]  
>  不是任何数据源都支持所有查询类型。 例如，仅数据源类型 **OLE DB** 和 **ODBC** 支持 **Table**。  
  
 **查询**  
 选中 **Text** 命令类型选项后将显示此选项。 需键入一个查询或通过单击“导入”来导入一个预先存在的查询****。 单击“表达式”**** (*fx*) 按钮可编辑表达式。  
  
> [!NOTE]  
>  如果您已使用查询设计器生成了一个查询，则此对话框中将显示该查询的文本。  
  
 **表名称**  
 需输入要用作数据集的表的名称。 选中 **“表”** 后会显示此选项。  
  
 **选择或输入存储过程名称**  
 需键入或选择要使用的存储过程的名称。 单击“表达式”**** (*fx*) 按钮可编辑表达式。 选中“存储过程”命令类型选项后会显示此选项。  
  
 **超时（以秒为单位）**  
 键入查询超时前等待的秒数。默认值为30秒。 **“超时值”** 的值必须为空或大于零。 如果该值为空，则查询将不会超时。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 中的数据连接、数据源和连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [将数据添加到报表 &#40;报表生成器和 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [查询设计器 &#40;报表生成器&#41;](../../2014/reporting-services/query-designers-report-builder.md)   
 [Reporting Services 查询设计器](../../2014/reporting-services/reporting-services-query-designers.md)  
  
  
