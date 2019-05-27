---
title: 执行 SQL 任务编辑器 （常规页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.general.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: beb39086-28ce-46af-b6d8-f7b4fb8d9069
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 96d211defa789888a3fd7b513b4dff60fa795cb6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058992"
---
# <a name="execute-sql-task-editor-general-page"></a>执行 SQL 任务编辑器（“常规”页）
  可以使用 **“执行 SQL 任务编辑器”** 对话框的 **“常规”** 页，配置执行 SQL 任务以及提供任务运行的 SQL 语句。  
  
 若要了解有关此任务的信息，请参阅[执行 SQL 任务](control-flow/execute-sql-task.md)、[执行 SQL 任务中的参数和返回代码](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)和[执行 SQL 任务中的结果集](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)。 若要了解关于 Transact-SQL 查询语言的详细信息，请参阅 [Transact-SQL 引用（数据库引擎）](/sql/t-sql/language-reference)。  
  
## <a name="static-options"></a>静态选项  
 **名称**  
 为工作流中的执行 SQL 任务提供唯一的名称。 所提供的名称将在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中显示。  
  
 **说明**  
 描述执行 SQL 任务。 最好按照任务的用途对其进行说明，使其一目了然，便于维护。  
  
 **TimeOut**  
 指定任务超时之前运行的最大秒数。如果值为 0，则表示不限制时间。 默认值为 0。  
  
> [!NOTE]  
>  如果存储过程通过为要建立的连接和要完成的事务提供比 **TimeOut**指定秒数更长的时间来模拟睡眠功能，则将不会超时。 但是，执行查询的存储过程始终受 **TimeOut**指定时间的限制。  
  
 **CodePage**  
 指定在转换变量中的 Unicode 值时要使用的代码页。 默认值为本地计算机的代码页。  
  
> [!NOTE]  
>  当执行 SQL 任务使用 ADO 或 ODBC 连接管理器时， **CodePage** 属性不可用。 如果解决方案需要使用代码页，请将 OLE DB 或 ADO.NET 连接管理器与执行 SQL 任务一起使用。  
  
 **TypeConversionMode**  
 在您将此属性设置为 `Allowed` 时，“执行 SQL 任务”将尝试将输出参数和查询结果转换为结果赋值给的变量的数据类型。 这适用于 **单行** 结果集类型。  
  
 **ResultSet**  
 指定运行 SQL 语句预期的结果类型。 从 **“单行”**、 **“完整结果集”**、 **XML**或 **“无”** 中选择。  
  
 **ConnectionType**  
 选择连接数据源要使用的连接管理器的类型。 可用的连接类型包括 **OLE DB**、 **ODBC**、 **ADO**、 **ADO.NET** 和 **SQLMOBILE**。  
  
 **相关主题：**[OLE DB 连接管理器](connection-manager/ole-db-connection-manager.md)、[ODBC 连接管理器](connection-manager/odbc-connection-manager.md)、[ADO 连接管理器](connection-manager/ado-connection-manager.md)、[ADO.NET 连接管理器](connection-manager/ado-net-connection-manager.md)、[SQL Server Compact Edition 连接管理器](connection-manager/sql-server-compact-edition-connection-manager.md)  
  
 **“连接”**  
 从已定义的连接管理器的列表中选择连接。 要创建新连接，请选择“\<新建连接...>”。  
  
 **SQLSourceType**  
 选择任务运行的 SQL 语句的源类型。  
  
 根据执行 SQL 任务所用的连接管理器类型，必须在参数化 SQL 语句中使用特定的参数标记。  
  
 **相关主题：** 在运行参数化 SQL 命令部分[执行 SQL 任务](control-flow/execute-sql-task.md)  
  
 此属性具有下表所列的选项。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**直接输入**|将源设置为某个 Transact-SQL 语句。 选择此值将显示动态选项 **SQLStatement**。|  
|**文件连接**|选择包含 Transact-SQL 语句的文件。 设置此选项将显示动态选项 **FileConnection**。|  
|**变量**|将源设置为定义 Transact-SQL 语句的变量。 选择此值将显示动态选项 **SourceVariable**。|  
  
 **QueryIsStoredProcedure**  
 指示要运行的指定 SQL 语句是否为存储过程。 只有当任务使用 ADO 连接管理器时，此属性才是可读/写的。 否则该属性为只读，其值为 `false`。  
  
 **BypassPrepare**  
 指示 SQL 语句是否已准备就绪。  如果为 `true`，则跳过准备过程；如果为 `false`，则在运行 SQL 语句前准备 SQL 语句。 此选项仅可用于支持准备的 OLE DB 连接。  
  
 **相关主题：**[准备好的执行](../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
 **“浏览”**  
 使用“打开”对话框定位包含 SQL 语句的文件。 选择一个文件，将文件内容作为 SQL 语句复制到 **SQLStatement** 属性中。  
  
 **生成查询**  
 使用“查询生成器”对话框创建 SQL 语句，查询生成器是一种用于创建查询的图形工具。 此选项在 **SQLSourceType** 选项设置为 **“直接输入”** 时可用。  
  
 **分析查询**  
 验证 SQL 语句的语法。  
  
## <a name="sqlsourcetype-dynamic-options"></a>SQLSourceType 动态选项  
  
### <a name="sqlsourcetype--direct-input"></a>SQLSourceType = 直接输入  
 **SQLStatement**  
 在选项框中键入要执行的 SQL 语句，或者单击浏览按钮 (…)，在“输入 SQL 查询”对话框中键入 SQL 语句，还可以单击“生成查询”，使用“查询生成器”对话框编写 SQL 语句。  
  
 **相关主题：**[查询生成器](../../2014/integration-services/query-builder.md)  
  
### <a name="sqlsourcetype--file-connection"></a>SQLSourceType = 文件连接  
 **文件连接**  
 选择现有文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关主题：**[文件连接管理器](connection-manager/file-connection-manager.md)、[文件连接管理器编辑器](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="sqlsourcetype--variable"></a>SQLSourceType = 变量  
 **SourceVariable**  
 选择现有变量，或单击“\<新建变量...>”，创建一个新变量。  
  
 **相关主题：**[Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)、[添加变量](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [执行 SQL 任务编辑器&#40;参数映射页&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)   
 [执行 SQL 任务编辑器&#40;结果集页&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)  
  
  
