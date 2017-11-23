---
title: "命令语法 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-commands
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, commands
- commands [OLE DB]
- SQL Server Native Client OLE DB provider, stored procedures
- stored procedures [OLE DB], command syntax
ms.assetid: d463d3d7-e5cb-426d-8e92-aa29980356b6
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 099e8c0e1168663abed346e67b9f1721bbee275d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="command-syntax"></a>命令语法
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序识别由 DBGUID_SQL 宏指定的命令语法。 有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序，使用说明符指示的 ODBC sql、 ISO、 混合和[!INCLUDE[tsql](../../includes/tsql-md.md)]是有效语法。 例如，以下 SQL 语句使用 ODBC SQL 转义序列指定 LCASE 字符串函数：  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE 返回一个字符串，将所有大写字母字符转换为相应的小写字母字符。 ISO 字符串函数 LOWER 执行相同的操作，因此以下 SQL 语句是与上述 ODBC 语句等效的 ISO 命令：  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序处理其中任一种形式的语句已成功时指定为命令的文本。  
  
## <a name="stored-procedures"></a>存储过程  
 在执行时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]存储过程使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序命令，在命令文本中使用 ODBC 调用转义序列。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序然后使用远程过程调用机制的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以优化命令处理。 例如，以下 ODBC SQL 语句是比 [!INCLUDE[tsql](../../includes/tsql-md.md)] 形式更常使用的命令文本：  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [命令](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
