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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b5c2e4ed4d8bd64d02fb6a62861db832f6b0898
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300797"
---
# <a name="setting-extendedansisql"></a>设置 ExtendedAnsiSQL
可以通过添加 ExtendedAnsiSQL 属性在连接字符串中控制属性：  
  
|值|说明|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 （默认值）|此设置不会启用新功能。|  
|ExtendedAnsiSQL = 1|此设置启用新功能。|  
  
 通过控制面板配置 DSN 时，还可以通过 "**高级选项**" 对话框在 DSN 中设置该属性。  
  
 将属性设置为0会禁用新功能;将其设置为1可启用新功能。  
  
 还可以使用 SQLSetConnectAttr （）设置该属性。 属性值为65501，并设置为 SQLINTEGER 值1或0，如前面的表中所述。 它可以在连接之前或之后调用，但是，在连接后，最好是在连接后调用它，因为驱动程序处理缓存的连接属性和连接字符串的顺序。
