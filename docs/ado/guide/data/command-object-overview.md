---
title: 命令对象概述 |Microsoft 文档
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
- command object [ADO]
ms.assetid: e84a14b1-3c2a-4f7d-a966-9e08a93948df
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cdb2d323b57a63d0ffc84044ece0604571d04164
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="command-object-overview"></a>命令对象概述
与**命令**对象，你可以执行以下操作：  
  
-   通过使用定义的命令 （例如，SQL 语句或存储的过程） 的可执行文本**CommandText**属性。  
  
-   通过定义参数化的查询或存储的过程自变量**参数**对象和**参数**集合。  
  
-   执行命令并返回**记录集**对象，如果适当，通过使用**执行**方法。  
  
-   通过使用指定的命令类型**CommandType**属性，然后执行以优化性能。  
  
-   使用指定的命令文本相关的特定信息**方言**属性**命令**对象。  
  
-   控制提供程序是否使用保存在执行之前命令的已准备的 （或已编译的） 版本**已准备**属性。  
  
-   设置提供程序将等待要通过使用执行的命令的秒数**CommandTimeout**属性。  
  
-   将关联的打开连接使用**命令**对象通过设置其**ActiveConnection**属性。  
  
-   设置**名称**属性来标识**命令**作为关联的方法的对象**连接**对象。  
  
-   传递**命令**对象传递给**源**属性**记录集**为了获取数据。  
  
-   传递**流**到提供程序支持它的包含命令 （例如，XML 命令） 的对象。
