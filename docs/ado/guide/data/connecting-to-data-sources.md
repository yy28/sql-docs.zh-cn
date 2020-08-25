---
description: 连接到数据源
title: 连接到数据源 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 82770486-37bd-4c90-885f-6817a7c77ad7
author: rothja
ms.author: jroth
ms.openlocfilehash: 1de885a14dd2647df08ae6245f64a629d706796d
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806315"
---
# <a name="connecting-to-data-sources"></a>连接到数据源
ADO **连接** 对象表示与数据源的唯一会话，包括 DBMS、文件存储区或逗号分隔的文本文件。 对于客户端/服务器数据库系统，ADO 连接可以是与服务器的实际网络连接。  
  
 **Connection**对象支持不同的[属性和方法](../../reference/ado-api/connection-object-properties-methods-and-events.md)来指定连接配置、打开和关闭连接、针对数据源创建和执行命令，以及以架构行集的形式提供有关基础数据源设计的信息，等等。根据提供程序支持的功能，**连接**对象的某些集合、方法或属性可能不可用。  
  
 您可以通过使用 **连接** 对象或通过使用 **记录集** 对象来连接到数据源。  
  
 本部分包含以下主题。  
  
-   [使用连接对象](./using-a-connection-object.md)  
  
-   [使用记录集对象](./using-a-recordset-object.md)  
  
-   [创建连接字符串](./creating-a-connection-string.md)  
  
-   [指定连接属性](./specifying-connection-properties.md)  
  
-   [控制事务](./controlling-transactions-ado.md)