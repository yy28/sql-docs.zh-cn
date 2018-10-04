---
title: 指定连接属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 885d201736adb3cd16efbea4f3907cd0aa324128
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622755"
---
# <a name="specifying-connection-properties"></a>指定连接属性
你可以提供由指定的信息的大部分[连接字符串](../../../ado/guide/data/creating-a-connection-string.md)通过设置的属性**连接**之前打开连接的对象。 例如，可以达到同样的效果，如连接字符串中所述[创建的连接字符串](../../../ado/guide/data/creating-a-connection-string.md)通过使用下面的代码。  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 只有在您打开连接后设置 DefaultDatabase。  
  
> [!NOTE]
>  在 ADO 中必须不使用包含分号的密码 （";"） 除非密码括在单引号内。
