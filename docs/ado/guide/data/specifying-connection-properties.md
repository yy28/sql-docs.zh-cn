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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6fee9745bca206f00603b32a6c4cd29faab34eca
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760833"
---
# <a name="specifying-connection-properties"></a>指定连接属性
可以通过在打开连接之前设置**连接**对象的属性，来提供[连接字符串](../../../ado/guide/data/creating-a-connection-string.md)所指定的大量信息。 例如，你可以通过使用以下代码来实现与[创建连接字符串](../../../ado/guide/data/creating-a-connection-string.md)中所述的连接字符串相同的效果。  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 只有打开连接后才设置 DefaultDatabase。  
  
> [!NOTE]
>  在 ADO 中，不能使用包含分号（";"）的密码，除非密码用单引号引起来。
