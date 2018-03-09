---
title: "执行命令 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-provider
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- commands [SQL Server Native Client]
- OLE DB, executing commands
- sessions [SQL Server Native Client]
- OLE DB extensions for XML
- SQL Server Native Client OLE DB provider, command execution
ms.assetid: bb0b3cbf-fe45-46ba-b2ec-c5a39e3c7081
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 495f632181ec7697c08002684e2f6e77f272d39a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="executing-a-command"></a>执行命令
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  建立到数据源的连接后，使用者调用**IDBCreateSession::CreateSession**方法以创建会话。 该会话充当命令、行集或事务工厂。  
  
 要直接使用单个表或索引，使用者请求**IOpenRowset**接口。 **IOpenRowset::OpenRowset**方法打开，并返回一个包括来自一个基表或索引的所有行的行集。  
  
 若要执行的命令 (如 SELECT\*从作者)，使用者请求**IDBCreateCommand**接口。 使用者可以执行**IDBCreateCommand::CreateCommand**方法创建命令对象并请求**ICommandText**接口。 **ICommandText::SetCommandText**方法用于指定是要执行的命令。  
  
 **执行**命令用于执行命令。 该命令可以是任何 SQL 语句或过程名称。 不是所有命令都将生成结果集（行集）对象。 SELECT * FROM Authors 之类的命令将生成结果集。  
  
## <a name="see-also"></a>另请参阅  
 [创建 SQL Server Native Client OLE DB 提供程序应用程序](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
