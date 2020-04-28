---
title: 上下文连接 |Microsoft Docs
description: 在 Microsoft SQL Server 中，上下文连接使你可以在调用代码的上下文中运行 Transact-sql 语句。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f29914557e3a1c1e7a929bec22a2b55d0db2a50
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81485476"
---
# <a name="context-connection"></a>上下文连接
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  内部数据访问问题是一种非常常见的情况。 即您希望访问正在执行公共语言运行时 (CLR) 存储过程或函数的相同服务器。 一个选项是使用**SqlClient**创建一个连接，指定指向本地服务器的连接字符串，然后打开该连接。 这要求指定登录凭据。 连接位于与存储过程或函数不同的数据库会话中，它可能具有不同的**SET**选项，位于不同的事务中，看不到您的临时表等。 如果托管存储过程或函数代码正在 SQL Server 进程中执行，则是因为有人连接到了该服务器并执行了 SQL 语句调用它。 您可能希望存储过程或函数在该连接的上下文中执行，同时还需要在其事务、 **SET**选项等。 这称为上下文连接。  
  
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
  
  
