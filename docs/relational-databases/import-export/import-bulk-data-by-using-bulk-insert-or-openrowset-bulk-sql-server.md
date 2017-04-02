---
title: "使用 BULK INSERT 或 OPENROWSET(BULK...) 导入批量数据 (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "07/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-bulk-import-export"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "BULK INSERT 语句, 从远程数据文件导入数据"
  - "批量导入 [SQL Server], 方法"
  - "批量导出 [SQL Server], 方法"
  - "OPENROWSET 函数, BULK INSERT"
  - "批量导入 [SQL Server], 安全性"
  - "大容量行集提供程序 [SQL Server]"
  - "批量导出 [SQL Server], BULK INSERT 语句"
  - "远程数据访问 [SQL Server], 批量导入"
  - "批量导入 [SQL Server], BULK INSERT 语句"
  - "Transact-SQL 大容量导出/导入操作"
ms.assetid: 18a64236-0285-46ea-8929-6ee9bcc020b9
caps.latest.revision: 45
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 44
---
# 使用 BULK INSERT 或 OPENROWSET(BULK...) 导入批量数据 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  本主题概述了如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] BULK INSERT 语句和 INSERT...SELECT * FROM OPENROWSET(BULK...) 语句将数据从某一数据文件大容量导入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。 本主题还说明了使用 BULK INSERT 和 OPENROWSET(BULK...) 以及使用这些方法从远程数据源大容量导入数据的安全注意事项。  
  
> **注意：**在使用 BULK INSERT 或 OPENROWSET(BULK ) 时，请务必了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本是如何处理模拟的。 有关详细信息，请参阅本主题后面的“安全注意事项”。  
  
## BULK INSERT 语句  
 BULK INSERT 将数据从数据文件加载到表中。 此功能与 **bcp** 命令的 **in** 选项提供的功能相似，但是数据文件将由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程读取。 有关 BULK INSERT 语法的说明，请参阅 [BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md)。  
  
## BULK INSERT 示例  
 
  
-   [BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
-   [批量导入和导出 XML 文档的示例 (SQL Server)](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [批量导入数据时保留标识值 (SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [在批量导入期间保留 Null 或使用默认值 (SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [指定字段终止符和行终止符 (SQL Server)](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [使用格式化文件批量导入数据 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用字符格式导入或导出数据 (SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用本机格式导入或导出数据 (SQL Server)](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字符格式导入或导出数据 (SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 本机格式导入或导出数据 (SQL Server)](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用格式化文件跳过表列 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [使用格式化文件将表列映射到数据文件字段 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## OPENROWSET(BULK ) 函数  
 通过调用 OPENROWSET 函数并指定 BULK 选项，访问 OPENROWSET 大容量行集提供程序。 使用 OPENROWSET(BULK...) 函数可以通过 OLE DB 访问接口连接到远程数据源（如数据文件）以访问远程数据。  
  
 若要大容量导入数据，请从 INSERT 语句中的 SELECT...FROM 子句调用 OPENROWSET(BULK...)。 大容量导入数据的基本语法如下：  
  
 INSERT ... SELECT * FROM OPENROWSET(BULK...)  
  
 在 INSERT 语句中使用时，OPENROWSET(BULK...) 支持表提示。 BULK 子句除了接受 TABLOCK 等常规表提示之外，还可以接受下列专用表提示：IGNORE_CONSTRAINTS（仅忽略 CHECK 约束）、IGNORE_TRIGGERS、KEEPDEFAULTS 和 KEEPIDENTITY。 有关详细信息，请参阅[表提示 (Transact-SQL)](../Topic/Table%20Hints%20\(Transact-SQL\).md)。  
  
 有关 BULK 选项的更多使用信息，请参阅 [OPENROWSET (Transact-SQL)](../../t-sql/functions/openrowset-transact-sql.md)。  
  
## INSERT...SELECT * FROM OPENROWSET(BULK...) 语句 - 示例：
  
-   [批量导入和导出 XML 文档的示例 (SQL Server)](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [批量导入数据时保留标识值 (SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [在批量导入期间保留 Null 或使用默认值 (SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [使用格式化文件批量导入数据 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用字符格式导入或导出数据 (SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用格式化文件跳过表列 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [使用格式化文件跳过数据字段 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [使用格式化文件将表列映射到数据文件字段 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## 安全注意事项  
 如果用户使用的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名，则系统将使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程帐户的安全配置文件。 使用 SQL Server 身份验证的登录名不能在数据库引擎外部进行身份验证。 因此，当 BULK INSERT 命令由使用 SQL Server 身份验证的登录名启动时，使用 SQL Server 进程帐户（SQL Server 数据库引擎服务使用的帐户）的安全上下文建立到数据的连接。 
 
 要成功读取源数据，您必须授予 SQL Server 数据库引擎使用的帐户访问源数据的权限。 与此相反，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户使用 Windows 身份验证登录，则该用户只能读取用户帐户可以访问的那些文件，而不考虑 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的安全配置文件。  
  
 例如，假设用户使用 Windows 身份验证登录到某个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 对于能够使用 BULK INSERT 或 OPENROWSET 将数据从数据文件导入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中的用户，用户帐户需要具有数据文件的读取权限。 有了数据文件的访问权限，即使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程没有访问该文件的权限，用户也可以将数据从文件导入表中。 用户无需将文件访问权限授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows，使得一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例可以通过转发已经过身份验证的 Windows 用户的凭据来连接到另一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 这种安排称为“模拟”  或“委托” 。 在使用 BULK INSERT 或 OPENROWSET 时，请务必了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本是如何处理用户模拟的安全性的。 用户模拟允许数据文件保存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程或用户所在的计算机以外的另一台计算机上。 例如，如果 **Computer_A** 上的用户具有对 **Computer_B** 上的数据文件的访问权限，而且凭据委托已设置妥当，则用户可以连接到运行在 **Computer_C** 上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，访问 **Computer_B** 中的数据文件以及将数据从该文件大容量导入到 **Computer_C** 中的表中。  
  
## 从远程数据文件中批量导入  
 若要使用 BULK INSERT 或 INSERT...SELECT \* FROM OPENROWSET(BULK...) 从其他计算机中大容量导入数据，必须在两台计算机之间共享数据文件。 指定共享数据文件时，请使用它的通用命名约定 (UNC) 名称，其一般形式为 **\\\\**服务器名**\\**共享名**\\**路径**\\**文件名。 此外，用来访问该数据文件的帐户必须具有读取远程磁盘上的文件所需的权限。  
  
 例如，下面的 `BULK INSERT` 语句会将名为 `SalesOrderDetail` 的数据文件中的数据大容量导入到 `AdventureWorks` 数据库的 `newdata.txt`表。 此数据文件驻留在系统 `\dailyorders` 的 `salesforce` 网络共享目录下的 `computer2` 共享文件夹中。  
  
```  
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
   FROM '\\computer2\salesforce\dailyorders\neworders.txt';  
GO  
```  
  
> **注意：**此限制不适用于 **bcp** 实用工具，因为客户端独立于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 读取文件。  
  
## 另请参阅  
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT 子句 (Transact-SQL)](../../t-sql/queries/select-clause-transact-sql.md)   
 [批量导入和导出数据 (SQL Server)](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [OPENROWSET (Transact-SQL)](../../t-sql/functions/openrowset-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [bcp 实用工具](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
  