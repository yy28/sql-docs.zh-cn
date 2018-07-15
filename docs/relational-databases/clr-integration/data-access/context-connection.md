---
title: 上下文连接 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 5d464e257ca7d0f967dfbaf9325f3a30a30f0bc3
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37356859"
---
# <a name="context-connection"></a>上下文连接
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  内部数据访问问题是一种非常常见的情况。 即您希望访问正在执行公共语言运行时 (CLR) 存储过程或函数的相同服务器。 一种选择是创建一个连接使用**System.Data.SqlClient.SqlConnection**，指定指向本地服务器的连接字符串，并打开该连接。 这要求指定登录凭据。 此连接位于不同的数据库会话与存储的过程或函数中，它可能具有不同**设置**选项，位于一个单独的事务，并且不到您的临时表，等等。 如果托管存储过程或函数代码正在 SQL Server 进程中执行，则是因为有人连接到了该服务器并执行了 SQL 语句调用它。 您可能希望存储的过程或函数的该连接，以及其事务上下文中执行**设置**选项，依次类推。 这称为上下文连接。  
  
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
 [常规连接与上下文连接](../../../relational-databases/clr-integration/data-access/context-connections-vs-regular-connections.md)  
 说明常规连接和上下文连接之间的差异。  
  
 [对常规连接和上下文连接的限制](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)  
 说明常规连接和上下文连接的限制。  
  
  
