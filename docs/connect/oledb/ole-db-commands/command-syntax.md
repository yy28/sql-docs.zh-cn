---
title: 命令语法 |Microsoft Docs
description: 命令语法和存储过程
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- commands [OLE DB]
- OLE DB Driver for SQL Server, stored procedures
- stored procedures [OLE DB], command syntax
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 12658166ef66a05bfa18eb6c5c77809e548252ea
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43019223"
---
# <a name="command-syntax"></a>命令语法
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server 的 OLE DB 驱动程序可以识别由 DBGUID_SQL 宏指定的命令语法。 对于 OLE DB 驱动程序适用于 SQL Server，说明符指示 ODBC SQL、 ISO、 组合和[!INCLUDE[tsql](../../../includes/tsql-md.md)]是有效的语法。 例如，以下 SQL 语句使用 ODBC SQL 转义序列指定 LCASE 字符串函数：  
  
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
  
  
