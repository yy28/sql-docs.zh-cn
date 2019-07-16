---
title: 设置 ExtendedAnsiSQL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], setting
ms.assetid: 37b775d1-65ac-45ac-8572-454bc4e3c1a2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 330b55ef2d4fee090c453990d3fe75e6e2dacb6f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063602"
---
# <a name="setting-extendedansisql"></a>设置 ExtendedAnsiSQL
该属性可以通过添加 ExtendedAnsiSQL 属性控制在连接字符串中：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 （默认值）|此设置不会启用新功能。|  
|ExtendedAnsiSQL=1|此设置启用了新功能。|  
  
 该属性还可以设置在通过 DSN**高级选项**对话框配置通过控制面板 DSN 时。  
  
 将属性设置为 0 会禁用新的功能;将其设置为 1 启用新功能。  
  
 此外可以使用 SQLSetConnectAttr() 设置该属性。 属性值是 65501 和前面的表中所述设置为 1 或 0，SQLINTEGER 值。 它可以调用之前或之后连接，但更好一些，因为驱动程序进程在其中缓存的连接属性和连接字符串的顺序连接后调用。
