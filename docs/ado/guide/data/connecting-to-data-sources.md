---
title: 连接到数据源 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 82770486-37bd-4c90-885f-6817a7c77ad7
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d082e3e90f562ef5434bbe1f84964e32ebdd52ab
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-data-sources"></a>连接到数据源
ADO**连接**对象表示与数据源，包括 DBMS、 文件存储区中或以逗号分隔的文本文件的唯一会话。 对于客户端/服务器数据库系统，ADO 连接可以是实际的网络连接到服务器。  
  
 **连接**对象支持各种[属性和方法](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)用于指定连接配置，打开和关闭连接、 创建和执行的命令对数据源并提供有关设计的基础数据源的架构行集窗体中的信息，等等。具体取决于提供程序、 一些集合、 方法或属性的支持的功能**连接**对象可能不可用。  
  
 你可以连接到数据源可通过使用**连接**对象或通过使用**记录集**对象。  
  
 本部分包含以下主题。  
  
-   [使用连接对象](../../../ado/guide/data/using-a-connection-object.md)  
  
-   [使用记录集对象](../../../ado/guide/data/using-a-recordset-object.md)  
  
-   [创建连接字符串](../../../ado/guide/data/creating-a-connection-string.md)  
  
-   [指定连接属性](../../../ado/guide/data/specifying-connection-properties.md)  
  
-   [控制事务](../../../ado/guide/data/controlling-transactions-ado.md)
