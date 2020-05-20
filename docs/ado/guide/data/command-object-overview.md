---
title: 命令对象概述 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command object [ADO]
ms.assetid: e84a14b1-3c2a-4f7d-a966-9e08a93948df
author: rothja
ms.author: jroth
ms.openlocfilehash: 0048765d3a5f5cb57419f9dbd755790c9931e218
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761193"
---
# <a name="command-object-overview"></a>命令对象概述
使用**Command**对象，您可以执行以下操作：  
  
-   使用**CommandText**属性定义命令的可执行文本（例如，SQL 语句或存储过程）。  
  
-   使用**参数**对象和**参数**集合定义参数化查询或存储过程参数。  
  
-   执行命令并使用**Execute**方法返回**记录集**对象（如果适用）。  
  
-   通过在执行之前使用**CommandType**属性来指定命令的类型，以优化性能。  
  
-   使用**命令**对象的**方言**属性指定有关命令文本的特定信息。  
  
-   使用**预定义**的属性，控制提供程序是否在执行之前保存命令的准备好的（或编译的）版本。  
  
-   使用**CommandTimeout**属性设置提供程序将等待命令执行的秒数。  
  
-   通过设置其**ActiveConnection**属性，将打开的连接与**命令**对象相关联。  
  
-   设置**名称**属性以将**命令**对象标识为关联的**连接**对象上的方法。  
  
-   将**命令**对象传递到**记录集**的**源**属性，以便获取数据。  
  
-   将包含命令的**流**对象（例如，XML 命令）传递给支持它的提供程序。
