---
title: 大容量导入和导出数据 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- exporting data
- bulk importing [SQL Server], about bulk importing
- data [SQL Server], bulk export and import
- transferring data
- importing data, (See also bulk importing [SQL Server])
- copying data [SQL Server]
- bulk exporting [SQL Server]
- importing data, bulk import
- copying data [SQL Server], bulk export and import
- exporting data,(See also bulk exporting [SQL Server])
- bulk exporting [SQL Server], about bulk exporting
- bulk importing [SQL Server]
- importing data
ms.assetid: 19049021-c048-44a2-b38d-186d9f9e4a65
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a80eb337bfc03d826ab0933ac235f76dd16bfde9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140614"
---
# <a name="bulk-import-and-export-of-data-sql-server"></a>大容量导入和导出数据 (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表大容量导出数据（“大容量数据”）以及将大容量数据导入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表或未分区的视图。 大容量导入和大容量导出对在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和异类数据源之间有效传输数据是非常重要的。 “大容量导出” 是指将数据从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表复制到数据文件。 “大容量导入” 是指将数据从数据文件加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表。 例如，您可以将数据从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 应用程序导出到数据文件，然后将这些数据大容量导入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。  
  
 **本主题内容：**  
  
-   [大容量导入和大容量导出操作简介](#Intro)  
  
-   [相关任务](#RelatedTasks)  
  
##  <a name="Intro"></a> 大容量导入和大容量导出概述  
 本节列出并简要比较了可用于大容量导入和导出数据的各种方法。 本节还介绍了格式化文件。  
  
 **本主题内容：**  
  
-   [批量导入和导出数据的方法](#MethodsForBuliIE)  
  
-   [格式化文件](#FFs)  
  
###  <a name="MethodsForBuliIE"></a> 批量导入和导出数据的方法  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表大容量导出数据以及将数据大容量导入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表或未分区的视图。 可以使用下列基本方法：  
  
|方法|Description|导入数据|导出数据|  
|------------|-----------------|------------------|------------------|  
|[bcp 实用工具](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)|大容量导出数据和大容量导入数据并生成格式化文件的命令行实用工具 (Bcp.exe)。|是|是|  
|[BULK INSERT 语句](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|将数据直接从数据文件导入数据库表或未分区视图的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。|是|否|  
|[INSERT ...SELECT * FROM OPENROWSET(BULK...) 语句](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|通过在 INSERT 语句中指定 OPENROWSET(BULK…) 函数来选择数据，从而使用 OPENROWSET 大容量行集提供程序将数据大容量导入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语句。|是|否|  
  
> [!IMPORTANT]  
>  SQL Server 大容量导入操作不支持逗号分隔值 (CSV) 文件。 但是，在某些情况下，CSV 文件可在将数据大容量导入 SQL Server 时用作数据文件。 请注意，CSV 文件的字段终止符不一定是逗号。 有关详细信息，请参阅[准备用于批量导出或导入的数据 (SQL Server)](prepare-data-for-bulk-export-or-import-sql-server.md)。  
  
###  <a name="FFs"></a> 格式化文件  
 **bcp** 实用工具、BULK INSERT 和 INSERT ...SELECT \* FROM OPENROWSET(BULK...) 都支持使用专门的“格式化文件”来存储数据文件中每个字段的格式信息。 格式化文件还可以包含相应的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表的有关信息。 格式化文件可以用于提供从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例大容量导出数据和向其中大容量导入数据时所需的所有格式信息。  
  
 格式化文件提供了一种解释导入期间数据文件中数据的格式以及设置导出期间数据文件中数据格式的灵活方式。 这种灵活性使得解释数据时无需编写专用代码，也无需为满足 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或外部应用程序的特殊需要而重新设置数据的格式。 例如，如果将要加载的数据大容量导出到某个需要逗号分隔值的应用程序，则可以使用格式化文件将逗号作为字段终止符插入导出的数据中。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持两种类型的格式化文件：XML 格式化文件和非 XML 格式化文件。  
  
 **bcp** 实用工具是唯一能够生成格式化文件的工具。 有关详细信息，请参阅 [创建格式化文件 (SQL Server)](create-a-format-file-sql-server.md)。 有关格式化文件的详细信息，请参阅[导入或导出数据的格式化文件 (SQL Server)](format-files-for-importing-or-exporting-data-sql-server.md)。  
  
> [!NOTE]  
>  如果在大容量导出或导入操作期间未提供格式化文件，您可以在命令行处覆盖默认格式。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [导入和导出大容量数据使用 bcp 实用工具&#40;SQL Server&#41;](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)  
  
-   [使用 BULK INSERT 或 OPENROWSET 大容量数据导入&#40;大容量...&#41; &#40;SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)  
  
-   [批量导入数据时保留标识值 (SQL Server)](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [在批量导入期间保留 Null 或使用默认值 (SQL Server)](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [准备用于批量导出或导入的数据 (SQL Server)](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **使用格式化文件**  
  
-   [创建格式化文件 (SQL Server)](create-a-format-file-sql-server.md)  
  
-   [使用格式化文件批量导入数据 (SQL Server)](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用格式化文件将表列映射到数据文件字段 (SQL Server)](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [使用格式化文件跳过数据字段 (SQL Server)](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [使用格式化文件跳过表列 (SQL Server)](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **使用数据格式进行大容量导入或大容量导出**  
  
-   [导入来自早期版本的 SQL Server 的本机格式数据和字符格式数据](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用字符格式导入或导出数据 (SQL Server)](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用本机格式导入或导出数据 (SQL Server)](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字符格式导入或导出数据 (SQL Server)](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 本机格式导入或导出数据 (SQL Server)](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **在使用 bcp 时指定数据格式以获得兼容性**  
  
1.  [指定字段终止符和行终止符 (SQL Server)](specify-field-and-row-terminators-sql-server.md)  
  
2.  [使用 bcp 指定数据文件中的前缀长度 (SQL Server)](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [使用 bcp 指定文件存储类型 (SQL Server)](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [在大容量导入中按最小方式记录日志的前提条件](prerequisites-for-minimal-logging-in-bulk-import.md)   
 [用来导入或导出数据的格式化文件 (SQL Server)](format-files-for-importing-or-exporting-data-sql-server.md)   
 [批量导入和导出 XML 文档的示例 (SQL Server)](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)   
 [将数据库复制到其他服务器](../databases/copy-databases-to-other-servers.md)   
 [对 XML 数据执行大容量加载 (SQLXML 4.0)](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)   
 [执行大容量复制操作](../native-client/features/performing-bulk-copy-operations.md)   
 [bcp 实用工具](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [用来导入或导出数据的格式化文件 (SQL Server)](format-files-for-importing-or-exporting-data-sql-server.md)   
 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)  
  
  
