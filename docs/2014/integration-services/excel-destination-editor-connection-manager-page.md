---
title: Excel 目标编辑器 （连接管理器页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.exceldestadapter.connection.f1
helpviewer_keywords:
- Excel Destination Editor
ms.assetid: fc13f725-963c-488e-91e2-20627133e842
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f790e0cc9193f2f31c7f021c4d4901e7a825fb13
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62769733"
---
# <a name="excel-destination-editor-connection-manager-page"></a>Excel 目标编辑器（“连接管理器”页）
  使用 **“Excel 目标编辑器”** 对话框的 **“连接管理器”** 页可以指定数据源信息和预览结果。 Excel 目标将数据加载到 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 工作簿中的工作表或指定范围。  
  
> [!NOTE]  
>  `CommandTimeout` Excel 目标的属性不是在可用**Excel 目标编辑器**，但可以通过使用设置**高级编辑器**。 另外，某些快速加载选项仅在 **“高级编辑器”** 中提供。 有关这些属性的详细信息，请参阅 [Excel Custom Properties](data-flow/excel-custom-properties.md)的“Excel 目标”部分。  
  
 若要了解有关 Excel 目标的详细信息，请参阅 [Excel Destination](data-flow/excel-destination.md)。  
  
## <a name="static-options"></a>静态选项  
 **Excel 连接管理器**  
 从列表中选择现有的 Excel 连接管理器，或单击“新建”创建新连接。  
  
 **新建**  
 使用“Excel 连接管理器”对话框创建一个新连接管理器。  
  
 **数据访问模式**  
 指定从源选择数据的方法。  
  
|Option|Description|  
|------------|-----------------|  
|表或视图|将数据加载到 Excel 数据源中的工作表或指定范围。|  
|表名变量或视图名变量|在变量中指定工作表名称或范围名称。<br /><br /> **相关信息**：[在包中使用变量](../../2014/integration-services/use-variables-in-packages.md)|  
|SQL 命令|使用 SQL 查询将数据加载到 Excel 目标中。|  
  
 **Excel 表的名称**  
 从下拉列表中选择 Excel 目标。 如果此列表为空，请单击 **“新建”**。  
  
 **新建**  
 单击“新建”将启动“创建表”对话框。 当您单击 **“确定”** 时，此对话框将创建 **“Excel 连接管理器”** 指向的 Excel 文件。  
  
 **查看现有数据**  
 使用“预览查询结果”对话框预览结果。 预览最多可以显示 200 行。  
  
> [!WARNING]  
>  如果你选择的“Excel 连接管理器”指向的 Excel 文件不存在，则单击此按钮时你将看到一条错误消息。  
  
## <a name="data-access-mode-dynamic-options"></a>数据访问模式动态选项  
  
### <a name="data-access-mode--table-or-view"></a>数据访问模式 = 表或视图  
 **Excel 表的名称**  
 从数据源中可用的工作表或指定范围列表中选择工作表或指定范围的名称。  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>数据访问模式 = 表名变量或视图名变量  
 **变量名称**  
 选择包含工作表名称或指定范围名称的变量。  
  
### <a name="data-access-mode--sql-command"></a>数据访问模式 = SQL 命令  
 **SQL 命令文本**  
 输入 SQL 查询的文本，通过单击“生成查询”来生成查询，或通过单击“浏览”定位到包含查询文本的文件。  
  
 **生成查询**  
 使用“查询生成器”对话框可直观地构造 SQL 查询。  
  
 **“浏览”**  
 使用“打开”对话框可定位到包含 SQL 查询文本的文件。  
  
 **分析查询**  
 验证查询文本的语法。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Excel 目标编辑器（“映射”页）](../../2014/integration-services/excel-destination-editor-mappings-page.md)   
 [Excel 目标编辑器（“错误输出”页）](../../2014/integration-services/excel-destination-editor-error-output-page.md)   
 [使用 Foreach 循环容器循环遍历 Excel 文件和表](control-flow/foreach-loop-container.md)  
  
  
