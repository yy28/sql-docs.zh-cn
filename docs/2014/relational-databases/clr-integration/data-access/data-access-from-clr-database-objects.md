---
title: 从 CLR 数据库对象进行数据访问 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], data access
- routines [CLR integration]
- data access [CLR integration]
- ADO.NET [CLR integration]
- internal data access [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], data access
- managed code [SQL Server], database objects
- .NET Data Access Provider for SQL Server [CLR integration]
- managed code [SQL Server], data access
- SqlClient provider
- in-process data access providers [CLR integration]
ms.assetid: 9a0f4dee-71c1-42e9-a85e-52382807010f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4561c7b8979a919ea144bab6d9b42f722b089e48
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62874082"
---
# <a name="data-access-from-clr-database-objects"></a>从 CLR 数据库对象进行数据访问
  公共语言运行时（CLR）例程可以轻松地访问存储在其中运行的[!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]实例中的数据，以及存储在远程实例中的数据。 该例程可以访问的特定数据由代码正在其中运行的用户上下文确定。 通过使用来自托管客户端和中间层应用程序的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据的 .NET Framework 数据提供程序，从 CLR 数据库对象中访问数据。 因此，您可以在客户端和中间层应用程序中充分利用您所掌握的有关 ADO.NET 和 `SqlClient` 的知识。  
  
> [!NOTE]  
>  默认情况下，不允许用户定义类型方法和用户定义函数执行数据访问。 您必须将 `DataAccess` 或 `SqlMethodAttribute` 的 `SqlFunctionAttribute` 属性设置为 `DataAccessKind.Read`，才能从用户定义类型 (UDT) 方法或用户定义函数进行只读数据访问。 不允许从 UDT 或用户定义函数执行数据修改操作，否则，将在执行时引发异常。  
  
 本节只讨论当从 CLR 数据库对象中访问数据时特定的功能差异和行为差异。 有关 ADO.NET 的特性和功能的详细信息，请参阅 .NET Framework SDK 随附的 ADO.NET 文档。  
  
 下表列出了本节的主题。  
  
 [上下文连接](context-connection.md)  
 介绍与 SQL Server 之间的上下文连接。  
  
 [模拟和连接凭据](impersonation-and-credentials-for-connections.md)  
 介绍模拟连接和连接凭据。  
  
 [SQL Server 进程内专用的 ADO.NET 扩展](../../clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
 讨论进程内特定的 `SqlPipe`、`SqlContext`、`SqlTriggerContext` 和 `SqlDataRecord` 对象。  
  
 [CLR 集成和事务](../../native-client-ole-db-transactions/transactions.md)  
 介绍 System.Transactions 命名空间中提供的新事务框架如何与 ADO.NET 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR 集成相集成。  
  
 [从 CLR 数据库对象进行 XML 序列化](../../../database-engine/dev-guide/xml-serialization-from-clr-database-objects.md)  
 说明如何对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 CLR 数据库对象启用 XML 序列化方案。  
  
  
