---
description: 命令对象概述
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
ms.openlocfilehash: d44c727a69dc74bf243bc2f2c0204cb41cd9f585
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453679"
---
# <a name="command-object-overview"></a>命令对象概述
使用 **Command** 对象，您可以执行以下操作：  
  
-   使用 **CommandText** 属性定义命令的可执行文本 (例如，SQL 语句或存储过程) 。  
  
-   使用 **参数** 对象和 **参数** 集合定义参数化查询或存储过程参数。  
  
-   执行命令并使用**Execute**方法返回**记录集**对象（如果适用）。  
  
-   通过在执行之前使用 **CommandType** 属性来指定命令的类型，以优化性能。  
  
-   使用**命令**对象的**方言**属性指定有关命令文本的特定信息。  
  
-   使用 **预定义** 的属性，控制提供程序是否在执行之前保存已准备的 (或编译的) 版本的命令。  
  
-   使用 **CommandTimeout** 属性设置提供程序将等待命令执行的秒数。  
  
-   通过设置其**ActiveConnection**属性，将打开的连接与**命令**对象相关联。  
  
-   设置 **名称** 属性以将 **命令** 对象标识为关联的 **连接** 对象上的方法。  
  
-   将**命令**对象传递到**记录集**的**源**属性，以便获取数据。  
  
-   传递包含命令 (的 **流** 对象，例如，将 XML 命令) 到支持它的提供程序。
