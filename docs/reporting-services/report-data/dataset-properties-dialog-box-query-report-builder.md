---
title: "数据集属性对话框中，查询 （报表生成器） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- "10024"
- sql13.rtp.rptdesigner.datasetproperties.query.f1
- "10160"
ms.assetid: 75432318-0b00-4797-917c-0a2e74f9d951
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cc89e2a412163811aca2c8a99bdc3fae574d0926
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="dataset-properties-dialog-box-query-report-builder"></a>“数据集属性”对话框 -&gt;“查询”（报表生成器）
  选择 **“数据集属性”** 对话框中的 **“查询”** 可以从报表服务器选择共享数据集或创建嵌入数据集。 对于嵌入数据集，必须选择一个数据源并生成查询。  
  
 与 **“数据集属性”** 对话框相关的主题还有：  
  
-   [“数据集属性”对话框 -&gt;“参数”（报表生成器）](http://msdn.microsoft.com/library/3a0672ad-c969-455b-b952-585164ce1dda)  
  
-   [“数据集属性”对话框 -&gt;“字段”（报表生成器）](http://msdn.microsoft.com/library/75c7e54a-3d20-4c9a-88da-ab36dce2ce42)  
  
-   [“数据集属性”对话框 -&gt;“选项”（报表生成器）](../../reporting-services/report-data/dataset-properties-dialog-box-options-report-builder.md)  
  
-   [“数据集属性”对话框 -&gt;“筛选器”（报表生成器）](http://msdn.microsoft.com/library/933a6f44-4eb7-4e73-9c40-ac0fd17b23d3)  
  
 有关详细信息，请参阅[报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="options"></a>选项  
 **名称**  
 为数据集键入名称。 该名称不能与报表中的任何数据区域或组的名称相同。  
  
 **使用共享数据集**  
 选择此选项可以使用报表服务器中的预定义数据集。  
  
 **浏览**  
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
 需输入要用作数据集的表的名称。 选中 **“表”**后会显示此选项。  
  
 **选择或输入存储过程名称**  
 需键入或选择要使用的存储过程的名称。 单击“表达式” (*fx*) 按钮可编辑表达式。 选中“存储过程”命令类型选项后会显示此选项。  
  
 **超时（以秒为单位）**  
 键入查询在多长时间后超时（秒）。 默认值为 30 秒。 **“超时值”** 的值必须为空或大于零。 如果该值为空，则查询将不会超时。  
  
 **刷新字段**  
 运行查询命令来更新“数据集属性”对话框 -&gt;“字段” [](http://msdn.microsoft.com/library/75c7e54a-3d20-4c9a-88da-ab36dce2ce42) 页中的字段列表。  
  
## <a name="see-also"></a>另请参阅  
 [报表数据集 (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [用于对话框、窗格和向导的报表生成器帮助](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [查询设计器（报表生成器）](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9)  
  
  
