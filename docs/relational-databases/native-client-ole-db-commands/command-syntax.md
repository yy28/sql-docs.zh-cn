---
title: 命令语法（Native Client OLE DB 提供程序） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, commands
- commands [OLE DB]
- SQL Server Native Client OLE DB provider, stored procedures
- stored procedures [OLE DB], command syntax
ms.assetid: d463d3d7-e5cb-426d-8e92-aa29980356b6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b927ef211c21773eeccd183a4f18bab8ae5e6e91
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942877"
---
# <a name="command-syntax"></a>命令语法
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序识别 DBGUID_SQL 宏指定的命令语法。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序，说明符指示 ODBC SQL、ISO 和的综合 [!INCLUDE[tsql](../../includes/tsql-md.md)] 是有效的语法。 例如，以下 SQL 语句使用 ODBC SQL 转义序列指定 LCASE 字符串函数：  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE 返回一个字符串，将所有大写字母字符转换为相应的小写字母字符。 ISO 字符串函数 LOWER 执行相同的操作，因此以下 SQL 语句是与上述 ODBC 语句等效的 ISO 命令：  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]当指定为命令的文本时，Native Client OLE DB 提供程序成功地处理语句的一种形式。  
  
## <a name="stored-procedures"></a>存储过程  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider 命令执行存储过程时，请在命令文本中使用 ODBC CALL 转义序列。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]然后，Native Client OLE DB 提供程序使用的远程过程调用机制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来优化命令处理。 例如，以下 ODBC SQL 语句是比 [!INCLUDE[tsql](../../includes/tsql-md.md)] 形式更常使用的命令文本：  
  
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
  
  
