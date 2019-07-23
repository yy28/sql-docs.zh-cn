---
title: SQL Server 消息结果 |Microsoft Docs
description: SQL Server 消息结果
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 05d731f418bad21f9e8ec32c620b352c5663994a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994917"
---
# <a name="sql-server-message-results"></a>SQL Server 消息结果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  执行下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句时不会生成适用于 SQL Server 的 OLE DB 驱动程序行集或受影响的行数：  
  
-   PRINT  
  
-   严重性级别为 10 或更低的 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 这些语句会返回一个或多个信息性消息，或者使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 返回信息性消息以替代行集或计数结果。 成功执行时, SQL Server 的 OLE DB 驱动程序返回 S_OK, 消息可用于 SQL Server 使用者的 OLE DB 驱动程序。  
  
 SQL Server 的 OLE DB 驱动程序返回 S_OK, 并在执行多[!INCLUDE[tsql](../../../includes/tsql-md.md)]个语句或使用者执行 SQL Server 成员函数的 OLE DB 驱动程序时提供一个或多个信息性消息。  
  
 在每次执行成员函数之后，不论返回代码的值如何、是否存在返回的 IRowset 或 IMultipleResults 接口引用或受影响的行数是多少，允许动态指定查询文本的适用于 SQL Server 的 OLE DB 驱动程序使用者都应检查错误接口   。  
  
## <a name="see-also"></a>另请参阅  
 [错误](../../oledb/ole-db-errors/errors.md)  
  
  
