---
title: "指定连接属性 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6e07a16be9d12aa905abbad4b2007726b853d805
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
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
