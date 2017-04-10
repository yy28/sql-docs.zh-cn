---
title: "执行 SQL 任务 | Microsoft Docs"
ms.custom: 
  - "ssisdev020617"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.executesqltask.f1"
  - "sql13.dts.designer.executesqltask.general.f1"
  - "sql13.dts.designer.executesqltask.parametermapping.f1"
  - "sql13.dts.designer.executesqltask.resultset.f1"
helpviewer_keywords: 
  - "Transact-SQL 语句, SSIS"
  - "语句 [Integration Services]"
  - "批处理 [Integration Services]"
  - "执行 SQL 任务 [Integration Services]"
ms.assetid: bebb2e8c-0410-43b2-ac2f-6fc80c8f2e9e
caps.latest.revision: 115
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 113
---
# 执行 SQL 任务
  执行 SQL 任务从包中运行 SQL 语句或存储过程。 此任务可以包含单个 SQL 语句，也可以包含按顺序运行的多个 SQL 语句。 可以将执行 SQL 任务用于下列用途：  
  
-   截断表或视图，以便为插入数据作准备。  
  
-   创建、更改和删除数据库对象（如表和视图）。  
  
-   在向事实数据表和维度表加载数据之前，重新创建这些表。  
  
-   运行存储过程。 如果 SQL 语句调用从临时表返回结果的某一存储过程，则使用 WITH RESULT SETS 选项可为结果集定义元数据。  
  
-   将查询返回的行集保存到变量中。  
  
 执行 SQL 任务可以与 Foreach 循环和 For 循环容器一起组合使用，以运行多个 SQL 语句。 这些容器在包中实现重复运行控制流，并可重复运行执行 SQL 任务。 例如，包可以使用 Foreach 循环容器来枚举文件夹中的文件，并重复运行执行 SQL 任务来执行存储在各个文件中的 SQL 语句。  
  
## 连接数据源  
 执行 SQL 任务可使用不同类型的连接管理器来连接到在其中运行 SQL 语句或存储过程的数据源。 此任务可使用下表中列出的连接类型。  
  
|连接类型|连接管理器|  
|---------------------|------------------------|  
|EXCEL|[Excel 连接管理器](../../integration-services/connection-manager/excel-connection-manager.md)|  
|OLE DB|[OLE DB 连接管理器](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|[ODBC 连接管理器](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|ADO|[ADO 连接管理器](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|[ADO.NET 连接管理器](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|SQLMOBILE|[SQL Server Compact Edition 连接管理器](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
  
## 创建 SQL 语句  
 此任务使用的 SQL 语句的源可以是包含语句的任务属性、到包含一个或多个语句的文件的连接，或者是包含语句的变量的名称。 必须用源数据库管理系统 (DBMS) 的方言编写 SQL 语句。 有关详细信息，请参阅 [Integration Services (SSIS) 查询](../../integration-services/integration-services-ssis-queries.md)。  
  
 如果 SQL 语句存储在某个文件中，则该任务使用文件连接管理器来连接到该文件。 有关详细信息，请参阅 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)。  
  
 在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中，可以使用 **“执行 SQL 任务编辑器”** 对话框来键入 SQL 语句，也可使用 **“查询生成器”**（用于创建 SQL 查询的图形用户界面）键入。 有关详细信息，请参阅[执行 SQL 任务编辑器（常规页）](../Topic/Execute%20SQL%20Task%20Editor%20\(General%20Page\).md)和[查询生成器](../Topic/Query%20Builder.md)。  
  
> [!NOTE]  
>  执行 SQL 任务可能无法成功分析在执行 SQL 任务外编写的有效 SQL 语句。  
  
> [!NOTE]  
>  执行 SQL 任务将使用 **RecognizeAll** ParseMode 枚举值。 有关详细信息，请参阅 [ManagedBatchParser 命名空间](http://go.microsoft.com/fwlink/?LinkId=223617)。  
  
## 按批发送多个语句  
 如果在执行 SQL 任务中包含了多个语句，则可以将这些语句进行分组，并将它们作为一批来运行。 若要标明批的结束，请使用 GO 命令。 在两个 GO 命令间的所有 SQL 语句都作为一批发送到 OLE DB 访问接口来运行。 SQL 命令可以包含多个由 GO 命令分隔的批。  
  
 对可以分组到批的 SQL 语句类型有一些限制。 有关详细信息，请参阅 [Batches of Statements](../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)。  
  
 如果执行 SQL 任务运行一个 SQL 语句批，则下列规则适用于批：  
  
-   只有一个语句可以返回结果集，且该语句必须是批中的第一个语句。  
  
-   如果结果集使用结果绑定，则查询必须返回相同数量的列。 如果查询返回不同数量的列，则任务失败。 但是，即使任务失败，其运行的查询（如 DELETE 或 INSERT 查询）也可能成功。  
  
-   如果结果绑定使用列名，则查询必须返回与任务中使用的结果集具有相同名称的列。 如果缺少列，则任务失败。  
  
-   如果任务使用参数绑定，则批中的所有查询都必须具有相同数量和类型的参数。  
  
## 运行参数化 SQL 命令  
 SQL 语句和存储过程常常使用输入参数、输出参数和返回代码。 执行 SQL 任务支持 **Input**、 **Output**和 **ReturnValue** 参数类型。 应当将 **Input** 类型用于输入参数，将 **Output** 用于输出参数并将 **ReturnValue** 用于返回代码。  
  
> [!NOTE]  
>  只有数据访问接口支持这些参数时，才可在执行 SQL 任务中使用它们。  
  
 有关在执行 SQL 任务中使用参数和返回代码的信息，请参阅[执行 SQL 任务中的参数和返回代码](../Topic/Parameters%20and%20Return%20Codes%20in%20the%20Execute%20SQL%20Task.md)。  
  
## 指定结果集类型  
 执行 SQL 任务可能有结果集返回也可能没有结果集返回，这取决于 SQL 命令的类型。 例如，SELECT 语句通常返回结果集，而 INSERT 语句通常不返回结果集。 SELECT 语句所返回的结果集可包含零行、单行或多行。 存储过程还可返回指示过程的执行状态的整数值（称为返回代码）。 这种情况下，结果集由单行组成。  
  
 有关从执行 SQL 任务的 SQL 命令中检索结果集的信息，请参阅[执行 SQL 任务中的结果集](../Topic/Result%20Sets%20in%20the%20Execute%20SQL%20Task.md)。  
  
## 执行 SQL 任务故障排除  
 可以记录执行 SQL 任务对外部数据访问接口的调用。 您可以使用这项日志记录功能对执行 SQL 任务运行的 SQL 命令进行故障排除。 若要记录执行 SQL 任务对外部数据访问接口的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅[包执行的疑难解答工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
 有时，SQL 命令或存储过程会返回多个结果集。 这些结果集不仅包含 **SELECT** 查询结果的行集，还包含 **RAISERROR** 或 **PRINT** 语句的错误结果的单个值。 该任务是否忽略第一个结果集之后出现的结果集中的错误，取决于所用的连接管理器类型：  
  
-   在您使用 OLE DB 和 ADO 连接管理器时，该任务会忽略在第一个结果集之后出现的结果集。 因此，使用这些连接管理器，当错误不属于第一个结果集时，该任务会忽略 SQL 命令或存储过程返回的错误。  
  
-   在您使用 ODBC 和 ADO.NET 连接管理器时，该任务不会忽略在第一个结果集之后出现的结果集。 使用这些连接管理器，当第一个结果集以外的结果集中包含错误时，该任务将失败并出现错误。  
  
### 自定义日志项  
 下表介绍了执行 SQL 任务的自定义日志项。 有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../../integration-services/performance/integration-services-ssis-logging.md)和[日志记录的自定义消息](../../integration-services/performance/custom-messages-for-logging.md)。  
  
|日志项|Description|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|提供有关 SQL 语句的执行阶段的信息。 在任务获得与数据库的连接时、任务开始准备 SQL 语句时以及执行完 SQL 语句之后写入日志项。 准备阶段的日志条目包括任务所使用的 SQL 语句。|  
  
## 配置执行 SQL 任务  
 可以按照下列方式配置执行 SQL 任务：  
  
-   指定用于连接到数据库的连接管理器的类型。  
  
-   指定 SQL 语句返回的结果集的类型。  
  
-   指定 SQL 语句的超时值。  
  
-   指定 SQL 语句的源。  
  
-   指明任务是否跳过 SQL 语句的准备阶段。  
  
-   如果使用 ADO 连接类型，则必须指明 SQL 语句是否为存储过程。 对于其他的连接类型，该属性为只读且其值始终为 **false**。  
  
 可以采用编程方式或通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击下列主题之一：  
  
-   [执行 SQL 任务编辑器（“常规”页）](../Topic/Execute%20SQL%20Task%20Editor%20\(General%20Page\).md)  
  
-   [执行 SQL 任务编辑器（“参数映射”页）](../Topic/Execute%20SQL%20Task%20Editor%20\(Parameter%20Mapping%20Page\).md)  
  
-   [执行 SQL 任务编辑器（“结果集”页）](../Topic/Execute%20SQL%20Task%20Editor%20\(Result%20Set%20Page\).md)  
  
-   [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## 以编程方式配置执行 SQL 任务  
 有关以编程方式设置这些属性的详细信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask>  
  
## 相关任务  
  
-   [在执行 SQL 任务中将查询参数映射到变量](../Topic/Map%20Query%20Parameters%20to%20Variables%20in%20an%20Execute%20SQL%20Task.md)  
  
-   [在执行 SQL 任务中将结果集映射到变量](../Topic/Map%20Result%20Sets%20to%20Variables%20in%20an%20Execute%20SQL%20Task.md)  
  
## 相关内容  
  
-   [执行 SQL 任务中的参数和返回代码](../Topic/Parameters%20and%20Return%20Codes%20in%20the%20Execute%20SQL%20Task.md)  
  
-   [执行 SQL 任务中的结果集](../Topic/Result%20Sets%20in%20the%20Execute%20SQL%20Task.md)  
  
-   [Transact-SQL 引用（数据库引擎）](../../t-sql/transact-sql-reference-database-engine.md)  
  
-   mssqltips.com 上的博客文章： [SQL Server 2012 中新的日期和时间函数](http://go.microsoft.com/fwlink/?LinkId=239783)  
  
  