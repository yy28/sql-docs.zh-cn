---
title: "ADO NET 目标编辑器（“连接管理器”页） | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.adonetdest.connection.f1"
ms.assetid: a3b11286-32c8-40e1-8ae7-090e2590345a
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 31
---
# ADO NET 目标编辑器（“连接管理器”页）
  可以使用 **“ADO NET 目标编辑器”** 对话框的 **“连接管理器”** 页，为目标选择 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接。 使用此页还可以选择数据库中的表或视图。  
  
 若要了解有关 ADO NET 目标的详细信息，请参阅 [ADO NET Destination](../../integration-services/data-flow/ado-net-destination.md)。  
  
 **打开“连接管理器”页**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开具有 ADO NET 目标的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 ADO NET 目标。  
  
3.  在 **“ADO NET 目标编辑器”**中，单击 **“连接管理器”**。  
  
## 静态选项  
 **“ODBC 目标编辑器”**  
 从列表中选择一个现有连接管理器，或通过单击“新建”创建一个新连接。  
  
 **新建**  
 使用“配置 ADO.NET 连接管理器”对话框创建新的连接管理器。  
  
 **使用表或视图**  
 从列表中选择现有表或视图，或单击“新建”创建新表。  
  
 **新建**  
 使用“创建表”对话框创建新表或视图。  
  
> [!NOTE]  
>  单击 **“新建”**时， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将基于所连接的数据源生成一条默认的 CREATE TABLE 语句。 即使源表包含一个已声明了 FILESTREAM 属性的列，此默认 CREATE TABLE 语句也不会包含 FILESTREAM 属性。 若要运行具有 FILESTREAM 属性的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件，首先要在目标数据库上实现 FILESTREAM 存储。 然后在 **“创建表”** 对话框中将 FILESTREAM 属性添加到 CREATE TABLE 语句中。 有关详细信息，请参阅[二进制大型对象 (Blob) 数据 (SQL Server)](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
 **预览**  
 使用“预览查询结果”对话框预览结果。 预览最多可以显示 200 行。  
  
 **可用时使用大容量插入**  
 指定是否使用 <xref:System.Data.SqlClient.SqlBulkCopy> 接口来提高大容量插入操作的性能。  
  
 只有可返回 <xref:System.Data.SqlClient.SqlConnection> 对象的 ADO.NET 提供程序才支持使用 <xref:System.Data.SqlClient.SqlBulkCopy> 接口。 SQL Server 的 .NET 数据提供程序 (SqlClient) 可以返回 <xref:System.Data.SqlClient.SqlConnection> 对象，而自定义提供程序可以返回 <xref:System.Data.SqlClient.SqlConnection> 对象。  
  
 可使用 SQL Server 的 .NET 数据提供程序 (SqlClient) 连接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。  
  
 如果选择“可用时使用大容量插入”并将“错误”选项设置为“重定向该行”，则目标重定向到错误输出的数据批次可能包含正确的行。有关以大容量操作方式处理错误的详细信息，请参阅[数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。 有关“错误”选项的详细信息，请参阅 [ADO NET 目标编辑器（“错误输出”页）](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md)。  
  
> [!NOTE]  
>  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Sybase 源表包含一个标识列，则必须在 ADO NET 目标前后使用执行 SQL 任务来运行 SET IDENTITY_INSERT 语句。 标识列属性为列指定一个增量值。 SET IDENTITY_INSERT 语句启用要插入到标识列的显式值。 若要基于同一个数据库连接运行 CREATE TABLE 和 SET IDENTITY 语句，请将 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器的 **RetainSameConnection** 属性设置为 **True**。 此外，还要对执行 SQL 任务和 ADO NET 目标使用相同的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器。  
>   
>  有关详细信息，请参阅 [SET IDENTITY_INSERT (Transact SQL)](../../t-sql/statements/set-identity-insert-transact-sql.md) 和 [IDENTITY（属性）(Transact-SQL)](../Topic/IDENTITY%20\(Property\)%20\(Transact-SQL\).md)。  
  
## 外部资源  
 sqlcat.com 上的技术文章 [快速将数据加载到 Windows Azure SQL Database 中](http://go.microsoft.com/fwlink/?LinkId=244333)。  
  
## 另请参阅  
 [ADO NET 目标编辑器（“映射”页）](../../integration-services/data-flow/ado-net-destination-editor-mappings-page.md)   
 [ADO NET 目标编辑器（“错误输出”页）](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md)   
 [ADO.NET 连接管理器](../../integration-services/connection-manager/ado-net-connection-manager.md)   
 [执行 SQL 任务](../../integration-services/control-flow/execute-sql-task.md)  
  
  