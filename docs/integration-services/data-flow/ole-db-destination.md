---
title: OLE DB 目标 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbdest.f1
- sql13.dts.designer.oledbdestadapter.connection.f1
- sql13.dts.designer.oledbdestadapter.mappings.f1
- sql13.dts.designer.oledbdestadapter.errorhandling.f1
helpviewer_keywords:
- fast-load data access mode [Integration Services]
- OLE DB destination [Integration Services]
- fast load options [Integration Services]
- fast-load options [Integration Services]
- destinations [Integration Services], OLE DB
- fast load data access mode [Integration Services]
- inserting data
ms.assetid: 873a2fa0-2a02-41fc-a80a-ec9767f36a8a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 0e406e5966b9b865d7e25d8156880f333d5cba26
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897165"
---
# <a name="ole-db-destination"></a>OLE DB 目标

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  OLE DB 目标用数据库表或视图或者用 SQL 命令，将数据加载到各种符合 OLE DB 的数据库中。 例如，OLE DB 源可以将数据加载到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的表中。  
  
> [!NOTE]  
>  如果数据源是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007，则数据源需要一个不同于早期版本 Excel 的连接管理器。 有关详细信息，请参阅 [连接到 Excel 工作簿](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)。  
  
 OLE DB 目标为数据加载提供了五种数据访问模式：  
  
-   表或视图。 可以指定现有的表或视图，也可以创建新表。  
  
-   使用快速加载选项的表或视图。 可以指定现有的表或者创建新表。  
  
-   变量中指定的表或视图。  
  
-   使用快速加载选项在变量中指定的表或视图。  
  
-   SQL 语句的运行结果。  
  
> [!NOTE]  
>  OLE DB 目标不支持参数。 如果需要执行参数化 INSERT 语句，请考虑使用 OLE DB 命令转换。 有关详细信息，请参阅 [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md)。  
  
 当 OLE DB 目标加载使用双字节字符集 (DBCS) 的数据时，如果没有使用快速加载选项的数据访问模式，并且 OLE DB 连接管理器使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLOLEDB)，则该数据可能会被损坏。 为了确保 DBCS 数据的完整性，应将 OLE DB 连接管理器配置为使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 或使用以下任一快速加载访问模式：“表或视图 - 快速加载”或“表名称或视图名称变量 - 快速加载”。 这两个选项都可以在 **“OLE DB 目标编辑器”** 对话框中使用。 编程 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 对象模型时，应将 AccessMode 属性设置为 **OpenRowset Using FastLoad**或 **OpenRowset Using FastLoad From Variable**。  
  
> [!NOTE]  
>  如果用 **设计器中的** “OLE DB 目标编辑器” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 对话框创建 OLE DB 目标要向其插入数据的目标表，可能需要手动选择新创建的表。 当 OLE DB 访问接口（如 OLE DB Provider for DB2）自动将架构标识符添加到表名称时，需要进行手动选择。  
  
> [!NOTE]  
>  **“OLE DB 目标编辑器”** 对话框生成的 CREATE TABLE 语句可能需要修改，具体取决于目标类型。 例如，某些目标不支持 CREATE TABLE 语句所使用的数据类型。  
  
 此目标使用 OLE DB 连接管理器连接数据源，该连接管理器指定要使用的 OLE DB 访问接口。 有关详细信息，请参阅 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目还提供了可从中创建 OLE DB 连接管理器的数据源对象，使数据源和数据源视图可用于 OLE DB 目标。  
  
 OLE DB 目标包括输入列和目标数据源中的列之间的映射。 您不必将输入列映射到所有目标列，但有时如果没有将输入列映射到目标列可能会出错，具体取决于目标列的属性。 例如，如果目标列不允许出现 Null 值，则必须将输入列映射到该列。 另外，映射的列的数据类型必须是兼容的。 例如，不能将数据类型为字符串的输入列映射到数据类型为数值的目标列。  
  
 OLE DB 目标具有一个常规输入和一个错误输出。  
  
 有关数据类型的详细信息，请参阅 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="fast-load-options"></a>快速加载选项  
 如果 OLE DB 目标使用快速加载数据访问模式，则可以在用户界面“OLE DB 目标编辑器”中为目标指定以下快速加载选项：  
  
-   保持导入数据文件的标识值或使用由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]分配的唯一值。  
  
-   在大容量加载操作过程中保留 Null 值。  
  
-   在大容量导入操作过程中检查目标表或视图的约束。  
  
-   在大容量加载操作期间获取表级锁。  
  
-   指定批中的行数和提交大小。  
  
 某些快速加载选项存储在 OLE DB 目标的特定属性中。 例如，FastLoadKeepIdentity 指定是否保持标识值，FastLoadKeepNulls 指定是否保持 Null 值，而 FastLoadMaxInsertCommitSize 则指定作为批提交的行数。 其他快速加载选项则存储在 FastLoadOptions 属性内的以逗号分隔的列表中。 如果 OLE DB 目标使用存储于 FastLoadOptions 中和“OLE DB 目标编辑器”对话框中列出的所有快速加载选项，则该属性的值将设置为 **TABLOCK, CHECK_CONSTRAINTS, ROWS_PER_BATCH=1000**。 值 1000 指示已将目标配置为使用 1000 行组成的批。  
  
> [!NOTE]  
>  目标中任何约束失败都将导致 FastLoadMaxInsertCommitSize 所定义的整批行失败。  
  
 除了在“OLE DB 目标编辑器”对话框中公开的快速加载选项以外，还可以通过在“高级编辑器”对话框的 FastLoadOptions 属性中键入选项，将 OLE DB 目标配置为使用以下大容量加载选项。  
  
|快速加载选项|描述|  
|----------------------|-----------------|  
|KILOBYTES_PER_BATCH|指定要插入的大小 (KB)。 选项的格式为 KILOBYTES_PER_BATCH  = \<正整数值>。|  
|FIRE_TRIGGERS|指定是否在插入表上激发触发器。 选项的格式为 **FIRE_TRIGGERS**。 出现该选项说明要激发触发器。|  
|ORDER|指定输入数据如何排序。 选项格式为 ORDER \<列名称> ASC&#124;DESC。 可以列出任何列数，是否包括排序顺序是可选的。 如果省略排序顺序，则插入操作假定数据不排序。<br /><br /> 注意：如果使用 ORDER 选项根据表中的聚集索引对输入数据进行排序，可以提升性能。|  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 关键字传统上采用大写字母键入，但并不区分大小写。  
  
 若要了解快速加载选项的详细信息，请参阅[BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md)。  
  
## <a name="troubleshooting-the-ole-db-destination"></a>OLE DB 目标故障排除  
 可以记录 OLE DB 目标对外部数据访问接口所做的调用。 利用此日志记录功能，可以对 OLE DB 目标在执行将数据保存到外部数据源的操作进行故障排除。 若要记录 OLE DB 目标对外部数据访问接口所做的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅 [包执行的疑难解答工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuring-the-ole-db-destination"></a>配置 OLE DB 目标  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [OLE DB 自定义属性](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
 有关如何设置属性的详细信息，请单击下列主题之一：  
  
-   [通过使用 OLE DB 目标来加载数据](../../integration-services/data-flow/load-data-by-using-the-ole-db-destination.md)  
  
-   [设置数据流组件的属性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="ole-db-destination-editor-connection-manager-page"></a>OLE DB 目标编辑器（“连接管理器”页）
  使用 **“OLE DB 目标编辑器”** 对话框的 **“连接管理器”** 页可以为目标选择 OLE DB 连接。 使用此页还可以选择数据库中的表或视图。  
  
> [!NOTE]  
>  如果数据源是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007，则数据源需要一个不同于早期版本 Excel 的连接管理器。 有关详细信息，请参阅 [连接到 Excel 工作簿](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)。  
  
> [!NOTE]  
>  OLE DB 目标的 **CommandTimeout** 属性未在 **“OLE DB 目标编辑器”** 中提供，但可以使用 **“高级编辑器”** 进行设置。 另外，某些快速加载选项仅在 **“高级编辑器”** 中提供。 有关这些属性的详细信息，请参阅 [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md)的“OLE DB 目标”部分。  
  
### <a name="static-options"></a>静态选项  
 **“无缓存”**  
 从列表中选择一个现有连接管理器，或通过单击“新建”创建一个新连接。  
  
 **新建**  
 通过使用“配置 OLE DB 连接管理器”对话框创建一个新连接管理器。  
  
 **数据访问模式**  
 指定向目标中加载数据的方法。 加载双字节字符集 (DBCS) 数据需要使用一个快速加载选项。 有关针对大容量插入进行了优化的快速加载数据访问模式的详细信息，请参阅 [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)。  
  
|选项|描述|  
|------------|-----------------|  
|表或视图|将数据加载到 OLE DB 目标中的表或视图。|  
|表或视图 - 快速加载|将数据加载到 OLE DB 目标中的表或视图，并使用快速加载选项。 有关针对大容量插入进行了优化的快速加载数据访问模式的详细信息，请参阅 [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)。|  
|表名变量或视图名变量|在变量中指定表或视图名称。<br /><br /> **相关信息**：[在包中使用变量](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|表名变量或视图名变量 - 快速加载|在变量中指定表或视图名称，并使用快速加载选项加载数据。 有关针对大容量插入进行了优化的快速加载数据访问模式的详细信息，请参阅 [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)。|  
|SQL 命令|使用 SQL 查询将数据加载到 OLE DB 目标中。|  
  
 **预览**  
 使用“预览查询结果”对话框预览结果。 预览最多可以显示 200 行。  
  
### <a name="data-access-mode-dynamic-options"></a>数据访问模式动态选项  
 每个 **“数据访问模式”** 设置都显示一组特定于该设置的动态选项。 下面几节介绍对于每个 **“数据访问模式”** 设置均可用的所有动态选项。  
  
#### <a name="data-access-mode--table-or-view"></a>数据访问模式 = 表或视图  
 **表或视图的名称**  
 从数据源的可用表列表或视图列表中选择表或视图的名称。  
  
 **新建**  
 通过使用“创建表”对话框创建一个新表。  
  
> [!NOTE]  
>  单击 **“新建”** 时， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将基于所连接的数据源生成一条默认的 CREATE TABLE 语句。 即使源表包含一个已声明了 FILESTREAM 属性的列，此默认 CREATE TABLE 语句也不会包含 FILESTREAM 属性。 若要运行具有 FILESTREAM 属性的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件，首先要在目标数据库上实现 FILESTREAM 存储。 然后在 **“创建表”** 对话框中将 FILESTREAM 属性添加到 CREATE TABLE 语句中。 有关详细信息，请参阅[二进制大型对象 (Blob) 数据 (SQL Server)](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
#### <a name="data-access-mode--table-or-view---fast-load"></a>数据访问模式 = 表或视图 – 快速加载  
 **表或视图的名称**  
 使用此列表从数据库中选择表或视图，或单击“新建”创建新表。  
  
 **新建**  
 通过使用“创建表”对话框创建一个新表。  
  
> [!NOTE]  
>  单击 **“新建”** 时， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将基于所连接的数据源生成一条默认的 CREATE TABLE 语句。 即使源表包含一个已声明了 FILESTREAM 属性的列，此默认 CREATE TABLE 语句也不会包含 FILESTREAM 属性。 若要运行具有 FILESTREAM 属性的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件，首先要在目标数据库上实现 FILESTREAM 存储。 然后在 **“创建表”** 对话框中将 FILESTREAM 属性添加到 CREATE TABLE 语句中。 有关详细信息，请参阅[二进制大型对象 (Blob) 数据 (SQL Server)](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
 **保留标识**  
 指定加载数据时是否复制标识值。 仅在选择快速加载选项时，此属性才可用。 此属性的默认值为 **false**。  
  
 **保留 Null**  
 指定加载数据时是否复制 Null 值。 仅在选择快速加载选项时，此属性才可用。 此属性的默认值为 **false**。  
  
 **表锁**  
 指定加载期间是否锁定表。 此属性的默认值为 **true**。  
  
 **检查约束**  
 指定目标在加载数据时是否检查约束。 此属性的默认值为 **true**。  
  
 **每批行数**  
 指定每批中的行数。 此属性的默认值为 **-1**，表示尚未分配值。  
  
> [!NOTE]  
>  如果在“OLE DB 目标编辑器”中清空此文本框，则表示不希望为此属性分配自定义值。  
  
 **最大插入提交大小**  
 指定 OLE DB 目标在快速加载操作期间尝试提交的批大小。 值为 **0** 表示在处理完所有行之后以单批方式提交所有数据。  
  
> [!NOTE]  
>  如果该 OLE DB 目标和其他数据流组件正在更新同一源表，则 **0** 值可能导致正在运行的包停止响应。 若要防止包停止，请将 **“最大插入提交大小”** 选项设置为 **2147483647**。  
  
 如果为此属性提供一个值，目标将分批提交行，提交的行数是 (a) “最大插入提交大小”与 (b) 当前正在处理的缓冲区中的剩余行数中的较小者。  
  
> [!NOTE]  
>  目标中任何约束失败都将导致“最大插入提交大小”所定义的整批行失败。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>数据访问模式 = 表名变量或视图名变量  
 **变量名称**  
 选择包含表或视图名称的变量。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable---fast-load"></a>数据访问模式 = 表名变量或视图名变量 – 快速加载）  
 **变量名称**  
 选择包含表或视图名称的变量。  
  
 **新建**  
 通过使用“创建表”对话框创建一个新表。  
  
> [!NOTE]  
>  单击 **“新建”** 时， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将基于所连接的数据源生成一条默认的 CREATE TABLE 语句。 即使源表包含一个已声明了 FILESTREAM 属性的列，此默认 CREATE TABLE 语句也不会包含 FILESTREAM 属性。 若要运行具有 FILESTREAM 属性的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件，首先要在目标数据库上实现 FILESTREAM 存储。 然后在 **“创建表”** 对话框中将 FILESTREAM 属性添加到 CREATE TABLE 语句中。 有关详细信息，请参阅[二进制大型对象 (Blob) 数据 (SQL Server)](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
 **保留标识**  
 指定加载数据时是否复制标识值。 仅在选择快速加载选项时，此属性才可用。 此属性的默认值为 **false**。  
  
 **保留 Null**  
 指定加载数据时是否复制 Null 值。 仅在选择快速加载选项时，此属性才可用。 此属性的默认值为 **false**。  
  
 **表锁**  
 指定加载期间是否锁定表。 此属性的默认值为 **false**。  
  
 **检查约束**  
 指定任务是否检查约束。 此属性的默认值为 **false**。  
  
 **每批行数**  
 指定每批中的行数。 此属性的默认值为 **-1**，表示尚未分配值。  
  
> [!NOTE]  
>  如果在“OLE DB 目标编辑器”中清空此文本框，则表示不希望为此属性分配自定义值。  
  
 **最大插入提交大小**  
 指定 OLE DB 目标在快速加载操作期间尝试提交的批大小。 默认值为 **2147483647** ，表示在处理完所有行之后以单批方式提交所有数据。  
  
> [!NOTE]  
>  如果该 OLE DB 目标和其他数据流组件正在更新同一源表，则 **0** 值可能导致正在运行的包停止响应。 若要防止包停止，请将 **“最大插入提交大小”** 选项设置为 **2147483647**。  
  
#### <a name="data-access-mode--sql-command"></a>数据访问模式 = SQL 命令  
 **SQL 命令文本**  
 输入 SQL 查询的文本，通过单击“生成查询”来生成查询，或通过单击“浏览”定位到包含查询文本的文件。  
  
> [!NOTE]  
>  OLE DB 目标不支持参数。 如果需要执行参数化 INSERT 语句，请考虑使用 OLE DB 命令转换。 有关详细信息，请参阅 [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md)。  
  
 **生成查询**  
 使用“查询生成器”对话框可直观地构造 SQL 查询。  
  
 **“浏览”**  
 使用“打开”对话框可定位到包含 SQL 查询文本的文件。  
  
 **分析查询**  
 验证查询文本的语法。  
  
## <a name="ole-db-destination-editor-mappings-page"></a>OLE DB 目标编辑器（“映射”页）
  可以使用 **“OLE DB 目标编辑器”** 对话框的 **“映射”** 页，将输入列映射到目标列。  
  
### <a name="options"></a>选项  
 **可用输入列**  
 查看可用输入列的列表。 使用拖放操作可以将表中的可用输入列映射到目标列。  
  
 **可用目标列**  
 查看可用目标列的列表。 使用拖放操作可以将表中的可用目标列映射到输入列。  
  
 **输入列**  
 查看选定的输入列。 可以通过选择“\<忽略>”以从输出中排除列来移除映射。  
  
 **目标列**  
 查看每个可用目标列，而不管是否已对其进行映射。  
  
## <a name="ole-db-destination-editor-error-output-page"></a>OLE DB 目标编辑器（“错误输出”页）
  可以使用 **“OLE DB 目标编辑器”** 对话框的 **“错误输出”** 页指定错误处理选项。  
  
### <a name="options"></a>选项  
 **输入/输出**  
 查看输入的名称。  
  
 **列**  
 未使用。  
  
 **错误**  
 指定发生错误时应执行的操作：忽略失败、重定向行或使组件失败。  
  
 **相关主题：**[数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **截断**  
 未使用。  
  
 **Description**  
 查看操作的说明。  
  
 **将此值设置到选定的单元格**  
 指定发生错误或截断时应对所有选定单元格执行的操作：忽略失败、重定向行或使组件失败。  
  
 **应用**  
 将错误处理选项应用到选定的单元格。  
  
## <a name="related-content"></a>相关内容  
 [OLE DB 源](../../integration-services/data-flow/ole-db-source.md)  
  
 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)  
  
 [数据流](../../integration-services/data-flow/data-flow.md)  
  
  
