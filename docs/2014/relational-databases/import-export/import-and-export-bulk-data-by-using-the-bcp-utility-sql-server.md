---
title: 使用 bcp 实用工具导入和导出批量数据 (SQL Server) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk exporting [SQL Server], bcp utility
- bulk importing [SQL Server], bcp utility
- bcp utility [SQL Server], about bcp utility
ms.assetid: 73e949de-67a3-4c84-9735-7da1ad4ba34a
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: ''
ms.custom: ''
ms.date: 06/14/2017
ms.openlocfilehash: 7075bf87ed64686750bc4a267af431268987ff35
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708214"
---
# <a name="import-and-export-bulk-data-by-using-the-bcp-utility-sql-server"></a>使用 bcp 实用工具导入和导出大容量数据 (SQL Server)

本主题概述了如何使用 [bcp 实用工具](../../tools/bcp-utility.md) 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中可使用 SELECT 语句的任意位置（包括分区视图）导出数据。  
  
 bcp 实用工具 (Bcp.exe) 是一个使用大容量复制程序 (BCP) API 的命令行工具。 bcp 实用工具可执行以下任务：  
  
-   将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中的数据大容量导出到数据文件中。  
  
-   从查询中批量导出数据。  
  
-   将数据文件中的数据大容量导入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。  
  
-   生成格式化文件。  
  
 bcp 实用工具可通过 **bcp** 命令进行访问。 使用 **bcp** 命令批量导入数据时，除非使用已有的格式化文件，否则必须了解表的架构及其各列的数据类型。  
  
 bcp 实用工具可将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中的数据导出到数据文件，以供其他程序使用。 此实用工具还可将其他程序（通常为另一数据库管理系统 (DBMS)）中的数据导入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表。 数据首先从源程序导出到数据文件，然后再通过单独的操作将数据文件中的数据复制到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。  
  
 **bcp** 命令提供可指定数据文件的数据类型和其他信息的开关。 如果未指定这些开关，则此命令会提示您指定格式信息，例如数据文件中数据字段的类型。 然后此命令会询问您是否要创建包含交互式响应的格式化文件。 如果希望在以后的批量导入或批量导出操作中具有灵活性，格式化文件通常会很有用。 可以在稍后对同等数据文件使用 **bcp** 命令时指定该格式化文件。 有关详细信息，请参阅[在使用 bcp 时指定数据格式以获得兼容性 (SQL Server)](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)。  
  
> [!NOTE]  
>  bcp 实用工具通过使用 ODBC 大容量复制进行编写  
  
 有关 **bcp** 命令语法的说明，请参阅 [bcp Utility](../../tools/bcp-utility.md)。  
  
## <a name="examples"></a>示例

 有关 **bcp** 示例，请参阅：  
  
-   [bcp Utility](../../tools/bcp-utility.md)  
  
-   [创建格式化文件 (SQL Server)](create-a-format-file-sql-server.md)  
  
-   [批量导入和导出 XML 文档的示例 (SQL Server)](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [批量导入数据时保留标识值 (SQL Server)](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [在批量导入期间保留 Null 或使用默认值 (SQL Server)](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [指定字段终止符和行终止符 (SQL Server)](specify-field-and-row-terminators-sql-server.md)  
  
-   [使用格式化文件批量导入数据 (SQL Server)](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用字符格式导入或导出数据 (SQL Server)](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用本机格式导入或导出数据 (SQL Server)](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字符格式导入或导出数据 (SQL Server)](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 本机格式导入或导出数据 (SQL Server)](use-unicode-native-format-to-import-or-export-data-sql-server.md)  

## <a name="see-also"></a>另请参阅

[INSERT &#40;&#41; transact-sql](/sql/t-sql/statements/insert-transact-sql)
[SELECT 子句&#40;&#41; transact-sql](/sql/t-sql/queries/select-clause-transact-sql)
[bcp 实用工具](../../tools/bcp-utility.md)   
[准备大容量导入&#40;数据&#41; SQL Server](prepare-to-bulk-import-data-sql-server.md)
[ &#40;BULK INSERT transact-sql&#41; ](/sql/t-sql/statements/bulk-insert-transact-sql)
[大容量导入和导出数据&#40;SQL Server&#41; ](bulk-import-and-export-of-data-sql-server.md)
[OPENROWSET &#40;transact-sql&#41; ](/sql/t-sql/functions/openrowset-transact-sql)
[创建格式化文件&#40;SQL Server&#41; ](create-a-format-file-sql-server.md)