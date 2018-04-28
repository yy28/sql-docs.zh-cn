---
title: 命令语法 |Microsoft 文档
description: 命令语法和存储过程
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- commands [OLE DB]
- OLE DB Driver for SQL Server, stored procedures
- stored procedures [OLE DB], command syntax
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67759000537b9387df6c0c6dfe85123437a96896
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="command-syntax"></a>命令语法
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server 的 OLE DB 驱动程序识别由 DBGUID_SQL 宏指定的命令语法。 对于 OLE DB 驱动程序的 SQL Server，使用说明符指示的 ODBC sql、 ISO、 混合和[!INCLUDE[tsql](../../../includes/tsql-md.md)]是有效语法。 例如，以下 SQL 语句使用 ODBC SQL 转义序列指定 LCASE 字符串函数：  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE 返回一个字符串，将所有大写字母字符转换为相应的小写字母字符。 ISO 字符串函数 LOWER 执行相同的操作，因此以下 SQL 语句是与上述 ODBC 语句等效的 ISO 命令：  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 SQL Server 的 OLE DB 驱动程序处理其中任一种形式的语句已成功时指定为命令的文本。  
  
## <a name="stored-procedures"></a>存储过程  
 在执行时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]对于 SQL Server 命令，使用 OLE DB 驱动程序的存储的过程在命令文本中使用 ODBC 调用转义序列。 SQL Server 的 OLE DB 驱动程序，然后使用远程过程调用机制的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]以优化命令处理。 例如，以下 ODBC SQL 语句是比 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 形式更常使用的命令文本：  
  
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
  
  
