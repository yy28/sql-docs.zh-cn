---
title: 执行命令 |Microsoft 文档
description: 执行命令
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- commands [OLE DB Driver for SQL Server]
- OLE DB, executing commands
- sessions [OLE DB Driver for SQL Server]
- OLE DB extensions for XML
- OLE DB Driver for SQL Server, command execution
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 20d2a7314db4a70fbc27221fba34e510441d9236
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2018
ms.locfileid: "35665527"
---
# <a name="executing-a-command"></a>执行命令
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  建立到数据源的连接后，使用者调用**IDBCreateSession::CreateSession**方法以创建会话。 该会话充当命令、行集或事务工厂。  
  
 要直接使用单个表或索引，使用者请求**IOpenRowset**接口。 **IOpenRowset::OpenRowset**方法打开，并返回一个包括来自一个基表或索引的所有行的行集。  
  
 若要执行的命令 (如 SELECT\*从作者)，使用者请求**IDBCreateCommand**接口。 使用者可以执行**IDBCreateCommand::CreateCommand**方法创建命令对象并请求**ICommandText**接口。 **ICommandText::SetCommandText**方法用于指定是要执行的命令。  
  
 **执行**命令用于执行命令。 该命令可以是任何 SQL 语句或过程名称。 不是所有命令都将生成结果集（行集）对象。 SELECT * FROM Authors 之类的命令将生成结果集。  
  
## <a name="see-also"></a>请参阅  
 [创建适用于 SQL Server 的 OLE DB 驱动程序应用程序](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
