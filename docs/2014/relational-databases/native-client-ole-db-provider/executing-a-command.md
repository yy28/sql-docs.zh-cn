---
title: 执行命令 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- commands [SQL Server Native Client]
- OLE DB, executing commands
- sessions [SQL Server Native Client]
- OLE DB extensions for XML
- SQL Server Native Client OLE DB provider, command execution
ms.assetid: bb0b3cbf-fe45-46ba-b2ec-c5a39e3c7081
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f94cc014a04c3392fefb61f4fa291a8f5a44ad8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62638457"
---
# <a name="executing-a-command"></a>执行命令
  建立到数据源的连接后，使用者调用**idbcreatesession:: Createsession**方法来创建会话。 该会话充当命令、行集或事务工厂。  
  
 为了直接使用单独的表或索引，使用者请求 `IOpenRowset` 接口。 `IOpenRowset::OpenRowset` 方法打开并返回一个行集，该行集包括来自单个基表或索引的所有行。  
  
 若要执行的命令 (如 SELECT \* FROM Authors)，使用者请求`IDBCreateCommand`接口。 使用者可以执行 `IDBCreateCommand::CreateCommand` 方法，以便为 `ICommandText` 接口创建一个命令对象和请求。 `ICommandText::SetCommandText` 方法用于指定要执行的命令。  
  
 `Execute` 命令用于执行该命令。 该命令可以是任何 SQL 语句或过程名称。 不是所有命令都将生成结果集（行集）对象。 SELECT * FROM Authors 之类的命令将生成结果集。  
  
## <a name="see-also"></a>请参阅  
 [创建 SQL Server Native Client OLE DB 提供程序应用程序](creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
