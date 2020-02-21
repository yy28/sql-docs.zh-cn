---
title: 执行命令 | Microsoft Docs
description: 执行命令
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- commands [OLE DB Driver for SQL Server]
- OLE DB, executing commands
- sessions [OLE DB Driver for SQL Server]
- OLE DB extensions for XML
- OLE DB Driver for SQL Server, command execution
author: pmasl
ms.author: pelopes
ms.openlocfilehash: f13c9177a74212b849572881f114e503a9530286
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67994987"
---
# <a name="executing-a-command"></a>执行命令
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  与数据源建立连接后，使用者调用 IDBCreateSession::CreateSession 方法来创建会话。 该会话充当命令、行集或事务工厂。  
  
 为了直接使用单独的表或索引，使用者请求 IOpenRowset 接口。 IOpenRowset::OpenRowset 方法打开并返回一个行集，该行集包括来自单个基表或索引的所有行。  
  
 为了执行某一命令（例如 SELECT \* FROM Authors），使用者请求 IDBCreateCommand 接口。 使用者可以执行 IDBCreateCommand::CreateCommand 方法，以便为 ICommandText 接口创建命令对象和请求。 ICommandText::SetCommandText 方法用于指定要执行的命令。  
  
 Execute 命令用于执行该命令。 该命令可以是任何 SQL 语句或过程名称。 不是所有命令都将生成结果集（行集）对象。 SELECT * FROM Authors 之类的命令将生成结果集。  
  
## <a name="see-also"></a>另请参阅  
 [创建适用于 SQL Server 的 OLE DB 驱动程序应用程序](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
