---
title: 上下文连接 |Microsoft 文档
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- context connections [CLR integration]
- database objects [CLR integration], connections
- connections [CLR integration]
- context [CLR integration]
ms.assetid: 67dd1925-d672-4986-a85f-bce4fe832ef7
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a95f4c4b190f37674290588714fc3e7b0c6582a5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125635"
---
# <a name="context-connection"></a>上下文连接
  内部数据访问问题是一种非常常见的情况。 即您希望访问正在执行公共语言运行时 (CLR) 存储过程或函数的相同服务器。 一种选择是使用 `System.Data.SqlClient.SqlConnection` 创建连接，指定指向本地服务器的连接字符串，然后打开该连接。 这要求指定登录凭据。 连接与存储过程或函数处于不同的数据库会话中，它可能具有不同的 `SET` 选项，位于单独的事务中，找不到临时表等等。 如果托管存储过程或函数代码正在 SQL Server 进程中执行，则是因为有人连接到了该服务器并执行了 SQL 语句调用它。 您可能希望在该连接上下文中执行存储过程或函数，以及其事务、`SET` 选项等。 这称为上下文连接。  
  
 利用上下文连接，您可以在首先调用代码的同一上下文中执行 Transact-SQL 语句。 若要获取上下文连接，您必须使用“context connection”连接字符串关键字，如以下示例所示：  
  
 [C#]  
  
```  
using(SqlConnection connection = new SqlConnection("context connection=true"))   
{  
    connection.Open();  
    // Use the connection  
}  
```  
  
 [Visual Basic]  
  
```  
Using connection as new SqlConnection("context connection=true")  
    connection.Open()  
    ' Use the connection  
End Using  
  
```  
  
## <a name="in-this-section"></a>本节内容  
 [常规连接与上下文连接](context-connections-vs-regular-connections.md)  
 说明常规连接和上下文连接之间的差异。  
  
 [对常规连接和上下文连接的限制](context-connections-and-regular-connections-restrictions.md)  
 说明常规连接和上下文连接的限制。  
  
  