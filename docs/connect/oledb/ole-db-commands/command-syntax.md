---
title: 命令语法 |Microsoft Docs
description: 命令语法和存储过程
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- commands [OLE DB]
- OLE DB Driver for SQL Server, stored procedures
- stored procedures [OLE DB], command syntax
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 15d6d221c9e3435a3ba4c3f58c7d6b6e55314f29
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016120"
---
# <a name="command-syntax"></a>命令语法
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server 的 OLE DB 驱动程序识别 DBGUID_SQL 宏指定的命令语法。 对于 SQL Server 的 OLE DB 驱动程序, 说明符指示 ODBC SQL、ISO 和[!INCLUDE[tsql](../../../includes/tsql-md.md)]的综合是有效的语法。 例如，以下 SQL 语句使用 ODBC SQL 转义序列指定 LCASE 字符串函数：  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE 返回一个字符串，将所有大写字母字符转换为相应的小写字母字符。 ISO 字符串函数 LOWER 执行相同的操作，因此以下 SQL 语句是与上述 ODBC 语句等效的 ISO 命令：  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 在指定为命令的文本时，适用于 SQL Server 的 OLE DB 驱动程序成功处理这种语句的形式之一。  
  
## <a name="stored-procedures"></a>存储过程  
 使用适用于 SQL Server 的 OLE DB 驱动程序命令执行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 存储过程时，在命令文本中使用 ODBC CALL 转义序列。 适用于 SQL Server 的 OLE DB 驱动程序然后使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的远程过程调用机制优化命令处理。 例如，以下 ODBC SQL 语句是比 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 形式更常使用的命令文本：  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [命令](../../oledb/ole-db-commands/commands.md)  
  
  
