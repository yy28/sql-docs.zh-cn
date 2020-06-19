---
title: 用于批量导入或批量导出的数据格式 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], choosing
- bulk importing [SQL Server], data formats
ms.assetid: 73fe6741-9437-4b26-b030-28b863e74399
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1b92ac8c038362ff18a1459a8bf3c55b6b596a17
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85026836"
---
# <a name="data-formats-for-bulk-import-or-bulk-export-sql-server"></a>用于批量导入或导出的数据格式 (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以接受字符数据格式或本机二进制数据格式的数据。 当在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和其他应用程序（例如， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel）或其他数据库服务器（例如，Oracle 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）之间移动数据时，请使用字符格式。 只有在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例之间传输数据时才可以使用本机格式。  
  
 **本主题内容：**  
  
-   [用于大容量导入或导出的数据格式](#ComponentsAndConcepts)  
  
-   [相关任务](#RelatedTasks)  
  
##  <a name="data-formats-for-bulk-import-or-export"></a><a name="ComponentsAndConcepts"></a> 用于大容量导入或导出的数据格式  
 下表列出了不同数据显示方式和操作的源或目标一般适合使用的数据格式。  
  
|Operation|本机|Unicode 本机|字符|Unicode 字符|  
|---------------|------------|--------------------|---------------|-----------------------|  
|使用不包含任何扩展字符或双字节字符集 (DBCS) 字符的数据文件在多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之间进行大容量的数据传输。 除非使用格式化文件，否则这些表的定义必须相同。|是<sup>1</sup>|-|-|-|  
|对于 `sql_variant` 列，最好使用本机数据格式，因为本机数据格式可以保留每一个 `sql_variant` 值的元数据，这一点不同于字符格式或 Unicode 格式。|是|-|-|-|  
|使用包含扩展字符或 DBCS 字符的数据文件在多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之间进行大容量的数据传输。|-|是|-|-|  
|大容量导入其他程序生成的文本文件中的数据。|-|-|是|-|  
|将数据大容量导出到要在其他程序中使用的文本文件中。|-|-|是|-|  
|使用包含 Unicode 数据而不包含任何扩展字符或 DBCS 字符的数据文件在多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之间进行大容量的数据传输。|-|-|-|是|  
  
 <sup>1</sup> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用**bcp**时从大容量导出数据的最快方法。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
  
-   [使用本机格式导入或导出数据 (SQL Server)](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用字符格式导入或导出数据 (SQL Server)](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 本机格式导入或导出数据 (SQL Server)](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字符格式导入或导出数据 (SQL Server)](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [导入来自早期版本的 SQL Server 的本机格式数据和字符格式数据](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)   
 [在使用 bcp 时指定数据格式以获得兼容性 (SQL Server)](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)  
  
  
