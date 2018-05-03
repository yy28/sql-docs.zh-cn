---
title: 指定连接属性 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca5a8ba0492e93fb886e86233d4bab4a5f84f4ea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="specifying-connection-properties"></a>指定连接属性
你可以提供由指定的信息大部分[连接字符串](../../../ado/guide/data/creating-a-connection-string.md)通过设置属性的**连接**之前打开连接的对象。 例如，无法获得同样的效果，如连接字符串中所述[创建连接字符串](../../../ado/guide/data/creating-a-connection-string.md)通过使用下面的代码。  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 只有在打开连接后，设置 DefaultDatabase。  
  
> [!NOTE]
>  在 ADO 必须不使用包含分号的密码 （";"） 除非密码包含在单引号。
