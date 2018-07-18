---
title: 大容量插入任务编辑器 （连接页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.bulkinserttask.connection.f1
helpviewer_keywords:
- Bulk Insert Task Editor
ms.assetid: 51252c20-8865-4ede-a3fd-bd73a968f47d
caps.latest.revision: 30
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ed6ab27e4c60aa398cafe1be0d4bbcb19ce3bb3d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201807"
---
# <a name="bulk-insert-task-editor-connection-page"></a>大容量插入任务编辑器（“连接”页）
  可以使用 **“大容量插入任务编辑器”** 对话框的 **“连接”** 页，指定大容量插入操作的源和目标以及使用的格式。  
  
 若要了解大容量插入，请参阅[大容量插入任务](control-flow/bulk-insert-task.md)和[用来导入或导出数据的格式化文件 (SQL Server)](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)。  
  
## <a name="options"></a>“常规”  
 **“连接”**  
 在列表中选择一个 OLE DB 连接管理器，或单击“\<新建连接…>”，创建一个新连接。  
  
 **相关主题：**[OLE DB 连接管理器](connection-manager/ole-db-connection-manager.md)、[配置 OLE DB 连接管理器](../../2014/integration-services/configure-ole-db-connection-manager.md)  
  
 **DestinationTable**  
 键入目标表或视图的名称，或在列表中选择表或视图。  
  
 **格式**  
 选择大容量插入任务的格式源。 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**使用文件**|选择包含格式规范的文件。 选择此选项将显示动态选项 **FormatFile**。|  
|**指定**|指定格式。 选择此选项将显示动态选项`RowDelimiter`和`ColumnDelimiter`。|  
  
 **File**  
 在列表中选择一个文件或平面文件连接管理器，或单击“\<新建连接…>”，创建一个新连接。  
  
 文件位置与在此任务的连接管理器中指定的 SQL Server 数据库引擎有关。 该文本文件必须可被服务器本地硬盘上的 SQL Server 数据库引擎访问，或可通过 SQL Server 的共享驱动器或映射的驱动器访问。 SSIS 运行时不访问该文件。  
  
 如果通过使用平面文件连接管理器来访问源文件，则大容量插入任务不会使用在平面文件连接管理器中指定的格式。 相反，大容量插入任务将使用在格式化文件中指定的格式，或者使用该任务的 RowDelimite 和 ColumnDelimiter 属性的值。  
  
 **相关主题：**[文件连接管理器](connection-manager/file-connection-manager.md)、[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)、[平面文件连接管理器](connection-manager/flat-file-connection-manager.md)、[平面文件连接管理器编辑器（“常规”页）](general-page-of-integration-services-designers-options.md)、[平面文件连接管理器编辑器（“列”页）](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)、[平面文件连接管理器编辑器（“高级”页）](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)  
  
 **刷新表**  
 刷新表和视图的列表。  
  
## <a name="format-dynamic-options"></a>Format 动态选项  
  
### <a name="format--use-file"></a>Format = 使用文件  
 **FormatFile**  
 键入格式化文件的路径，或单击省略号按钮 **(…)** 定位到该格式化文件。  
  
### <a name="format--specify"></a>Format = 指定  
 `RowDelimiter`  
 指定源文件中的行分隔符。 默认值为 **{CR}{LF}**。  
  
 `ColumnDelimiter`  
 指定源文件中的列分隔符。 默认值为 **“制表符”**。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [大容量插入任务编辑器&#40;常规页&#41;](../../2014/integration-services/bulk-insert-task-editor-general-page.md)   
 [大容量插入任务编辑器&#40;选项页&#41;](../../2014/integration-services/bulk-insert-task-editor-options-page.md)   
 [表达式页](expressions/expressions-page.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [控制流](control-flow/control-flow.md)  
  
  
