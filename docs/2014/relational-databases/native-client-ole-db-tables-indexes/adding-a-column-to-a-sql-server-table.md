---
title: 向 SQL Server 表添加列 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- SQL Server Native Client OLE DB provider, columns
- adding columns
ms.assetid: 22bae18a-bc9d-4617-8660-ed8b17a468d4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32e78feae791788e0aad87079546ea8c7d49e734
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046492"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>向 SQL Server 表添加列
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口公开**itabledefinition:: Addcolumn**函数。 利用此函数，使用者便可向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中添加列。  
  
 当您添加到列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口使用者约束，如下所示：  
  
-   如果 DBPROP_COL_AUTOINCREMENT 为 VARIANT_TRUE，则 DBPROP_COL_NULLABLE 必须为 VARIANT_FALSE。  
  
-   如果相应列是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] timestamp 数据类型定义的，则 DBPROP_COL_NULLABLE 必须为 VARIANT_FALSE。  
  
-   对于任何其他列定义，DBPROP_COL_NULLABLE 都必须为 VARIANT_TRUE。  
  
 在 pTableID 参数的 uName 联合的 pwszName 成员中，使用者将表名指定为 Unicode 字符串。 pTableID 的 eKind 成员必须是 DBKIND_NAME。  
  
 在 uName 联合（位于 DBCOLUMNDESC 参数 pColumnDesc 的 dbcid 成员中）的 pwszName 成员中，将新列的名称指定为 Unicode 字符串。 eKind 成员必须为 DBKIND_NAME。  
  
## <a name="see-also"></a>请参阅  
 [表和索引](tables-and-indexes.md)   
 [ALTER TABLE (Transact-SQL)](/sql/t-sql/statements/alter-table-transact-sql)  
  
  
