---
title: 执行 SQL 任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.executesqltask.f1
- sql13.dts.designer.executesqltask.general.f1
- sql13.dts.designer.executesqltask.parametermapping.f1
- sql13.dts.designer.executesqltask.resultset.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- batches [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: bebb2e8c-0410-43b2-ac2f-6fc80c8f2e9e
caps.latest.revision: 115
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 35cfefdbc23ef269579476c098d31825b319a41e
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35404749"
---
# <a name="execute-sql-task"></a>执行 SQL 任务
  执行 SQL 任务从包中运行 SQL 语句或存储过程。 此任务可以包含单个 SQL 语句，也可以包含按顺序运行的多个 SQL 语句。 可以将执行 SQL 任务用于下列用途：  
  
-   截断表或视图，以便为插入数据作准备。  
  
-   创建、更改和删除数据库对象（如表和视图）。  
  
-   在向事实数据表和维度表加载数据之前，重新创建这些表。  
  
-   运行存储过程。 如果 SQL 语句调用从临时表返回结果的某一存储过程，则使用 WITH RESULT SETS 选项可为结果集定义元数据。  
  
-   将查询返回的行集保存到变量中。  
  
 执行 SQL 任务可以与 Foreach 循环和 For 循环容器一起组合使用，以运行多个 SQL 语句。 这些容器在包中实现重复运行控制流，并可重复运行执行 SQL 任务。 例如，包可以使用 Foreach 循环容器来枚举文件夹中的文件，并重复运行执行 SQL 任务来执行存储在各个文件中的 SQL 语句。  
  
## <a name="connect-to-a-data-source"></a>连接到数据源  
 执行 SQL 任务可使用不同类型的连接管理器来连接到在其中运行 SQL 语句或存储过程的数据源。 此任务可使用下表中列出的连接类型。  
  
|连接类型|连接管理器|  
|---------------------|------------------------|  
|EXCEL|[Excel 连接管理器](../../integration-services/connection-manager/excel-connection-manager.md)|  
|OLE DB|[OLE DB 连接管理器](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|[ODBC 连接管理器](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|ADO|[ADO 连接管理器](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|[ADO.NET 连接管理器](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|SQLMOBILE|[SQL Server Compact Edition 连接管理器](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
  
## <a name="create-sql-statements"></a>创建 SQL 语句  
 此任务使用的 SQL 语句的源可以是包含语句的任务属性、到包含一个或多个语句的文件的连接，或者是包含语句的变量的名称。 必须用源数据库管理系统 (DBMS) 的方言编写 SQL 语句。 有关详细信息，请参阅 [Integration Services (SSIS) 查询](../../integration-services/integration-services-ssis-queries.md)。  
  
 如果 SQL 语句存储在某个文件中，则该任务使用文件连接管理器来连接到该文件。 有关详细信息，请参阅 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)。  
  
 在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中，可以使用 **“执行 SQL 任务编辑器”** 对话框来键入 SQL 语句，也可使用 **“查询生成器”**（用于创建 SQL 查询的图形用户界面）键入。 
  
> [!NOTE]  
>  执行 SQL 任务可能无法成功分析在执行 SQL 任务外编写的有效 SQL 语句。  
  
> [!NOTE]  
>  执行 SQL 任务将使用 **RecognizeAll** ParseMode 枚举值。 有关详细信息，请参阅 [ManagedBatchParser 命名空间](http://go.microsoft.com/fwlink/?LinkId=223617)。  
  
## <a name="send-multiple-statements-in-a-batch"></a>在批中发送多个语句  
 如果在执行 SQL 任务中包含了多个语句，则可以将这些语句进行分组，并将它们作为一批来运行。 若要标明批的结束，请使用 GO 命令。 在两个 GO 命令间的所有 SQL 语句都作为一批发送到 OLE DB 访问接口来运行。 SQL 命令可以包含多个由 GO 命令分隔的批。  
  
 对可以分组到批的 SQL 语句类型有一些限制。 有关详细信息，请参阅 [Batches of Statements](../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)。  
  
 如果执行 SQL 任务运行一个 SQL 语句批，则下列规则适用于批：  
  
-   只有一个语句可以返回结果集，且该语句必须是批中的第一个语句。  
  
-   如果结果集使用结果绑定，则查询必须返回相同数量的列。 如果查询返回不同数量的列，则任务失败。 但是，即使任务失败，其运行的查询（如 DELETE 或 INSERT 查询）也可能成功。  
  
-   如果结果绑定使用列名，则查询必须返回与任务中使用的结果集具有相同名称的列。 如果缺少列，则任务失败。  
  
-   如果任务使用参数绑定，则批中的所有查询都必须具有相同数量和类型的参数。  
  
## <a name="run-parameterized-sql-commands"></a>运行参数化 SQL 命令  
 SQL 语句和存储过程常常使用输入参数、输出参数和返回代码。 执行 SQL 任务支持 **Input**、 **Output**和 **ReturnValue** 参数类型。 应当将 **Input** 类型用于输入参数，将 **Output** 用于输出参数并将 **ReturnValue** 用于返回代码。  
  
> [!NOTE]  
>  只有数据访问接口支持这些参数时，才可在执行 SQL 任务中使用它们。  
  
## <a name="specify-a-result-set-type"></a>指定结果集类型  
 执行 SQL 任务可能有结果集返回也可能没有结果集返回，这取决于 SQL 命令的类型。 例如，SELECT 语句通常返回结果集，而 INSERT 语句通常不返回结果集。 SELECT 语句所返回的结果集可包含零行、单行或多行。 存储过程还可返回指示过程的执行状态的整数值（称为返回代码）。 这种情况下，结果集由单行组成。  
  
## <a name="configure-the-execute-sql-task"></a>配置执行 SQL 任务  
 可以按照下列方式配置执行 SQL 任务：  
  
-   指定用于连接到数据库的连接管理器的类型。  
  
-   指定 SQL 语句返回的结果集的类型。  
  
-   指定 SQL 语句的超时值。  
  
-   指定 SQL 语句的源。  
  
-   指明任务是否跳过 SQL 语句的准备阶段。  
  
-   如果使用 ADO 连接类型，则必须指明 SQL 语句是否为存储过程。 对于其他的连接类型，该属性为只读且其值始终为 **false**。  
  
 可以采用编程方式或通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器来设置属性。  

## <a name="general-page---execute-sql-task-editor"></a>“常规”页 - 执行 SQL 任务编辑器
 可以使用 **“执行 SQL 任务编辑器”** 对话框的 **“常规”** 页，配置执行 SQL 任务以及提供任务运行的 SQL 语句。  

若要了解关于 Transact-SQL 查询语言的详细信息，请参阅 [Transact-SQL 引用（数据库引擎）](../../t-sql/transact-sql-reference-database-engine.md)。  
  
### <a name="static-options"></a>静态选项  
 **名称**  
 为工作流中的执行 SQL 任务提供唯一的名称。 所提供的名称将在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中显示。  
  
 **Description**  
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
 将此属性设置为 **Allowed**时，“执行 SQL 任务”会尝试将输出参数和查询结果转换为结果赋值给的变量的数据类型。 这适用于 **单行** 结果集类型。  
  
 **ResultSet**  
 指定运行 SQL 语句预期的结果类型。 从 **“单行”**、 **“完整结果集”**、 **XML**或 **“无”** 中选择。  
  
 **ConnectionType**  
 选择连接数据源要使用的连接管理器的类型。 可用的连接类型包括 **OLE DB**、 **ODBC**、 **ADO**、 **ADO.NET** 和 **SQLMOBILE**。  
  
 **相关主题：**[OLE DB 连接管理器](../../integration-services/connection-manager/ole-db-connection-manager.md)、[ODBC 连接管理器](../../integration-services/connection-manager/odbc-connection-manager.md)、[ADO 连接管理器](../../integration-services/connection-manager/ado-connection-manager.md)、[ADO.NET 连接管理器](../../integration-services/connection-manager/ado-net-connection-manager.md)、[SQL Server Compact Edition 连接管理器](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)  
  
 **“连接”**  
 从已定义的连接管理器的列表中选择连接。 要创建新连接，请选择“\<新建连接...>”。  
  
 **SQLSourceType**  
 选择任务运行的 SQL 语句的源类型。  
  
 根据执行 SQL 任务所用的连接管理器类型，必须在参数化 SQL 语句中使用特定的参数标记。    
  
 此属性具有下表所列的选项。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接输入**|将源设置为某个 Transact-SQL 语句。 选择此值将显示动态选项 **SQLStatement**。|  
|**文件连接**|选择包含 Transact-SQL 语句的文件。 设置此选项将显示动态选项 **FileConnection**。|  
|**变量**|将源设置为定义 Transact-SQL 语句的变量。 选择此值将显示动态选项 **SourceVariable**。|  
  
 **QueryIsStoredProcedure**  
 指示要运行的指定 SQL 语句是否为存储过程。 只有当任务使用 ADO 连接管理器时，此属性才是可读/写的。 否则该属性为只读，其值为 **false**。  
  
 **BypassPrepare**  
 指示 SQL 语句是否已准备就绪。  如果为**true** ，则跳过准备过程；如果为 **false** ，则在运行 SQL 语句前准备 SQL 语句。 此选项仅可用于支持准备的 OLE DB 连接。  
  
 **相关主题：**[准备好的执行](../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
 **“浏览”**  
 使用“打开”对话框定位包含 SQL 语句的文件。 选择一个文件，将文件内容作为 SQL 语句复制到 **SQLStatement** 属性中。  
  
 **生成查询**  
 使用“查询生成器”对话框创建 SQL 语句，查询生成器是一种用于创建查询的图形工具。 此选项在 **SQLSourceType** 选项设置为 **“直接输入”** 时可用。  
  
 **分析查询**  
 验证 SQL 语句的语法。  
  
### <a name="sqlsourcetype-dynamic-options"></a>SQLSourceType 动态选项  
  
#### <a name="sqlsourcetype--direct-input"></a>SQLSourceType = 直接输入  
 **SQLStatement**  
 在选项框中键入要执行的 SQL 语句，或者单击“浏览(…)”按钮，在“输入 SQL 查询”对话框中键入 SQL 语句，还可以单击“生成查询”，使用“查询生成器”对话框编写 SQL 语句。  
  
 **相关主题：** [“查询生成器”](http://msdn.microsoft.com/library/780752c9-6e3c-4f44-aaff-4f4d5e5a45c5)  
  
#### <a name="sqlsourcetype--file-connection"></a>SQLSourceType = 文件连接  
 **文件连接**  
 选择现有文件连接管理器，或单击“\<新建连接...>”，创建新的连接管理器。  
  
 **相关主题：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="sqlsourcetype--variable"></a>SQLSourceType = 变量  
 **SourceVariable**  
 选择现有变量，或单击“\<新建变量...>”，创建一个新变量。  
  
 **相关主题：**[Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)、[添加变量](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
 
## <a name="parameter-mapping-page---execute-sql-task-editor"></a>“参数映射”页 - 执行 SQL 任务编辑器
可以使用 **“执行 SQL 任务编辑器”** 对话框的 **“参数映射”** 页，将变量映射到 SQL 语句中的参数。  
  
### <a name="options"></a>“常规”  
 **“变量名称”**  
 通过单击“添加”添加了参数映射之后，请从列表中选择系统变量或用户定义的变量，或单击“\<新建变量...>”以使用“添加变量”对话框添加新变量。  
  
 **相关主题：**[Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)  
  
 **方向**  
 选择参数的方向。 将每个变量映射到输入参数、输出参数或返回代码。  
  
 **数据类型**  
 选择参数的数据类型。 可用数据类型的列表取决于您为任务所用的连接管理器选择的访问接口。  
  
 **参数名称**  
 提供参数名称。  
  
 必须使用数值还是参数名称取决于任务所用的连接管理器类型。 某些连接管理器类型要求参数名称的第一个字符为 @ 符号，并要求将 @Param1 之类的特定名称或列名作为参数名称。  
  
 **参数大小**  
 提供具有可变长度的参数的大小，如字符串和二进制字段。  
  
 此设置可确保访问接口为长度可变的参数值分配足够的空间。  
  
 **“添加”**  
 单击此项可添加参数映射。  
  
 **删除**  
 选择列表中的参数映射，再单击“删除”。  
 
## <a name="result-set-page---execute-sql-task-editor"></a>“结果集”页 - 执行 SQL 任务编辑器
可以使用 **“执行 SQL 任务编辑器”** 对话框的 **“结果集”** 页，将 SQL 语句的结果映射到新变量或现有变量。 如果将“常规”页上的 **ResultSet** 设置为 **“无”**，将禁用此对话框中的选项。  
  
### <a name="options"></a>“常规”  
 **结果名称**  
 通过单击“添加”添加了结果集映射集之后，为结果提供名称。 必须根据结果集类型使用特定的结果名称。  
  
 如果结果集的类型为“单行” ，则可以使用由查询返回的列的名称，也可以使用代表列在查询所返回列的列表中位置的数字。  
  
 如果结果集类型为“完整结果集”  或 **XML**，则必须使用 0 作为结果集名称。  
 
  
 **“变量名称”**  
 通过选择变量或单击“\<新建变量...>”使用“添加变量”对话框添加新的变量，将结果集映射到变量。  
  
 **“添加”**  
 单击此项可以添加结果集映射。  
  
 **删除**  
 在列表中选择结果集映射，再单击“删除”。  
 
## <a name="parameters-in-the-execute-sql-task"></a>执行 SQL 任务中的参数
SQL 语句和存储过程常常使用 **input** 参数、 **output** 参数和返回代码。 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中，执行 SQL 任务支持 **Input**、**Output** 和 **ReturnValue** 参数类型。 应当将 **Input** 类型用于输入参数，将 **Output** 用于输出参数并将 **ReturnValue** 用于返回代码。  
  
> [!NOTE]  
>  只有数据访问接口支持这些参数时，才可在执行 SQL 任务中使用它们。  
  
 SQL 命令（包括查询和存储过程）中的参数被映射到在执行 SQL 任务作用域、父容器或包的作用域内创建的用户定义变量。 变量的值可在设计时设置，也可在运行时动态填充。 还可以将参数映射到系统变量。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)和[系统变量](../../integration-services/system-variables.md)。  
  
 但是，在执行 SQL 任务中使用参数和返回代码不只是要了解该任务支持的参数类型以及如何映射这些参数。 还有其他使用要求和准则可帮助您在执行 SQL 任务中成功使用参数和返回代码。 本主题的其余部分将介绍这些使用要求和准则：  
  
-   [使用参数名称和标记](#Parameter_names_and_markers)  
  
-   [将参数用于日期和时间数据类型](#Date_and_time_data_types)  
  
-   [在 WHERE 子句中使用参数](#WHERE_clauses)  
  
-   [在存储过程中使用参数](#Stored_procedures)  
  
-   [获取返回代码的值](#Return_codes)    
  
###  <a name="Parameter_names_and_markers"></a>参数名称和标记  
 执行 SQL 任务使用不同的连接类型时，SQL 命令的语法使用不同的参数标记。 例如，[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器类型要求 SQL 命令使用格式为 @varParameter 的参数标记，而 OLE DB 连接类型要求使用问号 (?) 参数标记。  
  
 在变量与参数之间的映射中可以用作参数名的名称也因连接管理器类型而异。 例如，[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器类型使用带 @ 前缀的用户定义名称，而 OLE DB 连接管理器类型要求使用从 0 开始的序数数值作为参数名。  
  
 下表总结了执行 SQL 任务可以使用的连接管理器类型的 SQL 命令要求。  
  
|连接类型|参数标记|参数名称|示例 SQL 命令|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO|?|Param1, Param2, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|@\<参数名称>|@\<参数名称>|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = @parmContactID|  
|ODBC|?|1, 2, 3, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL 和 OLE DB|?|0, 1, 2, 3, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
#### <a name="use-parameters-with-adonet-and-ado-connection-managers"></a>在 ADO.NET 和 ADO 连接管理器中使用参数  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 和 ADO 连接管理器对使用参数的 SQL 命令有特定要求：  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器要求 SQL 命令将参数名称用作参数标记。 这意味着变量可以直接映射到参数。 例如，变量 `@varName` 映射到名为 `@parName` 的参数，并向参数 `@parName`提供值。  
  
-   ADO 连接管理器要求 SQL 命令将问号 (?) 用作参数标记。 但是，您可以使用任何用户定义名称（整数值除外）作为参数名称。  
  
 为了向参数提供值，可将变量映射到参数名称。 然后，执行 SQL 任务使用参数列表中参数名称的序数值来将值从变量加载到参数。  
  
#### <a name="use-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>在 EXCEL、ODBC 和 OLE DB 连接管理器中使用参数  
 EXCEL、ODBC 和 OLE DB 连接管理器要求 SQL 命令使用问号 (?) 作为参数标记，并且使用从 0 开始或从 1 开始的数值作为参数名称。 如果执行 SQL 任务使用 ODBC 连接管理器，则映射到查询中的第一个参数的参数名称将为 1；否则该参数将命名为 0。 对于后续参数，参数名称的数值指示参数名称在 SQL 命令中映射到的参数。 例如，名为 3 的参数映射到第三个参数，这是由 SQL 命令中的第三个问号 (?) 来表示的。  
  
 若要向参数提供值，可以将变量映射到参数名称，然后执行 SQL 任务使用参数名称的序数值将值从变量加载到参数。  
  
 连接管理器使用的访问接口不同时，某些 OLE DB 数据类型可能不受支持。 例如，Excel 驱动程序只识别有限的一组数据类型。 有关带有 Excel 驱动程序的 Jet 访问接口的行为的详细信息，请参阅 [Excel Source](../../integration-services/data-flow/excel-source.md)。  
  
#### <a name="use-parameters-with-ole-db-connection-managers"></a>在 OLE DB 连接管理器中使用参数  
 如果执行 SQL 任务使用 OLE DB 连接管理器，则该任务的 BypassPrepare 属性可用。 如果执行 SQL 任务使用带有参数的 SQL 语句，则应将此属性设置为 **true** 。  
  
 使用 OLE DB 连接管理器时，不能使用参数化的子查询，这是因为执行 SQL 任务不能通过 OLE DB 访问接口得到参数信息。 但是，您可以使用表达式将参数值串联到查询字符串中，并设置该任务的 SqlStatementSource 属性。  
  
###  <a name="Date_and_time_data_types"></a>将参数用于日期和时间数据类型  
  
#### <a name="use-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>在 ADO.NET 和 ADO 连接管理器中使用日期和时间参数  
 读取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型、**time** 和 **datetimeoffset** 数据时，使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 或 ADO 连接管理器的执行 SQL 任务有以下附加要求：  
  
-   对于 **time** 数据，[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器要求此数据存储在参数类型为 **Input** 或 **Output** 并且数据类型为 **string** 的参数中。  
  
-   对于 **datetimeoffset** 数据，[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器要求此数据存储在下列参数之一中：  
  
    -   参数类型为 **Input** 并且数据类型为 **string**的参数。  
  
    -   参数类型为 **Output** 或 **ReturnValue**并且数据类型为 **datetimeoffset**、 **string**或 **datetime2**的参数。 如果选择数据类型为 **string** 或 **datetime2** 的参数，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会将数据转换为 string 或 datetime2。  
  
-   ADO 连接管理器要求 **time** 或 **datetimeoffset** 数据存储在参数类型为 **Input** 或 **Output**并且数据类型为 **adVarWchar**的参数中。  
  
 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型和它们如何映射到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型的详细信息，请参阅[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md) 和 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
#### <a name="use-date-and-time-parameters-with-ole-db-connection-managers"></a>在 OLE DB 连接管理器中使用日期和时间参数  
 使用 OLE DB 连接管理器时，执行 SQL 任务对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型为 **date**、**time**、**datetime**、**datetime2** 和 **datetimeoffset** 的数据有特定的存储要求。 您必须用下列参数类型之一来存储此数据：  
  
-   NVARCHAR 数据类型的输入参数。  
  
-   具有相应数据类型的输出参数，如下表中所示。  
  
    |**Output** 参数类型|Date 数据类型|  
    |-------------------------------|--------------------|  
    |DBDATE|**date**|  
    |DBTIME2|**time**|  
    |DBTIMESTAMP|**datetime**、 **datetime2**|  
    |DBTIMESTAMPOFFSET|**datetimeoffset**|  
  
 如果数据未存储在相应的输入或输出参数中，包将失败。  
  
#### <a name="use-date-and-time-parameters-with-odbc-connection-managers"></a>在 ODBC 连接管理器中使用日期和时间参数  
 使用 ODBC 连接管理器时，执行 SQL 任务对于带有以下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型之一的数据具有特定的存储要求：**date**、**time**、**datetime**、**datetime2** 或 **datetimeoffset**。 您必须用下列参数类型之一来存储此数据：  
  
-   SQL_WVARCHAR 数据类型的 **Input** 参数  
  
-   具有适当数据类型的 **output** 参数，如下表中所示。  
  
    |**Output** 参数类型|Date 数据类型|  
    |-------------------------------|--------------------|  
    |SQL_DATE|**date**|  
    |SQL_SS_TIME2|**time**|  
    |SQL_TYPE_TIMESTAMP<br /><br /> -或 -<br /><br /> SQL_TIMESTAMP|**datetime**、 **datetime2**|  
    |SQL_SS_TIMESTAMPOFFSET|**datetimeoffset**|  
  
 如果数据未存储在相应的输入或输出参数中，包将失败。  
  
###  <a name="WHERE_clauses"></a>在 WHERE 子句中使用参数  
 SELECT、INSERT、UPDATE 和 DELETE 命令经常包含 WHERE 子句以指定筛选器，这些筛选器定义源表中的每行要用于 SQL 命令所必须满足的条件。 参数在 WHERE 子句中提供筛选值。  
  
 可以使用参数标记来动态提供参数值。 可以在 SQL 语句中使用哪些参数标记和参数名称的规则取决于执行 SQL 所使用的连接管理器的类型。  
  
 下表按连接管理器类型列出了 SELECT 命令的示例。 INSERT、UPDATE 和 DELETE 语句相似。 示例使用 SELECT 返回 **的** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 表中 **ProductID** 大于且小于由两个参数指定的值的产品。  
  
|连接类型|SELECT 语法|  
|---------------------|-------------------|  
|EXCEL、ODBC 和 OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 这些示例要求使用具有以下名称的参数：  
  
-   EXCEL 和 OLED DB 连接管理器使用参数名称 0 和 1。 ODBC 连接类型使用 1 和 2。  
  
-   ADO 连接类型可以使用任何两个参数名称，例如 Param1 和 Param2，但是这两个参数必须按其在参数列表中的序数位置进行映射。  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接类型使用参数名称 @parmMinProductID 和 @parmMaxProductID。  
  
###  <a name="Stored_procedures"></a>在存储过程中使用参数  
 运行存储过程的 SQL 命令也可以使用参数映射。 与参数化查询的规则一样，参数标记和参数名称的使用规则取决于执行 SQL 所使用的连接管理器的类型。  
  
 下表按连接管理器类型列出了 EXEC 命令的示例。 示例运行 **中的** uspGetBillOfMaterials [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]存储过程。 该存储过程使用 `@StartProductID` 和 `@CheckDate` **Input** 参数。  
  
|连接类型|EXEC 语法|  
|---------------------|-----------------|  
|EXCEL 和 OLEDB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> 有关 ODBC 调用语法的详细信息，请参阅 MSDN Library 中的 ODBC 程序员参考的 [Procedure Parameters](http://go.microsoft.com/fwlink/?LinkId=89462)（过程参数）主题。|  
|ADO|如果 IsQueryStoredProcedure 设置为 False，则为 `EXEC uspGetBillOfMaterials ?, ?`<br /><br /> 如果 IsQueryStoredProcedure 设置为 True，则为 `uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|如果 IsQueryStoredProcedure 设置为 False，则为 `EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> 如果 IsQueryStoredProcedure 设置为 True，则为 `uspGetBillOfMaterials`|  
  
 若要使用输出参数，则语法要求在每个参数标记后跟 OUTPUT 关键字。 例如，以下 output 参数语法是正确的： `EXEC myStoredProcedure ? OUTPUT`。  
  
 有关在 Transact-SQL 存储过程中使用输入和输出参数的详细信息，请参阅 [EXECUTE (Transact-SQL)](../../t-sql/language-elements/execute-transact-sql.md)。  
 
### <a name="map-query-parameters-to-variables"></a>将查询参数映射到变量
本节介绍如何在执行 SQL 任务中使用参数化 SQL 语句以及如何在 SQL 语句的变量和参数之间创建映射。  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开要使用的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  如果该包尚未包括执行 SQL 任务，则向该包的控制流中添加一个此类任务。 有关详细信息，请参阅 [在控制流中添加或删除任务或容器](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)。  
  
5.  双击执行 SQL 任务。  
  
6.  以下列方式之一提供参数化 SQL 命令：  
  
    -   在 SQLStatement 属性中使用直接输入并键入 SQL 命令。  
  
    -   使用直接输入，单击 **“生成查询”**，然后使用查询生成器提供的图形工具创建 SQL 命令。  
  
    -   使用文件连接，然后引用包含该 SQL 命令的文件。  
  
    -   使用变量，然后引用包含该 SQL 命令的变量。  
  
     参数化 SQL 语句中使用的参数标记取决于执行 SQL 任务所使用的连接类型。  
  
    |连接类型|参数标记|  
    |---------------------|----------------------|  
    |ADO|?|  
    |ADO.NET 和 SQLMOBILE|@\<参数名称>|  
    |ODBC|?|  
    |EXCEL 和 OLE DB|?|  
  
     下表按连接管理器类型列出了 SELECT 命令的示例。 参数在 WHERE 子句中提供筛选值。 示例使用 SELECT 返回 **的** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 表中 **ProductID** 大于且小于由两个参数指定的值的产品。  
  
    |连接类型|SELECT 语法|  
    |---------------------|-------------------|  
    |EXCEL、ODBC 和 OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
   
7.  单击 **“参数映射”**。  
  
8.  若要添加参数映射，请单击 **“添加”**。  
  
9. 在 **“参数名称”** 框中提供名称。  
  
     所使用的参数名称取决于执行 SQL 任务所使用的连接类型。  
  
    |连接类型|“参数名称”|  
    |---------------------|--------------------|  
    |ADO|Param1, Param2, …|  
    |ADO.NET 和 SQLMOBILE|@\<参数名称>|  
    |ODBC|1, 2, 3, …|  
    |EXCEL 和 OLE DB|0, 1, 2, 3, …|  
  
10. 从 **“变量名称”** 列表中选择变量。 有关详细信息，请参阅 [添加、删除、更改包中用户定义变量的作用域](http://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e)。  
  
11. 在 **“方向”** 列表中指定该参数是输入、输出还是返回值。  
  
12. 在 **“数据类型”** 列表中，设置该参数的数据类型。  
  
    > [!IMPORTANT]  
    >  参数的数据类型必须与变量的数据类型兼容。  
  
13. 对 SQL 语句中的每个参数重复步骤 8 到 11。  
  
    > [!IMPORTANT]  
    >  参数映射的顺序必须与参数在 SQL 语句中出现的顺序相同。  
  
14. 单击“确定” 。  

##  <a name="Return_codes"></a>获取返回代码的值  
 存储过程可以返回一个整数值（称为“返回代码”），以指示过程的执行状态。 若要在执行 SQL 任务中实现返回代码，需要使用 **ReturnValue** 类型的参数。  
  
 下表按连接类型列出了实现返回代码的某些 EXEC 命令示例。 所有示例均使用 **input** 参数。 对于所有参数类型（**Input**、 **Output**和 **ReturnValue**），参数标记和参数名称的使用规则都相同。  
  
 某些语法不支持参数文字。 在此情况下，必须通过使用变量来提供参数值。  
  
|连接类型|EXEC 语法|  
|---------------------|-----------------|  
|EXCEL 和 OLEDB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> 有关 ODBC 调用语法的详细信息，请参阅 MSDN Library 中的 ODBC 程序员参考的 [Procedure Parameters](http://go.microsoft.com/fwlink/?LinkId=89462)（过程参数）主题。|  
|ADO|如果 IsQueryStoreProcedure 设置为 False，则为 `EXEC ? = myStoredProcedure 1`<br /><br /> 如果 IsQueryStoreProcedure 设置为 True，则为 `myStoredProcedure`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|将 IsQueryStoreProcedure 设置为 **True**。<br /><br /> `myStoredProcedure`|  
  
 如上表中语法所示，执行 SQL 任务使用 **“直接输入”** 源类型来运行存储过程。 执行 SQL 任务还可以使用 **“文件连接”** 源类型来运行存储过程。 无论执行 SQL 任务是使用 **“直接输入”** 源类型还是使用 **“文件连接”** 源类型，都请使用 **ReturnValue** 类型的参数来实现返回代码。
  
 有关在 Transact-SQL 存储过程中使用返回代码的详细信息，请参阅 [RETURN (Transact-SQL)](../../t-sql/language-elements/return-transact-sql.md)。  
  
## <a name="result-sets-in-the-execute-sql-task"></a>执行 SQL 任务中的结果集
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包中，结果集是否返回到执行 SQL 任务取决于该任务使用的 SQL 命令的类型。 例如，SELECT 语句通常返回结果集，而 INSERT 语句通常不返回结果集。  
  
 结果集所包含的内容也因 SQL 命令而异。 例如，SELECT 语句所返回的结果集可包含零行、单行或多行。 但返回计数或总和的 SELECT 语句所返回的结果集仅包含单个行。  
  
 在执行 SQL 任务中使用结果集不只是要了解 SQL 命令是否返回结果集，以及结果集所包含的内容。 还有其他使用要求和准则可帮助您在执行 SQL 任务中成功使用结果集。 本主题的其余部分将介绍这些使用要求和准则：  
  
-   [指定结果集类型](#Result_set_type)  
  
-   [使用结果集填充变量](#Populate_variable_with_result_set)  
  
###  <a name="Result_set_type"></a>指定结果集类型  
 执行 SQL 任务支持下列结果集类型：  
  
-   查询不返回结果时使用的 **“无”** 结果集。 例如，该结果集用于在表中添加、更改和删除记录的查询。  
  
-   查询仅返回一行时使用的 **“单行”** 结果集。 例如，该结果集用于返回计数或总和的 SELECT 语句。  
  
-   查询返回多行时使用的 **“完整结果集”** 结果集。 例如，该结果集用于可检索表中所有行的 SELECT 语句。  
  
-   查询返回 XML 格式的结果集时使用的 **“XML”** 结果集。 例如，该结果集用于包含 FOR XML 子句的 SELECT 语句。  
  
 如果“执行 SQL 任务”使用了 **“完整结果集”** 结果集并且查询返回多个行集，则该任务仅返回第一个行集。 如果该行集生成一个错误，则该任务将报告这个错误。 如果其他行集生成错误，则该任务不会报告这些错误。  
  
###  <a name="Populate_variable_with_result_set"></a>使用结果集填充变量  
 如果结果集类型为单行、行集或 XML，则可以将查询返回的结果集绑定到用户定义的变量。  
  
 如果结果集类型为“单行” ，则可以使用列名作为结果集名称，将返回结果中的列绑定到一个变量，也可以使用列列表中列的序号位置作为结果集名称。 例如，查询 `SELECT Color FROM Production.Product WHERE ProductID = ?` 的结果集名称可以是 **Color** 或 **0**。 如果查询返回多个列，而您要访问所有列中的值，则必须将每列绑定到一个不同的变量。 如果使用数字作为结果集名称，将列映射到变量，则数字将反映列在查询的列列表中显示的顺序。 例如，在查询 `SELECT Color, ListPrice, FROM Production.Product WHERE ProductID = ?`中，对 **Color** 列使用 0，对 **ListPrice** 列使用 1。 使用列名作为结果集名称的功能将依赖于所配置任务要使用的访问接口。 并非所有访问接口都使列名可用。  
  
 某些返回单个值的查询可能不包括列名称。 例如，语句 `SELECT COUNT (*) FROM Production.Product` 不返回列名称。 可以使用序数位置 0 作为结果名称来访问返回结果。 要按列名称访问返回结果，则查询必须包括 AS \<别名> 子句来提供列名称。 语句 `SELECT COUNT (*)AS CountOfProduct FROM Production.Product`提供 **CountOfProduct** 列。 然后可以使用 **CountOfProduct** 列名称或序数位置 0 来访问返回结果列。  
  
 如果结果集类型为“完整结果集”  或 **XML**，则必须使用 0 作为结果集名称。  
  
 当您将一个变量映射到结果集类型为“单行”  的结果集时，该变量的数据类型必须与该结果集包含的列的数据类型兼容。 例如，如果结果集包含 **String** 数据类型的列，则它不能映射到 numeric 数据类型的变量。 在您将 **TypeConversionMode** 属性设置为 **Allowed**时，“执行 SQL 任务”将尝试将输出参数和查询结果转换为结果赋值给的变量的数据类型。  
  
 XML 结果集只能映射到数据类型为 **String** 或 **Object** 的变量。 如果该变量的数据类型为 **String** ，则“执行 SQL 任务”返回一个字符串，并且 XML 源可以使用 XML 数据。 如果该变量的数据类型为 **Object** ，则“执行 SQL 任务”返回一个文档对象模型 (DOM) 对象。  
  
 **完整结果集** 必须映射到数据类型为 **Object** 的变量。 返回结果是一个行集对象。 可以使用 Foreach 循环容器将存储在对象变量中的表行值提取到包变量中，然后使用脚本任务将存储在包变量中的数据写入文件。 有关如何使用 Foreach 循环容器和脚本任务执行该操作的演示，请参阅 msftisprodsamples.codeplex.com 上的 CodePlex 示例： [执行 SQL 参数和结果集](http://go.microsoft.com/fwlink/?LinkId=157863)。  
  
 下表总结了可以映射到结果集的变量数据类型。  
  
|结果集类型|变量的数据类型|对象的类型|  
|---------------------|---------------------------|--------------------|  
|“单行”|与结果集中的类型列兼容的任意类型。|不适用|  
|“完整结果集”|**对象**|如果任务使用本机连接管理器（包括 ADO、OLE DB、Excel 和 ODBC 连接管理器），则返回的对象为 ADO **Recordset**。<br /><br /> 如果任务使用托管连接管理器（如 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器），则返回的对象为 **System.Data.DataSet**。<br /><br /> 您可以使用脚本任务访问 **System.Data.DataSet** 对象，如下面的示例中所示。<br /><br /> `Dim dt As Data.DataTable`<br /><br /> `Dim ds As Data.DataSet = CType(Dts.Variables("Recordset").Value, DataSet) dt = ds.Tables(0)`|  
|XML|**String**|**String**|  
|XML|**对象**|如果任务使用本机连接管理器（包括 ADO、OLE DB、Excel 和 ODBC 连接管理器），则返回的对象为 **MSXML6.IXMLDOMDocument**。<br /><br /> 如果任务使用托管连接管理器（如 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器），则返回的对象为 **System.Xml.XmlDocument**。|  
  
 您可在执行 SQL 任务作用域或包作用域内定义变量。 如果变量的作用域为包，则结果集可用于包中的其他任务和容器，并可用于执行包或执行 DTS 2000 包任务所运行的所有包。  
  
 如果将变量映射到“单行”  结果集，则在满足以下条件时，SQL 语句返回的非字符串值将转换为字符串：  
  
-   **TypeConversionMode** 属性设置为 true。 在属性窗口中或通过使用“执行 SQL 任务编辑器” 设置属性值。  
  
-   转换不会导致数据截断。  
  
## <a name="map-result-sets-to-variables-in-an-execute-sql-task"></a>在执行 SQL 任务中将结果集映射到变量
本节介绍如何在执行 SQL 任务中创建结果集和变量之间的映射。 将结果集映射到变量以便使结果集对包中其他元素可用。 例如，脚本任务中的脚本可以读取该变量，然后使用结果集中的值，或者 XML 源可以使用集存储在变量中的结果。 如果结果集是由父包生成的，那么通过将结果集映射到父包中的变量，然后在子包中创建父包变量配置以存储父变量值，就可以使结果集对执行包任务所调用的子包可用。  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在“解决方案资源管理器”中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  如果该包尚未包括执行 SQL 任务，则向该包的控制流中添加一个此类任务。 有关详细信息，请参阅 [在控制流中添加或删除任务或容器](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)。  
  
5.  双击执行 SQL 任务。  
  
6.  在 **“执行 SQL 任务编辑器”** 对话框中的 **“常规”** 页上，选择 **“单行”**、 **“完整结果集”** 或 **XML** 结果集类型。  

7.  单击 **“结果集”**。  
  
8.  若要添加结果集映射，请单击 **“添加”**。  
  
9. 从 **“变量名称”** 列表中，选择变量或创建新变量。 有关详细信息，请参阅 [添加、删除、更改包中用户定义变量的作用域](http://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e)。  
  
10. 在 **“结果名称”** 列表中，可根据需要修改结果集的名称。  
  
     通常，可以将列名用作结果集名称，也可以将列列表中的列的序号位置用作结果集名称。 使用列名作为结果集名称的功能将依赖于配置任务要使用的访问接口。 并非所有访问接口都使列名可用。  
  
11. 单击“确定” 。  

## <a name="troubleshoot-the-execute-sql-task"></a>执行 SQL 任务故障排除  
 可以记录执行 SQL 任务对外部数据访问接口的调用。 您可以使用这项日志记录功能对执行 SQL 任务运行的 SQL 命令进行故障排除。 若要记录执行 SQL 任务对外部数据访问接口的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅[包执行的疑难解答工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
 有时，SQL 命令或存储过程会返回多个结果集。 这些结果集不仅包含 **SELECT** 查询结果的行集，还包含 **RAISERROR** 或 **PRINT** 语句的错误结果的单个值。 该任务是否忽略第一个结果集之后出现的结果集中的错误，取决于所用的连接管理器类型：  
  
-   在您使用 OLE DB 和 ADO 连接管理器时，该任务会忽略在第一个结果集之后出现的结果集。 因此，使用这些连接管理器，当错误不属于第一个结果集时，该任务会忽略 SQL 命令或存储过程返回的错误。  
  
-   在您使用 ODBC 和 ADO.NET 连接管理器时，该任务不会忽略在第一个结果集之后出现的结果集。 使用这些连接管理器，当第一个结果集以外的结果集中包含错误时，该任务将失败并出现错误。  
  
### <a name="custom-log-entries"></a>自定义日志项  
 下表介绍了执行 SQL 任务的自定义日志项。 有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|日志项|描述|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|提供有关 SQL 语句的执行阶段的信息。 在任务获得与数据库的连接时、任务开始准备 SQL 语句时以及执行完 SQL 语句之后写入日志项。 准备阶段的日志条目包括任务所使用的 SQL 语句。|  

