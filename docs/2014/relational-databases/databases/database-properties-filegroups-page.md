---
title: 数据库属性（“文件组”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.filegroups.f1
ms.assetid: 8d06e859-73dd-4019-b6e8-99c5c5297697
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6f879da34541b11cf511c2178c9a9ab8223af549
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233357"
---
# <a name="database-properties-filegroups-page"></a>数据库属性（“文件组”页）
  使用此页可以查看文件组，或为所选数据库添加新的文件组。 文件组类型分为行 文件组、FILESTREAM 数据和内存优化文件组。  
  
 行文件组包含常规数据和日志文件。 FILESTREAM 数据文件组包含 FILESTREAM 数据文件。 这些数据文件存储有关在使用 FILESTREAM 存储时二进制大型对象 (BLOB) 数据在文件系统中的存储方式的信息。 两种类型的文件组具有相同的选项。  
  
 如果未启用 FILESTREAM，则不能使用 **Filestream** 部分。 可以通过 [服务器属性（“高级”页）](../../database-engine/configure-windows/server-properties-advanced-page.md)启用 FILESTREAM 存储。  
  
 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户如何使用行文件组的信息，请参阅[数据库文件和文件组](database-files-and-filegroups.md)。 有关 FILESTREAM 数据和文件组的详细信息，请参阅 [FILESTREAM (SQL Server)](../blob/filestream-sql-server.md)。  
  
 数据库必须有内存优化文件组才能包含一个或多个内存优化表。  
  
## <a name="row-and-filestream-data-filegroup-options"></a>行和 FILESTREAM 数据文件组选项  
 **名称**  
 输入文件组的名称。  
  
 **文件**  
 显示文件组中的文件数量。  
  
 **只读**  
 选中此项可以将文件组设为只读状态。  
  
 **Default**  
 选中此项可以将此文件组设为默认文件组。 您可以有一个用于行的默认文件组和一个用于 FILESTREAM 数据的默认文件组。  
  
 **“添加”**  
 向列出数据库文件组的网格中添加新的空白行。  
  
 **删除**  
 从网格中删除所选文件组行。  
  
## <a name="memory-optimized-data-filegroup-options"></a>内存优化数据文件组选项  
 **名称**  
 输入内存优化文件组的名称。  
  
 **Filestream 文件**  
 显示内存优化数据文件组中文件（容器）的数量。 可以在 **“文件”** 页面添加容器。  
  
 **“添加”**  
 向列出数据库文件组的网格中添加新的空白行。  
  
 **删除**  
 从网格中删除所选文件组行。  
  
## <a name="see-also"></a>请参阅  
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)   
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
