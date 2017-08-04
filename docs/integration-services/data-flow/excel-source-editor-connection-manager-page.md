---
title: "Excel 源编辑器 （连接管理器页） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.excelsourceadapter.connection.f1
helpviewer_keywords:
- Excel Source Editor
ms.assetid: 428e04e0-ad98-45d0-8345-12ec1b67b2eb
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c1f01be71a5093945a49c43a3a2aec334db7584b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="excel-source-editor-connection-manager-page"></a>Excel 源编辑器（“连接管理器”页）
  使用 **“Excel 源编辑器”** 对话框的 **“连接管理器”** 节点可以为源选择要使用的 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 工作簿。 Excel 源从现有工作簿中的工作表或指定范围中读取数据。  
  
> [!NOTE]  
>  Excel 源的 **CommandTimeout** 属性未在 **“Excel 源编辑器”**中提供，但可以使用 **“高级编辑器”**进行设置。 有关此属性的详细信息，请参阅 [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md)的“Excel 源”部分。  
  
 若要了解有关 Excel 源的详细信息，请参阅 [Excel Source](../../integration-services/data-flow/excel-source.md)。  
  
## <a name="static-options"></a>静态选项  
 **“无缓存”**  
 从列表中选择现有的 Excel 连接管理器，或单击“新建”创建新连接。  
  
 **新建**  
 使用“Excel 连接管理器”对话框创建一个新连接管理器。  
  
 **数据访问模式**  
 指定从源选择数据的方法。  
  
|“值”|Description|  
|-----------|-----------------|  
|表或视图|从 Excel 文件的工作表或指定范围中检索数据。|  
|表名变量或视图名变量|在变量中指定工作表名称或范围名称。<br /><br /> **相关信息：** [在包中使用变量](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL 命令|使用 SQL 查询从 Excel 文件中检索数据。 有关查询语法的详细信息，请参阅 [Excel Source](../../integration-services/data-flow/excel-source.md)。|  
|变量中的 SQL 命令|在变量中指定 SQL 查询文本。|  
  
 **预览**  
 通过使用“数据视图”对话框预览结果。 预览最多可以显示 200 行。  
  
## <a name="data-access-mode-dynamic-options"></a>数据访问模式动态选项  
  
### <a name="data-access-mode--table-or-view"></a>数据访问模式 = 表或视图  
 **Excel 表的名称**  
 从 Excel 工作簿可用的工作表或指定范围中选择工作表或指定范围的名称。  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>数据访问模式 = 表名变量或视图名变量  
 **变量名称**  
 选择包含工作表名称或指定范围名称的变量。  
  
### <a name="data-access-mode--sql-command"></a>数据访问模式 = SQL 命令  
 **SQL 命令文本**  
 输入 SQL 查询的文本，通过单击“生成查询”来生成查询，或通过单击“浏览”浏览至包含查询文本的文件。  
  
 **参数**  
 如果已经在参数化查询文本中使用 ? 作为参数占位符输入了参数化查询，请使用 **“设置查询参数”** 对话框将查询输入参数映射到包变量。  
  
 **生成查询**  
 使用“查询生成器”对话框可直观地构造 SQL 查询。  
  
 **浏览**  
 使用“打开”对话框可定位到包含 SQL 查询文本的文件。  
  
 **分析查询**  
 验证查询文本的语法。  
  
### <a name="data-access-mode--sql-command-from-variable"></a>数据访问模式 = 变量中的 SQL 命令  
 **变量名称**  
 选择包含 SQL 查询文本的变量。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [Excel 源编辑器 &#40;列页 &#41;](../../integration-services/data-flow/excel-source-editor-columns-page.md)   
 [Excel 源编辑器 &#40;错误输出页 &#41;](../../integration-services/data-flow/excel-source-editor-error-output-page.md)   
 [Excel 连接管理器](../../integration-services/connection-manager/excel-connection-manager.md)   
 [循环遍历 Excel 文件和表使用 Foreach 循环容器](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  
